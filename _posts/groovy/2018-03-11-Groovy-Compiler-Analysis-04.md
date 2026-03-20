---
title: "Groovy实现原理分析——语法分析"
categories:
  - groovy
tags:
  - Groovy
  - 源码分析
  - 编译原理
---

在上一篇文章中我们分析了Groovy的词法分析过程，了解了`GroovyLexer.g4`如何将源代码字符流转换为Token流。本篇我们继续深入，看看Groovy是如何将Token流转换为AST（Abstract Syntax Tree，抽象语法树）的。

## 语法分析的两个阶段

在Groovy 3.0中，语法分析实际上分为两个编译阶段：

- `PARSING`阶段：由Antlr4的Parser将Token流解析为CST（Concrete Syntax Tree，具体语法树，也叫Parse Tree）
- `CONVERSION`阶段：由`AstBuilder`将CST转换为Groovy的AST

这两个阶段在`Antlr4ParserPlugin`中被统一处理。

## GroovyParser.g4——语法规则定义

Groovy的语法规则定义在`src/antlr/GroovyParser.g4`文件中：

```antlr
parser grammar GroovyParser;

options {
    tokenVocab = GroovyLexer;
    contextSuperClass = GroovyParserRuleContext;
    superClass = AbstractParser;
}
```

这里有几个要点：

- `tokenVocab = GroovyLexer`：指定Token词汇表来自`GroovyLexer`，将词法分析器和语法分析器关联起来
- `contextSuperClass = GroovyParserRuleContext`：自定义的规则上下文基类，实现了`NodeMetaDataHandler`接口，可以在Parse Tree节点上附加元数据
- `superClass = AbstractParser`：自定义的Parser基类

### 编译单元规则

语法分析的起始规则是`compilationUnit`：

```antlr
compilationUnit
    :   nls (packageDeclaration sep?)? scriptStatements? EOF
    ;

scriptStatements
    :   scriptStatement (sep scriptStatement)* sep?
    ;

scriptStatement
    :   importDeclaration
    |   typeDeclaration
    |   { !SemanticPredicates.isInvalidMethodDeclaration(_input) }?
        methodDeclaration[3, 9]
    |   statement
    ;
```

一个Groovy编译单元由可选的包声明和一系列脚本语句组成。脚本语句可以是import声明、类型声明、方法声明或普通语句。

注意`methodDeclaration`前面的语义谓词`{ !SemanticPredicates.isInvalidMethodDeclaration(_input) }?`，这是Antlr4的语义谓词机制，用于在语法分析阶段进行额外的语义检查。

### 类声明规则

```antlr
typeDeclaration
    :   classOrInterfaceModifiersOpt classDeclaration
    ;

classOrInterfaceModifier
    :   annotation
    |   m=(   PUBLIC
          |   PROTECTED
          |   PRIVATE
          |   STATIC
          |   ABSTRACT
          |   FINAL
          |   STRICTFP
          |   DEFAULT
          )
    ;
```

### 修饰符规则

Groovy的修饰符系统比Java更灵活，支持`def`和`var`关键字：

```antlr
modifier
    :   classOrInterfaceModifier
    |   m=(   NATIVE
          |   SYNCHRONIZED
          |   TRANSIENT
          |   VOLATILE
          |   DEF
          |   VAR
          )
    ;

variableModifier
    :   annotation
    |   m=( FINAL | DEF | VAR | PUBLIC | PROTECTED | PRIVATE | STATIC | ABSTRACT | STRICTFP )
    ;
```

## CST的构建

CST的构建发生在`AstBuilder.buildCST()`方法中：

```java
private GroovyParserRuleContext buildCST() throws CompilationFailedException {
    GroovyParserRuleContext result;
    try {
        AtnManager.READ_LOCK.lock();
        try {
            result = buildCST(PredictionMode.SLL);
        } catch (Throwable t) {
            if (t instanceof GroovySyntaxError
                    && GroovySyntaxError.LEXER == ((GroovySyntaxError) t).getSource()) {
                throw t;
            }
            result = buildCST(PredictionMode.LL);
        } finally {
            AtnManager.READ_LOCK.unlock();
        }
    } catch (Throwable t) {
        throw convertException(t);
    }
    return result;
}
```

这里使用了Antlr4的两阶段解析策略：

1. 首先尝试`SLL`（Strong LL）模式，这是一种更快但不够强大的解析模式
2. 如果`SLL`模式失败（遇到歧义），则回退到完整的`LL`模式

这种策略在大多数情况下能获得更好的性能，因为大部分Groovy代码不需要完整的LL解析能力。

```java
private GroovyParserRuleContext buildCST(PredictionMode predictionMode) {
    parser.getInterpreter().setPredictionMode(predictionMode);
    if (PredictionMode.SLL.equals(predictionMode)) {
        this.removeErrorListeners();
    } else {
        parser.getInputStream().seek(0);
        this.addErrorListeners();
    }
    return parser.compilationUnit();
}
```

`parser.compilationUnit()`调用的就是`GroovyParser.g4`中定义的`compilationUnit`规则，Antlr4会自动生成对应的解析方法。

## CST到AST的转换——AstBuilder

`AstBuilder`是Groovy 3.0中最核心的类之一，它继承自Antlr4生成的`GroovyParserBaseVisitor`，通过Visitor模式遍历CST，将其转换为Groovy的AST。

```java
public class AstBuilder extends GroovyParserBaseVisitor<Object> {
    private final SourceUnit sourceUnit;
    private final ModuleNode moduleNode;
    private final GroovyLangLexer lexer;
    private final GroovyLangParser parser;
    // ...
}
```

### buildAST方法

```java
public ModuleNode buildAST() {
    try {
        return (ModuleNode) this.visit(this.buildCST());
    } catch (Throwable t) {
        throw convertException(t);
    }
}
```

`buildAST`方法先调用`buildCST()`构建CST，然后通过`this.visit()`遍历CST，触发各个`visitXxx`方法，最终生成`ModuleNode`。

### visitCompilationUnit

```java
@Override
public ModuleNode visitCompilationUnit(CompilationUnitContext ctx) {
    this.visit(ctx.packageDeclaration());

    for (ASTNode node : this.visitScriptStatements(ctx.scriptStatements())) {
        if (node instanceof DeclarationListStatement) {
            for (Statement stmt: ((DeclarationListStatement) node).getDeclarationStatements()) {
                this.moduleNode.addStatement(stmt);
            }
        } else if (node instanceof Statement) {
            this.moduleNode.addStatement((Statement) node);
        } else if (node instanceof MethodNode) {
            this.moduleNode.addMethod((MethodNode) node);
        }
    }

    for (ClassNode node : this.classNodeList) {
        this.moduleNode.addClass(node);
    }

    this.configureScriptClassNode();
    return this.moduleNode;
}
```

这个方法展示了CST到AST转换的核心逻辑：

1. 处理包声明
2. 遍历所有脚本语句，根据类型分别添加到`ModuleNode`中
3. 添加所有类定义
4. 配置脚本类节点

### visitImportDeclaration

以import声明为例，看看一个具体的visit方法是如何工作的：

```java
@Override
public ImportNode visitImportDeclaration(ImportDeclarationContext ctx) {
    ImportNode importNode;
    boolean hasStatic = asBoolean(ctx.STATIC());
    boolean hasStar = asBoolean(ctx.MUL());
    boolean hasAlias = asBoolean(ctx.alias);
    List<AnnotationNode> annotationNodeList = this.visitAnnotationsOpt(ctx.annotationsOpt());
    // ... 根据不同的import形式创建对应的ImportNode
}
```

每个`visitXxx`方法都接收对应的CST上下文节点，从中提取信息，创建对应的AST节点。

## AST的核心节点类型

Groovy的AST由`org.codehaus.groovy.ast`包中的类组成，核心节点类型包括：

- `ModuleNode`：模块节点，代表一个源文件，是AST的根节点
- `ClassNode`：类节点，代表一个类定义
- `MethodNode`：方法节点，代表一个方法定义
- `FieldNode`：字段节点
- `PropertyNode`：属性节点
- `Parameter`：参数节点

表达式节点（`org.codehaus.groovy.ast.expr`包）：

- `VariableExpression`：变量表达式
- `ConstantExpression`：常量表达式
- `BinaryExpression`：二元表达式
- `MethodCallExpression`：方法调用表达式
- `ClosureExpression`：闭包表达式
- `LambdaExpression`：Lambda表达式（Groovy 3.0新增）

语句节点（`org.codehaus.groovy.ast.stmt`包）：

- `BlockStatement`：代码块
- `ExpressionStatement`：表达式语句
- `IfStatement`：if语句
- `ForStatement`：for语句
- `ReturnStatement`：return语句
- `TryCatchStatement`：try-catch语句

## CONVERSION阶段

在`CompilationUnit`中，`CONVERSION`阶段的操作定义如下：

```java
addPhaseOperation(source -> {
    source.convert();
    getAST().addModule(source.getAST());
    Optional.ofNullable(getProgressCallback())
        .ifPresent(callback -> callback.call(source, getPhase()));
}, Phases.CONVERSION);
```

`source.convert()`最终调用`SourceUnit.buildAST()`：

```java
public ModuleNode buildAST() {
    if (null != this.ast) {
        return this.ast;
    }
    try {
        this.ast = parserPlugin.buildAST(this, this.classLoader, this.cst);
        this.ast.setDescription(this.name);
    } catch (SyntaxException e) {
        if (this.ast == null) {
            this.ast = new ModuleNode(this);
        }
        getErrorCollector().addError(new SyntaxErrorMessage(e, this));
    }
    return this.ast;
}
```

这里`parserPlugin.buildAST()`就是`Antlr4ParserPlugin.buildAST()`，它创建`AstBuilder`并调用`buildAST()`完成CST到AST的转换。

## SEMANTIC_ANALYSIS阶段

AST构建完成后，进入语义分析阶段。这个阶段主要做以下工作：

### 变量作用域分析

```java
private final ISourceUnitOperation resolve = (final SourceUnit source) -> {
    for (ClassNode classNode : source.getAST().getClasses()) {
        GroovyClassVisitor visitor = new VariableScopeVisitor(source);
        visitor.visitClass(classNode);

        resolveVisitor.setClassNodeResolver(classNodeResolver);
        resolveVisitor.startResolving(classNode, source);
    }
};
```

`VariableScopeVisitor`负责分析变量的作用域，`ResolveVisitor`负责解析类引用。

### ResolveVisitor

`ResolveVisitor`是语义分析阶段最重要的Visitor之一，它负责将AST中的类名引用解析为实际的`ClassNode`：

```java
public class ResolveVisitor extends ClassCodeExpressionTransformer {
    public static final String[] DEFAULT_IMPORTS = {
        "java.lang.", "java.util.", "java.io.", "java.net.",
        "groovy.lang.", "groovy.util."
    };
    // ...
}
```

注意Groovy默认导入了6个包，这就是为什么在Groovy中可以直接使用`List`、`Map`等类而不需要显式import。

### 其他语义分析操作

`CompilationUnit`在`SEMANTIC_ANALYSIS`阶段还注册了多个操作：

- `StaticImportVisitor`：处理静态导入
- `InnerClassVisitor`：处理内部类
- `GenericsVisitor`：检查泛型的正确性
- `StaticVerifier`：验证静态成员的使用
- `ClassCompletionVerifier`：验证类定义的完整性

## 一个例子

以我们在第一篇中的示例代码为例：

```groovy
package edu.jiangxin.test

class Test {
    static void main(def args) {
        def mygreeting = "Hello World"
        println mygreeting
    }
}
```

经过词法分析后，生成的Token流大致如下：

```
PACKAGE, "edu", DOT, "jiangxin", DOT, "test", NL,
CLASS, "Test", LBRACE, NL,
STATIC, VOID, "main", LPAREN, DEF, "args", RPAREN, LBRACE, NL,
DEF, "mygreeting", ASSIGN, StringLiteral("Hello World"), NL,
"println", "mygreeting", NL,
RBRACE, NL,
RBRACE, EOF
```

经过语法分析后，生成的AST结构大致如下：

```
ModuleNode
  └── ClassNode (Test)
        └── MethodNode (main)
              └── BlockStatement
                    ├── ExpressionStatement
                    │     └── DeclarationExpression
                    │           ├── VariableExpression (mygreeting)
                    │           └── ConstantExpression ("Hello World")
                    └── ExpressionStatement
                          └── MethodCallExpression
                                ├── VariableExpression (this)
                                ├── ConstantExpression ("println")
                                └── ArgumentListExpression
                                      └── VariableExpression (mygreeting)
```

## 小结

Groovy 3.0的语法分析基于Antlr4实现，核心文件是`GroovyParser.g4`和`AstBuilder.java`。语法分析分为两步：首先由Antlr4的Parser将Token流解析为CST，然后由`AstBuilder`通过Visitor模式将CST转换为Groovy的AST。语义分析阶段则通过多个Visitor对AST进行类型解析、作用域分析等处理。

下一篇我们将分析Groovy如何利用ASM将AST转换为JVM字节码。

（未完待续）
