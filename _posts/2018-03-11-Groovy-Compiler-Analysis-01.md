---
title: "Groovy实现原理分析——准备工作"
categories:
  - Blog
tags:
  - Groovy
  - 源码分析
  - 编译原理
---

首先说明一下为什么要写这样一系列分析Groovy实现原理的博文。我之前在华为大数据部门曾维护过一份规则引擎的项目，该项目说白了就是一种DSL(Domain Specified Language)，把用户的输入转化为一种可以执行的程序。让不懂编程语言的用户只定义一些规则说明便可以完成流程编写。后来由于部门调动，接触不到原来的规则引擎了，但是无意间发现Groovy这种DSL语言的实现机制和当时的规则引擎原理大体相当，所以便借分析Groovy的实现原理，缅怀当时负责的规则引擎吧。同时也希望给其他对规则引擎开发、DSL开发或者编程语言开发感兴趣的朋友一个参考，权当抛砖引玉了。

作为这一系列文章的第一篇，我们先做一些准备工作，为后来的原理分析做下铺垫。

## 安装JDK

要分析Groovy的实现原理，首先需要从源码构建Groovy，这样一边调试，一边看代码效率会高些。源码构建Groovy，需要JDK 9+，下载安装说明参考官网：<https://docs.oracle.com/javase>，我使用的版本是：10.0.2。

```powershell
PS C:\Users\jiang> java -version
java 10.0.2 2018-07-17
Java(TM) SE Runtime Environment 18.3 (build 10.0.2+13)
Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10.0.2+13, mixed mode)
```

## 安装Git工具

Git是当下最流行的版本管理工具，我们需要利用Git下载Groovy的源代码。Git下载安装请参考官网：<http://git-scm.com/>，我使用的版本是：2.27.0。

```powershell
PS C:\Users\jiang> git --version
git version 2.27.0.windows.1
```

## 下载Groovy源码

Groovy的源码托管在Apache的网站上，但是Github上有镜像，我们可以直接在Github镜像下载最新的主干版本，然后切换到最新的稳定版本3.0.5对应的TAG上。

```powershell
PS C:\Users\jiang> cd D:\temp\Groovy\
git clone https://github.com/apache/groovy.git
cd .\groovy\
PS D:\temp\Groovy\groovy> git fetch origin tag GROOVY_3_0_5
PS D:\temp\Groovy\groovy> git checkout GROOVY_3_0_5
```

## 准备Gradle工具

Groovy的编译需要Gradle工具，但是该工具不需要我们自己下载、配置，我们可以直接执行如下命令：

```powershell
PS D:\temp\Groovy\groovy> .\gradlew.bat
```

由于墙的原因，下载需要使用VPN，搭建VPN的方法这里不再叙述。命令执行完毕会在`%USERPROFILE%\.gradle\wrapper\dists`目录下下载对应版本的gradle，其中Groovy 3.0.5版本对应的Gradle版本是Gradle 6.5.1。

## 编译Groovy

执行下面命令，由源码编译Groovy（如果失败可能仍然是墙的原因，使用VPN后重试）：

```powershell
.\gradlew.bat clean dist
```

编译完成后会在`target\distributions`目录下生成目标文件。

## 安装编译后的Groovy

我们将`target\distributions\apache-groovy-binary-3.0.5.zip`文件中的内容解压到某个目录，比如说`C:\`，然后在%PATH%环境变量中添加`C:\groovy-3.0.5\bin`，并设置%GROOVY_HOME%环境变量为`C:\groovy-3.0.5`。然后我们新打开一个powershell验证Groovy是否安装成功：

```powershell
PS C:\Users\jiang> cd D:\temp\Groovy\
PS D:\temp\Groovy> groovy.bat -v
Groovy Version: 3.0.5 JVM: 10.0.2 Vendor: "Oracle Corporation" OS: Windows 10
```

## 将Groovy源码导入IDEA

为了更好的分析Groovy源码，我们需要一个IDE工具，具体是IDEA还是Eclipse或者其它都无所谓，看个人习惯，这里以IDEA为例。首先利用gradle生成IDEA项目：

```powershell
PS D:\temp\Groovy> cd .\groovy\
PS D:\temp\Groovy\groovy> .\gradlew jar idea
```

这时候就可以使用IDEA导入groovy源码项目，进行分析研究了。

## 执行Groovy程序

我们首先利用IDEA新建一个Groovy项目，写一个简单的Groovy程序，该程序会打印"Hello World"：

```groovy
package edu.jiangxin.test

class Test {
    static void main(def args) {
        def mygreeting = "Hello World"
        println mygreeting
    }
}
```

我们知道Groovy是一种依赖于JVM的DSL，其先将*.groovy文件编译成*.class文件，然后调用JVM执行*.class文件，我们可以直接在IDEA中反编译该class文件，得到如下Java代码:

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package edu.jiangxin.test;

import groovy.lang.GroovyObject;
import groovy.lang.MetaClass;
import groovy.transform.Generated;
import groovy.transform.Internal;
import org.codehaus.groovy.runtime.callsite.CallSite;

public class Test implements GroovyObject {
    @Generated
    public Test() {
        CallSite[] var1 = $getCallSiteArray();
        super();
        MetaClass var2 = this.$getStaticMetaClass();
        this.metaClass = var2;
    }

    public static void main(String... args) {
        CallSite[] var1 = $getCallSiteArray();
        Object mygreeting = "Hello World";
        var1[0].callStatic(Test.class, mygreeting);
    }

    @Generated
    @Internal
    public MetaClass getMetaClass() {
        MetaClass var10000 = this.metaClass;
        if (var10000 != null) {
            return var10000;
        } else {
            this.metaClass = this.$getStaticMetaClass();
            return this.metaClass;
        }
    }

    @Generated
    @Internal
    public void setMetaClass(MetaClass var1) {
        this.metaClass = var1;
    }
}
```

是不是看起来有些复杂？没关系我们会一点点搞懂它的。其实这里最关键的是三个函数`$getCallSiteArray()`,`$getStaticMetaClass()`以及`callStatic(Object, Object)`，我们会在之后的文章中逐步揭开他们的面纱。但是在这之前，我们先看下Groovy是如何将之前的*.groovy文件编译成对应的*.class文件的。

（未完待续）