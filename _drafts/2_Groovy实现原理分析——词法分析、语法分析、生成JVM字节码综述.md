# Groovy实现原理分析——词法分析、语法分析、生成JVM字节码综述

在上一篇文中中我们提到Groovy编译器将Groovy脚本编译成JVM可以执行的字节码文件，这之中涉及词法分析、语法分析、生成JVM字节码的过程，学过编译原理的同学可能会对这些概念比较熟悉，不熟悉也没关系，我们简单回忆一下一般编译器的编译过程。首先给出一张龙书中的示意图：

![编译过程示意图](https://images2018.cnblogs.com/blog/611264/201803/611264-20180311224530074-1999481514.png)

以一个很简单的表达式`position = initial + rate * 60`为例，要想生成机器可以执行的机器码或者汇编语言的话，要经过如下几个步骤：

* 词法分析器将输入表达式按照预定规则分隔为一系列的词素单元。
* 语法分析器将词素单元按照预定规则生成语法树。
* 语义分析器进行类型检查等语义分析。
* 中间代码生成器将语义分析之后的结果生成机器无关的代码。

## 参考资料

* Aho A V. Compilers: principles, techniques and tools (for Anna University), 2/e[M]. Pearson Education India, 2003.
* Parr T. The definitive ANTLR 4 reference[M]. Pragmatic Bookshelf, 2013.
* Bruneton E. ASM 4.0: A Java bytecode engineering library, Sept. 2011[J]. URL http://download.forge.objectweb.org/asm/asm4-guide.pdf. Version, 2.