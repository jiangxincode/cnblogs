---
title: "Groovy实现原理分析——生成JVM字节码"
categories:
  - groovy
tags:
  - Groovy
  - 源码分析
  - 编译原理
---

在前两篇文章中我们分析了Groovy的词法分析和语法分析过程，了解了源代码是如何被转换为AST的。本篇我们来看编译过程的最后一个关键步骤：如何将AST转换为JVM可以执行的字节码。

## 字节码生成的编译阶段

字节码生成涉及三个编译阶段：

- `CANONICALIZATION`（阶段5）：完善AST，包括Trait组合、枚举补全等
- `INSTRUCTION_SELECTION`（阶段6）：选择指令集，处理静态编译相关的转换
- `CLASS_GENERATION`（阶段7）：实际的字节码生成

## CLASS_GENERATION阶段的入口

字节码生成的核心逻辑在`CompilationUnit`的`classgen`回调中：

```java
private final IPrimaryClassNodeOperation classgen = new IPrimaryClassNodeOperation() {
    @Override
    public void call(final SourceUnit source, final GeneratorContext context,
                     final ClassNode classNode) throws CompilationFailedException {
        // 1. 优化
        new OptimizerVisitor(CompilationUnit.this).visitClass(classNode, source);

        // 2. 验证
        GroovyClassVisitor visitor = new Verifier();
        visitor.visitClass(classNode);

        visitor = new LabelVerifier(source);
        visitor.visitClass(classNode);

        visitor = new ClassCompletionVerifier(source);
        visitor.visitClass(classNode);

        visitor = new ExtendedVerifier(source);
        visitor.visitClass(classNode);

        getErrorCollector().failIfErrors();

        // 3. 创建ClassVisitor
        ClassVisitor classVisitor = createClassVisitor();

        // 4. 生成字节码
        visitor = new AsmClassGenerator(source, context, classVisitor, sourceName);
        visitor.visitClass(classNode);

        // 5. 获取字节码
        byte[] bytes = ((ClassWriter) classVisitor).toByteArray();
        getClasses().add(new GroovyClass(classNode.getName(), bytes));

        // 6. 递归处理内部类
        LinkedList<ClassNode> innerClasses = ((AsmClassGenerator) visitor).getInnerClasses();
        while (!innerClasses.isEmpty()) {
            classgen.call(source, context, innerClasses.removeFirst());
        }
    }
};
```

整个流程清晰明了：先验证AST的正确性，然后通过`AsmClassGenerator`遍历AST生成字节码，最后递归处理内部类。

## Verifier——AST的最终完善

在字节码生成之前，`Verifier`会对AST做最后的完善工作。这是一个非常重要的步骤，它会为Groovy类添加许多"隐藏"的成员：

```java
public class Verifier implements GroovyClassVisitor, Opcodes {
    @Override
    public void visitClass(final ClassNode node) {
        addDefaultParameterMethods(node);
        addDefaultParameterConstructors(node);
        addStaticMetaClassField(node, classInternalName);
        addFastPathHelperFieldsAndHelperMethod(node, classInternalName, knownSpecialCase);
        if (!knownSpecialCase) addGroovyObjectInterfaceAndMethods(node, classInternalName);
        addDefaultConstructor(node);
        addInitialization(node);
        // ...
    }
}
```

`Verifier`做的关键工作包括：

1. 为有默认参数的方法生成重载方法
2. 添加`metaClass`字段和`$getStaticMetaClass()`方法
3. 添加`__$stMC`静态字段（用于快速路径优化）
4. 实现`GroovyObject`接口的`getMetaClass()`和`setMetaClass()`方法
5. 添加默认构造函数

这就解释了我们在第一篇文章中看到的反编译结果——那些看起来"多余"的字段和方法都是`Verifier`添加的。

## ClassWriter的创建

```java
protected ClassVisitor createClassVisitor() {
    CompilerConfiguration config = getConfiguration();
    int computeMaxStackAndFrames = ClassWriter.COMPUTE_MAXS;
    if (CompilerConfiguration.isPostJDK7(config.getTargetBytecode()) || config.isIndyEnabled()) {
        computeMaxStackAndFrames += ClassWriter.COMPUTE_FRAMES;
    }
    return new ClassWriter(computeMaxStackAndFrames) {
        // 重写getCommonSuperClass以支持编译期类型解析
        @Override
        protected String getCommonSuperClass(String type1, String type2) {
            // ...
        }
    };
}
```

`ClassWriter`是ASM库的核心类，`COMPUTE_MAXS`让ASM自动计算操作数栈的最大深度和局部变量表的大小，`COMPUTE_FRAMES`让ASM自动计算栈帧映射（JDK 7+要求）。

## AsmClassGenerator——字节码生成的核心

`AsmClassGenerator`继承自`ClassGenerator`，是字节码生成的核心类：

```java
public class AsmClassGenerator extends ClassGenerator {
    private WriterController controller;
    private final SourceUnit source;
    private final GeneratorContext context;
    private ClassVisitor classVisitor;
    private final String sourceFile;
}
```

### visitClass——生成类结构

```java
@Override
public void visitClass(final ClassNode classNode) {
    referencedClasses.clear();
    WriterController normalController = new WriterController();
    this.controller = normalController;
    this.controller.init(this, context, classVisitor, classNode);

    int bytecodeVersion = controller.getBytecodeVersion();
    classVisitor.visit(
            bytecodeVersion,
            adjustedClassModifiersForClassWriting(classNode),
            controller.getInternalClassName(),
            BytecodeHelper.getGenericsSignature(classNode),
            controller.getInternalBaseClassName(),
            BytecodeHelper.getClassInternalNames(classNode.getInterfaces())
    );
    classVisitor.visitSource(sourceFile, null);

    // 处理注解
    visitAnnotations(classNode, classVisitor);

    if (classNode.isInterface()) {
        super.visitClass(classNode);
        createInterfaceSyntheticStaticFields();
    } else {
        super.visitClass(classNode);
        MopWriter mopWriter = mopWriterFactory.create(controller);
        mopWriter.createMopMethods();
        controller.getCallSiteWriter().generateCallSiteArray();
        createSyntheticStaticFields();
    }

    classVisitor.visitEnd();
}
```

这个方法的核心流程：

1. 初始化`WriterController`
2. 调用`classVisitor.visit()`生成类的基本结构（版本号、访问标志、类名、父类、接口）
3. 遍历类的所有成员（字段、方法、属性等）
4. 生成MOP（Meta-Object Protocol）方法
5. 生成CallSite数组
6. 调用`classVisitor.visitEnd()`结束类的生成

### visitConstructorOrMethod——生成方法字节码

```java
@Override
protected void visitConstructorOrMethod(final MethodNode node, final boolean isConstructor) {
    Parameter[] parameters = node.getParameters();
    String methodType = BytecodeHelper.getMethodDescriptor(node.getReturnType(), parameters);
    String signature = BytecodeHelper.getGenericsMethodSignature(node);
    int modifiers = node.getModifiers();
    if (isVargs(node.getParameters())) modifiers |= ACC_VARARGS;

    MethodVisitor mv = classVisitor.visitMethod(
            modifiers, node.getName(), methodType, signature,
            buildExceptions(node.getExceptions()));
    controller.setMethodVisitor(mv);

    // 处理注解
    visitAnnotations(node, mv);
    for (int i = 0, n = parameters.length; i < n; i += 1) {
        visitParameterAnnotations(parameters[i], i, mv);
    }

    // 生成方法体
    if (!node.isAbstract()) {
        // ... 生成方法体的字节码
    }
}
```

## WriterController——字节码生成的协调者

`WriterController`是字节码生成过程中的协调者，它管理着多个专门的Writer：

```java
public class WriterController {
    private AsmClassGenerator acg;
    private MethodVisitor methodVisitor;
    private CompileStack compileStack;
    private OperandStack operandStack;
    private ClassNode classNode;
    private CallSiteWriter callSiteWriter;
    private ClassVisitor cv;
    private ClosureWriter closureWriter;
    private LambdaWriter lambdaWriter;
    private InvocationWriter invocationWriter;
    private BinaryExpressionHelper binaryExpHelper;
    private UnaryExpressionHelper unaryExpressionHelper;
    private AssertionWriter assertionWriter;
    private StatementWriter statementWriter;
    // ...
}
```

各个Writer的职责：

- `CallSiteWriter`：生成方法调用的CallSite机制代码
- `ClosureWriter`：生成闭包相关的字节码
- `LambdaWriter`：生成Lambda表达式相关的字节码
- `InvocationWriter`：生成方法调用的字节码
- `BinaryExpressionHelper`：生成二元表达式的字节码
- `StatementWriter`：生成语句的字节码
- `CompileStack`：管理编译期的栈帧信息
- `OperandStack`：管理操作数栈

### InvokeDynamic支持

`WriterController`在初始化时会根据配置选择不同的Writer实现：

```java
public void init(final AsmClassGenerator asmClassGenerator, final GeneratorContext gcon,
                 final ClassVisitor cv, final ClassNode cn) {
    // ...
    if (invokedynamic) {
        this.invocationWriter = new InvokeDynamicWriter(this);
        this.callSiteWriter = new IndyCallSiteWriter(this);
        this.binaryExpHelper = new IndyBinHelper(this);
    } else {
        this.callSiteWriter = new CallSiteWriter(this);
        this.invocationWriter = new InvocationWriter(this);
        this.binaryExpHelper = new BinaryExpressionHelper(this);
    }
    // ...
}
```

当启用InvokeDynamic时，会使用`InvokeDynamicWriter`和`IndyCallSiteWriter`，利用JVM的`invokedynamic`指令来实现动态方法调用，这可以获得更好的性能。

## CallSite机制

Groovy的动态方法调用是通过CallSite机制实现的。在第一篇文章中我们看到反编译后的代码中有`$getCallSiteArray()`方法，这就是CallSite机制的体现。

`CallSiteWriter`负责生成CallSite数组：

```java
// 在AsmClassGenerator.visitClass中
controller.getCallSiteWriter().generateCallSiteArray();
```

对于每一个动态方法调用，编译器会在CallSite数组中分配一个槽位。运行时，第一次调用时会解析实际的方法，后续调用则直接使用缓存的结果，避免重复解析。

## MOP方法

MOP（Meta-Object Protocol）方法是Groovy实现动态特性的基础。`MopWriter`负责生成这些方法：

```java
MopWriter mopWriter = mopWriterFactory.create(controller);
mopWriter.createMopMethods();
```

MOP方法使得Groovy可以在运行时拦截和修改方法调用行为，这是`methodMissing`、`propertyMissing`等动态特性的基础。

## OUTPUT阶段

字节码生成完成后，进入`OUTPUT`阶段，将字节码写入文件系统：

```java
addPhaseOperation(groovyClass -> {
    String name = groovyClass.getName().replace('.', File.separatorChar) + ".class";
    File path = new File(getConfiguration().getTargetDirectory(), name);

    File directory = path.getParentFile();
    if (directory != null && !directory.exists()) {
        directory.mkdirs();
    }

    try (FileOutputStream stream = new FileOutputStream(path)) {
        byte[] bytes = groovyClass.getBytes();
        stream.write(bytes, 0, bytes.length);
    } catch (IOException e) {
        getErrorCollector().addError(Message.create(e.getMessage(), this));
    }
});
```

## 一个完整的例子

回到我们在第一篇中的示例，看看`println mygreeting`这行代码是如何被编译的。

在AST中，这行代码被表示为：

```
MethodCallExpression
  ├── object: VariableExpression(this)
  ├── method: ConstantExpression("println")
  └── arguments: ArgumentListExpression
        └── VariableExpression(mygreeting)
```

经过字节码生成后，大致会产生如下字节码（伪代码）：

```
// CallSite[] var1 = $getCallSiteArray();
INVOKESTATIC Test.$getCallSiteArray ()[Lorg/codehaus/groovy/runtime/callsite/CallSite;
ASTORE 1

// var1[0].callStatic(Test.class, mygreeting);
ALOAD 1
ICONST_0
AALOAD
LDC Test.class
ALOAD mygreeting
INVOKEINTERFACE CallSite.callStatic (Ljava/lang/Class;Ljava/lang/Object;)Ljava/lang/Object;
```

`println`调用被转换为通过CallSite的`callStatic`方法进行的间接调用。运行时，CallSite会解析到`DefaultGroovyMethods.println()`方法。

## 编译全流程总结

至此，我们已经完整地分析了Groovy编译器的三个核心阶段。整个编译流程可以总结为：

```
源代码 (.groovy)
    │
    ▼ GroovyLexer (Antlr4)
Token流
    │
    ▼ GroovyParser (Antlr4)
CST (Concrete Syntax Tree)
    │
    ▼ AstBuilder (Visitor模式)
AST (Abstract Syntax Tree)
    │
    ▼ ResolveVisitor, VariableScopeVisitor 等
完善的AST
    │
    ▼ Verifier
添加了运行时支持代码的AST
    │
    ▼ AsmClassGenerator + WriterController (ASM)
字节码 (byte[])
    │
    ▼ FileOutputStream
.class 文件
```

Groovy编译器的设计体现了良好的关注点分离：Antlr4负责词法分析和语法分析，多个Visitor负责语义分析和AST完善，ASM负责字节码生成。每个阶段都有清晰的输入和输出，便于理解和维护。

## 参考资料

* Groovy 3.0.5 源码：<https://github.com/apache/groovy/tree/GROOVY_3_0_5>
* ASM 官方文档：<https://asm.ow2.io/asm4-guide.pdf>
* Antlr4 官方文档：<https://github.com/antlr/antlr4/blob/master/doc/index.md>
* JVM 规范：<https://docs.oracle.com/javase/specs/jvms/se8/html/>

（全文完）
