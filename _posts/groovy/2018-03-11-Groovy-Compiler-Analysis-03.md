---
title: "Groovy实现原理分析——词法分析"
categories:
  - groovy
tags:
  - Groovy
  - 源码分析
  - 编译原理
---

在上一篇文章中我们介绍了编译器的基本流程以及Groovy编译器所使用的工具（Antlr和ASM），本篇我们深入Groovy 3.0.5的源码，看看Groovy是如何利用Antlr4实现词法分析的。

## 编译阶段概览

在分析词法分析之前，我们先看一下Groovy编译器定义的所有编译阶段。打开`org.codehaus.groovy.control.CompilePhase`，可以看到Groovy定义了9个编译阶段：

```java
public enum CompilePhase {
    INITIALIZATION(Phases.INITIALIZATION),   // 打开源文件，配置环境
    PARSING(Phases.PARSING),                 // 利用语法规则生成Token树
    CONVERSION(Phases.CONVERSION),           // 将Token树转换为AST
    SEMANTIC_ANALYSIS(Phases.SEMANTIC_ANALYSIS), // 语义分析，检查一致性和有效性
    CANONICALIZATION(Phases.CANONICALIZATION),    // 完善AST
    INSTRUCTION_SELECTION(Phases.INSTRUCTION_SELECTION), // 选择指令集
    CLASS_GENERATION(Phases.CLASS_GENERATION),   // 在内存中生成字节码
    OUTPUT(Phases.OUTPUT),                   // 将字节码写入文件系统
    FINALIZATION(Phases.FINALIZATION),       // 最终清理
}
```

词法分析发生在`PARSING`阶段，由`SourceUnit.parse()`方法触发。

## 词法分析的入口

词法分析的入口在`SourceUnit.parse()`方法中：

```java
public void parse() throws CompilationFailedException {
    if (this.phase > Phases.PARSING) {
        throw new GroovyBugError("parsing is already complete");
    }
    if (this.phase == Phases.INITIALIZATION) {
        nextPhase();
    }
    try (Reader reader = source.getReader()) {
        parserPlugin = getConfiguration().getPluginFactory().createParserPlugin();
        cst = parserPlugin.parseCST(this, reader);
    } catch (IOException e) {
        getErrorCollector().addFatalError(new SimpleMessage(e.getMessage(), this));
    }
}
```

这里有一个关键的设计：`ParserPlugin`接口。Groovy通过这个接口实现了解析器的可插拔机制：

```java
public interface ParserPlugin {
    Reduction parseCST(SourceUnit sourceUnit, Reader reader) throws CompilationFailedException;
    ModuleNode buildAST(SourceUnit sourceUnit, ClassLoader classLoader, Reduction cst) throws ParserException;
}
```

在Groovy 3.0中，默认使用的是基于Antlr4的新解析器（代号Parrot），对应的实现类是`Antlr4ParserPlugin`。旧版本使用的是基于Antlr2的`AntlrParserPlugin`。

## Antlr4ParserPlugin

我们来看`Antlr4ParserPlugin`的实现：

```java
public class Antlr4ParserPlugin implements ParserPlugin {
    @Override
    public Reduction parseCST(final SourceUnit sourceUnit, final Reader reader) {
        if (!sourceUnit.getSource().canReopenSource()) {
            try {
                sourceUnit.setSource(new StringReaderSource(
                        IOGroovyMethods.getText(reader),
                        sourceUnit.getConfiguration()
                ));
            } catch (IOException e) {
                throw new GroovyBugError("Failed to create StringReaderSource", e);
            }
        }
        return null;
    }

    @Override
    public ModuleNode buildAST(final SourceUnit sourceUnit, final ClassLoader classLoader, final Reduction cst) {
        AstBuilder builder = new AstBuilder(sourceUnit,
                sourceUnit.getConfiguration().isGroovydocEnabled(),
                sourceUnit.getConfiguration().isRuntimeGroovydocEnabled()
        );
        return builder.buildAST();
    }
}
```

注意这里`parseCST`方法返回了`null`。这是因为Groovy 3.0的新解析器将词法分析和语法分析合并到了`AstBuilder.buildAST()`中一起完成，不再像旧版本那样先生成CST（Concrete Syntax Tree）再转换为AST。但词法分析仍然是一个独立的步骤，由Antlr4的Lexer完成。

## GroovyLexer.g4——词法规则定义

Groovy的词法规则定义在`src/antlr/GroovyLexer.g4`文件中。这是一个标准的Antlr4词法规则文件，定义了Groovy语言中所有合法的Token类型。

### 文件头部

```antlr
lexer grammar GroovyLexer;

options {
    superClass = AbstractLexer;
}
```

`GroovyLexer`继承自`AbstractLexer`，这是Groovy自定义的一个基类，提供了一些辅助方法。

### 关键字定义

Groovy的关键字包括Java的所有关键字，以及Groovy特有的关键字：

```antlr
// Groovy特有关键字
AS              : 'as';
DEF             : 'def';
IN              : 'in';
TRAIT           : 'trait';
THREADSAFE      : 'threadsafe'; // 保留关键字
VAR             : 'var';

// Java关键字
ABSTRACT      : 'abstract';
ASSERT        : 'assert';
BREAK         : 'break';
CASE          : 'case';
// ... 其他Java关键字
```

### 基本类型

Groovy将基本类型定义为一个复合Token：

```antlr
BuiltInPrimitiveType
    :   BOOLEAN
    |   CHAR
    |   BYTE
    |   SHORT
    |   INT
    |   LONG
    |   FLOAT
    |   DOUBLE
    ;
```

### 字符串字面量

Groovy支持多种字符串形式，这是词法分析中最复杂的部分之一：

```antlr
StringLiteral
    :   GStringQuotationMark    DqStringCharacter* GStringQuotationMark      // 双引号字符串 "..."
    |   SqStringQuotationMark   SqStringCharacter* SqStringQuotationMark      // 单引号字符串 '...'
    |   Slash SlashyStringCharacter+ Slash                                     // 斜杠字符串 /.../
    |   TdqStringQuotationMark  TdqStringCharacter* TdqStringQuotationMark    // 三双引号字符串 """..."""
    |   TsqStringQuotationMark  TsqStringCharacter* TsqStringQuotationMark    // 三单引号字符串 '''...'''
    |   DollarSlashyGStringQuotationMarkBegin DollarSlashyStringCharacter+
        DollarSlashyGStringQuotationMarkEnd                                    // $/..../$ 字符串
    ;
```

### GString的词法处理

GString（Groovy String，即支持插值的字符串）的词法处理是Groovy词法分析中最精妙的部分。Antlr4的Lexer Mode机制在这里发挥了关键作用：

```antlr
GStringBegin
    :   GStringQuotationMark DqStringCharacter* Dollar
        -> pushMode(DQ_GSTRING_MODE), pushMode(GSTRING_TYPE_SELECTOR_MODE)
    ;
```

当词法分析器遇到`"...${`这样的模式时，它会：

1. 识别出`GStringBegin` Token
2. 通过`pushMode`切换到`DQ_GSTRING_MODE`和`GSTRING_TYPE_SELECTOR_MODE`

在`GSTRING_TYPE_SELECTOR_MODE`中，词法分析器会判断`$`后面跟的是`{`（表达式插值）还是标识符（简单变量插值）：

```antlr
mode GSTRING_TYPE_SELECTOR_MODE;
GStringLBrace
    :   '{' { this.enterParen(); }
        -> type(LBRACE), popMode, pushMode(DEFAULT_MODE)
    ;
GStringIdentifier
    :   IdentifierInGString
        -> type(Identifier), popMode, pushMode(GSTRING_PATH_MODE)
    ;
```

这种多模式切换机制使得词法分析器能够正确处理嵌套的GString表达式，比如`"Hello ${name}, you are ${age} years old"`。

### 数字字面量

Groovy支持多种数字格式：

```antlr
IntegerLiteral
    :   (   DecimalIntegerLiteral
        |   HexIntegerLiteral
        |   OctalIntegerLiteral
        |   BinaryIntegerLiteral
        ) (Underscore { require(false, "Number ending with underscores is invalid", -1, true); })?
    ;
```

### 括号匹配与换行处理

Groovy词法分析器中有一个重要的特性：在括号内部忽略换行符。这是通过一个括号栈实现的：

```java
private final Deque<Paren> parenStack = new ArrayDeque<>(32);

private void enterParen() {
    String text = getText();
    enterParenCallback(text);
    parenStack.push(new Paren(text, this.lastTokenType, getLine(), getCharPositionInLine()));
}

private void exitParen() {
    String text = getText();
    exitParenCallback(text);
    Paren paren = parenStack.peek();
    if (null == paren) return;
    parenStack.pop();
}

private boolean isInsideParens() {
    Paren paren = parenStack.peek();
    if (null == paren) return false;
    return ("(".equals(paren.getText()) && TRY != paren.getLastTokenType())
                || "[".equals(paren.getText());
}
```

当词法分析器检测到当前位于`(`或`[`内部时，换行符会被放入隐藏通道（`HIDDEN_CHANNEL`），不会传递给语法分析器。这就是为什么在Groovy中可以这样写代码：

```groovy
def list = [1,
            2,
            3]
```

### 正则表达式与除法的歧义

Groovy中`/`既可以是除法运算符，也可以是正则表达式的定界符。词法分析器通过`isRegexAllowed()`方法来判断：

```java
private boolean isRegexAllowed() {
    if (Arrays.binarySearch(REGEX_CHECK_ARRAY, this.lastTokenType) >= 0) {
        return false;
    }
    return true;
}
```

如果前一个Token是标识符、数字字面量、右括号等，则`/`被识别为除法运算符；否则被识别为正则表达式的开始。

## 词法分析的执行流程

在`AstBuilder`的构造函数中，词法分析器被创建并与语法分析器串联：

```java
public AstBuilder(final SourceUnit sourceUnit, final boolean groovydocEnabled,
                  final boolean runtimeGroovydocEnabled) {
    this.sourceUnit = sourceUnit;
    this.moduleNode = new ModuleNode(sourceUnit);
    CharStream charStream = createCharStream(sourceUnit);

    this.lexer = new GroovyLangLexer(charStream);
    this.parser = new GroovyLangParser(new CommonTokenStream(this.lexer));
    this.parser.setErrorHandler(new DescriptiveErrorStrategy(charStream));
    // ...
}
```

整个流程如下：

1. 从`SourceUnit`获取源代码，创建`CharStream`
2. 将`CharStream`传入`GroovyLangLexer`（`GroovyLexer.g4`生成的词法分析器的子类）
3. 词法分析器将字符流转换为`CommonTokenStream`（Token流）
4. Token流传入`GroovyLangParser`供语法分析使用

## GroovySourceToken

在旧版本的Antlr2解析器中，Groovy使用`GroovySourceToken`来表示一个Token，它包含了Token的类型、文本内容以及源码位置信息：

```java
public class GroovySourceToken extends Token implements SourceInfo {
    protected int line;
    protected String text = "";
    protected int col;
    protected int lineLast;
    protected int colLast;

    public String toString() {
        return "[\"" + getText() + "\",<" + type + ">," +
            "line=" + line + ",col=" + col +
            ",lineLast=" + lineLast + ",colLast=" + colLast + "]";
    }
}
```

在Antlr4的新解析器中，Token由Antlr4运行时库的`org.antlr.v4.runtime.Token`接口表示，包含了类似的信息。

## 小结

Groovy 3.0的词法分析基于Antlr4实现，核心文件是`GroovyLexer.g4`。词法分析器的主要职责是将源代码字符流转换为Token流，其中最复杂的部分是GString的多模式处理和正则表达式与除法运算符的歧义消解。词法分析器通过括号栈实现了括号内换行符的忽略，这是Groovy语法灵活性的基础之一。

下一篇我们将分析Groovy的语法分析过程，看看Token流是如何被转换为AST的。

（未完待续）
