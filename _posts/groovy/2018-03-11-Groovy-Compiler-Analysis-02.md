---
title: "Groovy实现原理分析——词法分析、语法分析、生成JVM字节码综述"
categories:
  - others
tags:
  - Groovy
  - 源码分析
  - 编译原理
---

在上一篇文中中我们提到Groovy编译器将Groovy脚本编译成JVM可以执行的字节码文件，这之中涉及词法分析、语法分析、生成JVM字节码的过程，学过编译原理的同学可能会对这些概念比较熟悉，不熟悉也没关系，我们简单回忆一下一般编译器的编译过程。首先给出一张龙书中的示意图：

![编译过程示意图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2018031101.png)

以一个很简单的表达式`position = initial + rate * 60`为例，要想生成机器可以执行的机器码或者JVM可以执行的字节码的话，最少需要执行以下几个步骤：

* 词法分析器（Lexical Analyzer）将输入表达式按照预定规则分隔为一系列的词素单元。
* 语法分析器（Syntax Analyzer）将词素单元按照预定规则生成语法树。
* 语义分析器（Semantic Analyzer）将语法树进行语义分析，比如检查变量是否定义，检查类型是否匹配等。
* 代码生成器（Code Generator）将语义分析之后的结果生成机器码或者JVM字节码。

当然这是简单到不能再简单的编译过程，真实情况下大多数编译期会做的更多，比如生成统一的中间代码进行优化后再生成机器码等。本系列文章的目的不是详细介绍编译原理，而是介绍Groovy编译器是如何实现这些过程的。如果你希望了更加详细的了解编译原理，龙书是我认为最好的学习资料。

![编译过程示意图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2018031102.png)

## 相关工具

现在手撸词法分析器、语法分析器、语义分析器、代码生成器这些工具很少见了，大部分还是会借助一些工具，Groovy的编译过程也不例外。下面我们介绍一些常用的工具。

词法分析生成器（专门用于生成词法分析器，一般称作: Lexical Analyzer Generator）:

* LEX: <http://dinosaur.compilertools.net/#lex>
* flex: <https://github.com/westes/flex>
* Jflex: <https://github.com/jflex-de/jflex>

语法分析生成器（专门用于生成语法分析器，一般称作Parser Generator）:

* YACC: <http://dinosaur.compilertools.net/#yacc>
* Bison: <https://www.gnu.org/software/bison/>
* CUP: <http://www2.cs.tum.edu/projects/cup/>

词法分析生成器+语法分析器生成器：

* JavaCC: <https://javacc.org/>
* Antlr: <https://www.antlr.org/>

字节码生成器：

* ASM: <https://asm.ow2.io/>
* CGLIB(Spring AOP): <https://github.com/cglib/cglib>
* Javaassist(Jboss AOP): <https://github.com/jboss-javassist/javassist>

All-In-One:

* Xtext: <https://eclipse.dev/Xtext/>
* MPS: <https://www.jetbrains.com/mps/>

接下来我们介绍如何使用Antlr+ASM实现Groovy的词法分析、语法分析、生成JVM字节码。

## 一个例子了解Antrl

假如我们希望做这样一种转化:把一个short类型的数组转换成一个Unicode表示的字符串。

```java
// from
static short[] data = {1, 2, 3};

// to
static String data = "\u0001\u0002\u0003";
```

要想实现这个转化，我们首先需要一个词法分析器，词法分析器需要将这些字符分成一个个的词素单元，比如数字、字母、符号等。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2018031103.png)

然后我们通过Antlr来生成词法分析器。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2018031104.png)

默认生成的词法分析器是将识别到的内容打印:

```java
/** Convert short array inits like {1,2,3} to "\u0001\u0002\u0003" */
public class ShortToUnicodeString extends ArrayInitBaseListener {
    /** Translate { to " */
    @Override
    public void enterInit(ArrayInitParser.InitContext ctx) {
        System.out.print('"');
    }
    /** Translate } to " */
    @Override
    public void exitInit(ArrayInitParser.InitContext ctx) {
        System.out.print('"');
    }
    /** Translate integers to 4-digit hexadecimal strings prefixed with \\u */
    @Override
    public void enterValue(ArrayInitParser.ValueContext ctx) {
        // Assumes no nested array initializers
        int value = Integer.valueOf(ctx.INT().getText());
        System.out.printf("\\u%04x", value);
    }
}
```

然后我们写一个调用类:

```java
// import ANTLR's runtime libraries
import org.antlr.v4.runtime.*;
import org.antlr.v4.runtime.tree.*;
public class Translate {
    public static void main(String[] args) throws Exception {
        // create a CharStream that reads from standard input
        ANTLRInputStream input = new ANTLRInputStream(System.in);
        // create a lexer that feeds off of input CharStream
        ArrayInitLexer lexer = new ArrayInitLexer(input);
        // create a buffer of tokens pulled from the lexer
        CommonTokenStream tokens = new CommonTokenStream(lexer);
        // create a parser that feeds off the tokens buffer
        ArrayInitParser parser = new ArrayInitParser(tokens);
        ParseTree tree = parser.init(); // begin parsing at init rule
        // Create a generic parse tree walker that can trigger callbacks
        ParseTreeWalker walker = new ParseTreeWalker();
        // Walk the tree created during the parse, trigger callbacks
        walker.walk(new ShortToUnicodeString(), tree);
        System.out.println(); // print a \n after translation
    }
}
```

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2018031105.png)

## 一个例子了解ASM

假如我们想构造这样一个类：

```java
package pkg;
public interface Comparable extends Mesurable {
    int LESS = -1;
    int EQUAL = 0;
    int GREATER = 1;
    int compareTo(Object o);
}
```

使用ClassVisitor生成这个类的字节码，需要调用6个方法：

```java
ClassWriter cw = new ClassWriter(0);
cw.visit(V1_5, ACC_PUBLIC + ACC_ABSTRACT + ACC_INTERFACE, "pkg/Comparable", null, "java/lang/Object", new String[] { "pkg/Mesurable" });
cw.visitField(ACC_PUBLIC + ACC_FINAL + ACC_STATIC, "LESS", "I", null, new Integer(-1)).visitEnd();
cw.visitField(ACC_PUBLIC + ACC_FINAL + ACC_STATIC, "EQUAL", "I", null, new Integer(0)).visitEnd();
cw.visitField(ACC_PUBLIC + ACC_FINAL + ACC_STATIC, "GREATER", "I", null, new Integer(1)).visitEnd();
cw.visitMethod(ACC_PUBLIC + ACC_ABSTRACT, "compareTo", "(Ljava/lang/Object;)I", null, null).visitEnd();
cw.visitEnd();
byte[] b = cw.toByteArray();
```

## 参考资料

* Aho A V. Compilers: principles, techniques and tools (for Anna University), 2/e[M]. Pearson Education India, 2003.
* Parr T. The definitive ANTLR 4 reference[M]. Pragmatic Bookshelf, 2013.
* Bruneton E. ASM 4.0: A Java bytecode engineering library, Sept. 2011[J]. URL http://download.forge.objectweb.org/asm/asm4-guide.pdf. Version, 2.

（未完待续）
