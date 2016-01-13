# JDK

JDK(Java Development Kit)是一个写Java程序所需的开发环境。它由一个处于操作系统层之上的运行环境，还有开发者编译、调试和运行Java应用程序所需的工具组成。JDK是Sun Microsystems为Java程序员提供的产品。目前JDK已经成为使用最广泛的Java SDK（Software development kit）。 JDK包含的基本组件包括：

* javac: 编译器，将源程序转成字节码
* jar: 打包工具，将相关的类文件打包成一个文件
* javadoc: 文档生成器，从源码注释中提取文档
* jdb: debugger，查错工具

JDK中还包括完整的JRE（Java Runtime Environment，Java运行环境），也被称为private runtime。包括了用于产品环境的各种库类，以及给开发员使用的补充库，如国际化的库、IDL库。 JDK中还包括各种例子程序，用以展示Java API中的各部分。

## 配置JDK环境变量(Windows 7)

安装jdk以后，需要配置一下环境变量，在我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量(假定你的jdk安装在c:\jdk1.6）:

    JAVA_HOME=c:\jdk1.6

JAVA_HOME指向的是JDK的安装路径，在这路径下你应该能够找到bin、lib等目录。JDK的安装路径可以选择任意磁盘目录，不过建议你放的目录层次浅一点。

    CLASSPATH=. ;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar

注：.;一定不能少，因为它代表当前路径。

在系统变量里找到Path变量，这是系统自带的，不用新建。你只需修改一下，使他指向JDK的bin目录，这样你在控制台下面编译、执行程序时就不需要再键入一大串路径了。双击Path，在已有的变量后加上：

    ;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin

注：注意前面的分号。

注：要以管理员身份运行cmd才可以更改系统变量。

## OpenJDK和JDK的区别与联系

使用过LINUX的人都应该知道，在大多数LINUX发行版本里，内置或者通过软件源安装JDK的话，都是安装的OpenJDK，那么到底什么是OpenJDK，它与SUN JDK有什么关系和区别呢？

历史上的原因是，OpenJDK是JDK的开放原始码版本，以GPL(General Public License)协议的形式放出。在JDK7的时候，OpenJDK已经作为JDK7的主干开发，SUN JDK7是在OpenJDK7的基础上发布的，其大部分原始码都相同，只有少部分原始码被替换掉。使用JRL(JavaResearch License，Java研究授权协议)发布。至于OpenJDK6则更是有其复杂的一面，首先是OpenJDK6是JDK7的一个分支，并且尽量去除Java SE7的新特性，使其尽量的符合Java6的标准。关于JDK和OpenJDK的区别，可以归纳为以下几点：

授权协议的不同：OpenJDK采用GPL V2协议放出，而SUN JDK则采用JRL放出。两者协议虽然都是开放源代码的，但是在使用上的不同在于GPL V2允许在商业上使用，而JRL只允许个人研究使用。

OpenJDK不包含Deployment（部署）功能：部署的功能包括：Browser Plugin、Java Web Start、以及Java控制面板，这些功能在OpenJDK中是找不到的。

OpenJDK源代码不完整：这个很容易想到，在采用GPL协议的OpenJDK中，SUN JDK的一部分源代码因为产权的问题无法开放给OpenJDK使用，其中最主要的部份就是JMX中的可选元件SNMP部份的代码。因此这些不能开放的源代码 将它作成plug，以供OpenJDK编译时使用，你也可以选择不要使用plug。而Icedtea则为这些不完整的部分开发了相同功能的源代码 (OpenJDK6)，促使OpenJDK更加完整。

部分源代码用开源代码替换：由于产权的问题，很多产权不是SUN的源代码被替换成一些功能相同的开源代码，比如说字体栅格化引擎，使用Free Type代替。

OpenIDK只包含最精简的JDK：OpenJDK不包含其他的软件包，比如Rhino Java DB JAXP……，并且可以分离的软件包也都是尽量的分离，但是这大多数都是自由软件，你可以自己下载加入。

不能使用Java商标：这个很容易理解，在安装OpenJDK的机器上，输入“java -version”显示的是OpenJDK，但是如果是使用Icedtea补丁的OpenJDK，显示的是java。

总之，在Java体系中，还是有很多不自由的成分，源代码的开发不够彻底，希望Oracle能够让JCP更自由开放一些，这也是所有Java社区所希望的。

## 怎样在Linux系统中下载和安装OpenJDK包

Debian, Ubuntu等系统：在命令行中，键入：

    $sudo apt-get install openjdk-7-jre
    $sudo apt-get install openjdk-6-jre

需要注意的是，openjdk-?-jre包只包含Java运行时环境（Java Runtime Environment）。如果是要开发Java应用程序，则需要安装openjdk-?-jdk包。命令如下：

    $sudo apt-get install openjdk-7-jdk
    $sudo apt-get install openjdk-6-jdk

Fedora, OracleLinux, Red Hat Enterprise Linux等系统：在命令行中，键入：

    $ su -c "yum install java-1.7.0-openjdk"
    $ su -c "yum install java-1.6.0-openjdk"

需要注意的是，java-1.?.0-openjdk包只包含Java运行时环境（Java Runtime Environment）。如果是要开发Java应用程序，则需要安装java-1.?.0-openjdk-devel包。命令如下：

    $ su -c "yum install java-1.7.0-openjdk-devel"
    $ su -c "yum install java-1.6.0-openjdk-devel"

# 制作可执行的JAR文件包及jar命令详解

常常在网上看到有人询问：如何把 java 程序编译成 .exe 文件。通常回答只有两种，一种是制作一个可执行的 JAR 文件包，然后就可以双击运行了；而另一种是使用 JET 来进行编译。但是 JET 是要用钱买的，而且据说 JET 也不是能把所有的 Java 程序都编译成执行文件，性能也要打些折扣。所以，使用制作可执行 JAR 文件包的方法就是最佳选择了，何况它还能保持 Java 的跨平台特性。下面就来看看什么是 JAR 文件包吧。  

## JAR 文件包

JAR 文件就是 Java Archive File，顾名思意，它的应用是与 Java 息息相关的，是 Java 的一种文档格式。JAR 文件非常类似 ZIP 文件——准确的说，它就是 ZIP 文件，所以叫它文件包。JAR 文件与 ZIP 文件唯一的区别就是在 JAR 文件的内容中，包含了一个 META-INF/MANIFEST.MF 文件，这个文件是在生成 JAR 文件的时候自动创建的。举个例子，如果我们具有如下目录结构的一些文件：

    ==
	-- test  
		-- Test.class  

把它压缩成 ZIP 文件 test.zip，则这个 ZIP 文件的内部目录结构为：

    test.zip  
	-- test  
        -- Test.class  

如果我们使用 JDK 的 jar 命令把它打成 JAR 文件包 test.jar，则这个 JAR 文件的内部目录结构为：

    test.jar  
    -- META-INF  
        -- MANIFEST.MF  
    -- test
        --Test.class

## 创建可执行的 JAR 文件包

制作一个可执行的 JAR 文件包来发布你的程序是 JAR 文件包最典型的用法。 Java 程序是由若干个 .class 文件组成的。这些 .class 文件必须根据它们所属的包不同而分级分目录存放；运行前需要把所有用到的包的根目录指定给 CLASSPATH 环境变量或者 java 命令的 -cp 参数；运行时还要到控制台下去使用 java 命令来运行，如果需要直接双击运行必须写 Windows 的批处理文件 (.bat) 或者 Linux 的 Shell 程序。因此，许多人说，Java 是一种方便开发者苦了用户的程序设计语言。其实不然，如果开发者能够制作一个可执行的 JAR 文件包交给用户，那么用户使用起来就方便了。在 Windows 下安装 JRE (Java Runtime Environment) 的时候，安装文件会将 .jar 文件映射给 javaw.exe 打开。那么，对于一个可执行的 JAR 文件包，用户只需要双击它就可以运行程序了。那么现在的关键就是如何来创建这个可执行的 JAR 文件包。 创建可执行的 JAR 文件包，需要使用带 cvfm 参数的 jar 命令，同样以上述 test 目录为例，命令如下：

    jar cvfm test.jar manifest.mf test

这里 test.jar 和 manifest.mf 两个文件，分别是对应的参数 f 和 m，其重头戏在 manifest.mf。因为要创建可执行的 JAR 文件包，光靠指定一个 manifest.mf 文件是不够的，因为 MANIFEST 是 JAR 文件包的特征，可执行的 JAR 文件包和不可执行的 JAR 文件包都包含 MANIFEST。关键在于可执行 JAR 文件包的 MANIFEST，其内容包含了 Main-Class 一项。这在 MANIFEST 中书写格式如下：

    Main-Class: 可执行主类全名(包含包名) 

例如，假设上例中的 Test.class 是属于 test 包的，而且是可执行的类 (定义了 public static void main(String[]) 方法)，那么这个 manifest.mf 可以编辑如下： 

    Main-Class: test.Test <回车>; 

这个 manifest.mf 可以放在任何位置，也可以是其它的文件名，只需要有 Main-Class: test.Test 一行，且该行以一个回车符结束即可。创建了 manifest.mf 文件之后，我们的目录结构变为：  

    ==
    -- test  
        -- Test.class  
    -- manifest.mf 

这时候，需要到 test 目录的上级目录中去使用 jar 命令来创建 JAR 文件包。也就是在目录树中使用“==”表示的那个目录中，使用如下命令： 

    jar cvfm test.jar manifest.mf test

之后在“==”目录中创建了 test.jar，这个 test.jar 就是执行的 JAR 文件包。运行时只需要使用 java -jar test.jar 命令即可。需要注意的是，创建的 JAR 文件包中需要包含完整的、与 Java 程序的包结构对应的目录结构，就像上例一样。而 Main-Class 指定的类，也必须是完整的、包含包路径的类名，如上例的 test.Test；而且在没有打成 JAR 文件包之前可以使用 java <类名>; 来运行这个类，即在上例中 java test.Test 是可以正确运行的 (当然要在 CLASSPATH 正确的情况下)。

## jar 命令详解

jar 是随 JDK 安装的，在 JDK 安装目录下的 bin 目录中，Windows 下文件名为 jar.exe，Linux 下文件名为 jar。它的运行需要用到 JDK 安装目录下 lib 目录中的 tools.jar 文件。不过我们除了安装 JDK 什么也不需要做，因为 SUN 已经帮我们做好了。我们甚至不需要将 tools.jar 放到 CLASSPATH 中。

使用不带任何参数的 jar 命令我们可以看到 jar 命令的用法如下：

jar {ctxu}[vfm0M] [jar-文件] [manifest-文件] [-C 目录] 文件名 ... 

其中 {ctxu} 是 jar 命令的子命令，每次 jar 命令只能包含 ctxu 中的一个，它们分别表示：

    -c　创建新的 JAR 文件包
    -t　列出 JAR 文件包的内容列表
    -x　展开 JAR 文件包的指定文件或者所有文件
    -u　更新已存在的 JAR 文件包 (添加文件到 JAR 文件包中) 

[vfm0M] 中的选项可以任选，也可以不选，它们是 jar 命令的选项参数

    -v　生成详细报告并打印到标准输出
    -f　指定 JAR 文件名，通常这个参数是必须的
    -m　指定需要包含的 MANIFEST 清单文件
    -0　只存储，不压缩，这样产生的 JAR 文件包会比不用该参数产生的体积大，但速度更快
    -M　不产生所有项的清单（MANIFEST〕文件，此参数会忽略 -m 参数

[jar-文件] 即需要生成、查看、更新或者解开的 JAR 文件包，它是 -f 参数的附属参数  

[manifest-文件] 即 MANIFEST 清单文件，它是 -m 参数的附属参数

[-C 目录] 表示转到指定目录下去执行这个 jar 命令的操作。它相当于先使用 cd 命令转该目录下再执行不带 -C 参数的 jar 命令，它只能在创建和更新 JAR 文件包的时候可用。　　  

文件名 ... 指定一个文件/目录列表，这些文件/目录就是要添加到 JAR 文件包中的文件/目录。如果指定了目录，那么 jar 命令打包的时候会自动把该目录中的所有文件和子目录打入包中。

## jar命令实例

1)jar cf test.jar test

该命令没有执行过程的显示，执行结果是在当前目录生成了 test.jar 文件。如果当前目录已经存在 test.jar，那么该文件将被覆盖。

2)jar cvf test.jar test

该命令与上例中的结果相同，但是由于 v 参数的作用，显示出了打包过程

3)jar cvfM test.jar test

该命令与 2) 结果类似，但在生成的 test.jar 中没有包含 META-INF/MANIFEST 文件，打包过程的信息也略有差别：

增加：test/(读入= 0) (写出= 0)(存储了 0%)  

增加：test/Test.class(读入= 7) (写出= 6)(压缩了 14%)  

4) jar cvfm test.jar manifest.mf test  

运行结果与 2) 相似，显示信息也相同，只是生成 JAR 包中的 META-INF/MANIFEST 内容不同，是包含了 manifest.mf 的内容  

5) jar tf test.jar  

在 test.jar 已经存在的情况下，可以查看 test.jar 中的内容，如对于 2) 和 3) 生成的 test.jar 分别应该此命令，结果如下；  

对于 2)  

META-INF/  

META-INF/MANIFEST.MF  

test/  

test/Test.class  

对于 3)  

test/  

test/Test.class  

6) jar tvf test.jar  

除显示 5) 中显示的内容外，还包括包内文件的详细信息，如：  

0 Wed Jun 19 15:39:06 GMT 2002 META-INF/  

86 Wed Jun 19 15:39:06 GMT 2002 META-INF/MANIFEST.MF  

0 Wed Jun 19 15:33:04 GMT 2002 test/  

7 Wed Jun 19 15:33:04 GMT 2002 test/Test.class  

7) jar xf test.jar  

解开 test.jar 到当前目录，不显示任何信息，对于 2) 生成的 test.jar，解开后的目录结构如下：  

　　==  

　　|-- META-INF  

　　|　 -- MANIFEST  

　　-- test  

　　　　--Test.class  

8) jar xvf test.jar  

运行结果与 7) 相同，对于解压过程有详细信息显示，如：  

创建：META-INF/  

展开：META-INF/MANIFEST.MF  

创建：test/  

展开：test/Test.class  

9) jar uf test.jar manifest.mf  

在 test.jar 中添加了文件 manifest.mf，此使用 jar tf 来查看 test.jar 可以发现 test.jar 中比原来多了一个 manifest。这里顺便提一下，如果使用 -m 参数并指定 manifest.mf 文件，那么 manifest.mf 是作为清单文件 MANIFEST 来使用的，它的内容会被添加到 MANIFEST 中；但是，如果作为一般文件添加到 JAR 文件包中，它跟一般文件无异。  

10) jar uvf test.jar manifest.mf  

与 9) 结果相同，同时有详细信息显示，如：  

增加：manifest.mf(读入= 17) (写出= 19)(压缩了 -11%)  

关于 JAR 文件包的一些技巧

使用 unzip 来解压 JAR 文件：在介绍 JAR 文件的时候就已经说过了，JAR 文件实际上就是 ZIP 文件，所以可以使用常见的一些解压 ZIP 文件的工具来解压 JAR 文件，如 Windows 下的 WinZip、WinRAR 等和 Linux 下的 unzip 等。使用 WinZip 和 WinRAR 等来解压是因为它们解压比较直观，方便。而使用 unzip，则是因为它解压时可以使用 -d 参数指定目标目录。在解压一个 JAR 文件的时候是不能使用 jar 的 -C 参数来指定解压的目标的，因为 -C 参数只在创建或者更新包的时候可用。那么需要将文件解压到某个指定目录下的时候就需要先将这具 JAR 文件拷贝到目标目录下，再进行解压，比较麻烦。如果使用 unzip，就不需要这么麻烦了，只需要指定一个 -d 参数即可。如：

unzip test.jar -d dest/  

使用 WinZip 或者 WinRAR 等工具创建 JAR 文件：上面提到 JAR 文件就是包含了 META-INF/MANIFEST 的 ZIP 文件，所以，只需要使用 WinZip、WinRAR 等工具创建所需要 ZIP 压缩包，再往这个 ZIP 压缩包中添加一个包含 MANIFEST 文件的 META-INF 目录即可。对于使用 jar 命令的 -m 参数指定清单文件的情况，只需要将这个 MANIFEST 按需要修改即可。

使用 jar 命令创建 ZIP 文件：有些 Linux 下提供了 unzip 命令，但没有 zip 命令，所以需要可以对 ZIP 文件进行解压，即不能创建 ZIP 文件。如要创建一个 ZIP 文件，使用带 -M 参数的 jar 命令即可，因为 -M 参数表示制作 JAR 包的时候不添加 MANIFEST 清单，那么只需要在指定目标 JAR 文件的地方将 .jar 扩展名改为 .zip 扩展名，创建的就是一个不折不扣的 ZIP 文件了，如将上一节的第 3) 个例子略作改动：

jar cvfM test.zip test

# javadoc注意点（原创）

javadoc生成文档时总是报java.lang.IllegalArgumentException错  

JavamavenEXTSUNJDK .

javadoc生成文档时总是报java.lang.IllegalArgumentException错误,是classpath里面字符冲突引起的。我在classpath中包含了%JAVA_HOME%\lib;解决方法是重新设置classpath或者删除classpath.要注意设置完成后重启下cmd或者editplus，重启后生效！ 

见官方参考文档 http://maven.apache.org/plugins/maven-javadoc-plugin/faq.html



javadoc生成时出错：编码GBK的不可映射字符

由于java源代码是用的UTF-8编码，Eclipse中默认编码是GB18030，因此，在生成javadoc的时候，需要手工指定一下编码和字符集。

解决方案是： 主菜单–>Project–>Generate javadoc–>next>next–> 在 “Extra javadoc options”下面的文本框中填入：

-encoding UTF-8 -charset UTF-8

# java程序必须有一个public类吗

public类只是说明这个类可以被它所在的包外面的类所访问到，如果不加，只能在包内被访问，但在某些情况下也是可以的，例如以下例子就是正确的：

```java
    class Example
    { 
        public static void main(String args[])
        { 
            System.out.println("This is a simple Java program."); 
        }
    }
```

# 向包中添加类

要把类放入一个包中，必须把此包的名字放在源文件头部，并且放在对包中的类进行定义的代码之前。例如在文件Employee.java的开始部分如下：

package com.horstmann.corejava;

public class Employee

{

	...

}

把包中的文件放入与此完整的包名相匹配的的子目录中。例如，在包com.horstmann.corejava中的所有类文件都必须放在子目录com/horstmann/core.java下，这是最简单的一种方法。类被存储在文件系统的子目录中。类的路径必须与所在包名相匹配。在前面的例子中，包目录com/horstmann/corejava是程序目录的一个子目录。然而这样的安排很不灵活。一般有多个程序需要访问包文件。为了使包可以在多个程序间共享，需要做以下事情：

1.把类放在一个或多个特定的目录中，比如/home/user/classdir。此目录是包树的基本目录。如果加入了类com.horstmann.corejava.Employee,那么此类文件必须位于子目录/home/user/classdir/com/horstmann/corejava下。

2.设置类路径。类路径是其子目录包含类文件的所有基本目录的集合。

# Java中char到底是多少字节？

貌似一个简单的问题（也许还真是简单的）但是却把曾经自认为弄清楚的我弄得莫名其妙 。char在Java中应该是16个字节 ，byte在Java中应该是8个字节 ，char x = '编'; //这样是合法的，输出也是16个字节 ，但是 

String str = "编"; 

byte[] bytes = str.getBytes(); //我想不明白，为什么这里要占用3个byte呢? 

3个byte一共是3*8=24个字节，那么char x怎么又放得下？我坚信char是16个字节， 但是str.getBytes()这个东西到底又怎么回事？ 

首先，要搞清楚 code point 和 encoding 的区别。Java 是遵循 unicode 4.0 标准的，而内部的 character 以 utf-16 作为 encoding。unicode 4.0 标准包含从 U+0000-U+FFFF 的基本多语言平面和 U+10000-U+10FFFF 的扩展平面的文字，这是 code point。Java 的 char 类型是 16 bit 的，所以单个 char 只支持基本平面内的文字，而扩展平面的文字是由一对 char 来表示的。 而 String.getBytes() 这个方法是按照指定的 encoding 返回字符串，一般中文系统的默认编码是 utf-8 (linux, mac) 或者 gbk/gb18030 (windows)。只要是基本平面内的文字，utf-8码的中文都是3字节的，而 gbk/gbk18030 是2字节的。

# 常用Java API

## 计算Java程序运行时间

第一种是以毫秒为单位计算的。

　　//伪代码

　　long startTime=System.currentTimeMillis();   //获取开始时间

　　doSomeThing();  //测试的代码段

　　long endTime=System.currentTimeMillis(); //获取结束时间

　　System.out.println("程序运行时间： "+(end-start)+"ms");

第二种是以纳秒为单位计算的。

//伪代码

　　long startTime=System.nanoTime();   //获取开始时间

　　doSomeThing();  //测试的代码段

　　long endTime=System.nanoTime(); //获取结束时间

System.out.println("程序运行时间： "+(end-start)+"ns");

## 获得系统换行符

System.getProperty("line.separator");

## Java获取当前路径

利用System.getProperty()函数获取当前路径：

System.out.println(System.getProperty("user.dir"));//user.dir指定了当前的路径

使用File提供的函数获取当前路径：

File directory = new File("");//设定为当前文件夹

try{

    System.out.println(directory.getCanonicalPath());//获取标准的路径

    System.out.println(directory.getAbsolutePath());//获取绝对路径

}catch(Exceptin e){}

File.getCanonicalPath()和File.getAbsolutePath()大约只是对于new File(".")和new File("..")两种路径有所区别。

对于getCanonicalPath()，“."就表示当前的文件夹，而”..“则表示当前文件夹的上一级文件夹

对于getAbsolutePath()，则不管”.”、“..”，返回当前的路径加上你在new File()时设定的路径

至于getPath()，得到的只是你在new File()时设定的路径

比如当前的路径为 C:\test ：

File directory = new File("abc");

directory.getCanonicalPath(); //得到的是C:\test\abc

directory.getAbsolutePath();    //得到的是C:\test\abc

direcotry.getPath();                    //得到的是abc



File directory = new File(".");

directory.getCanonicalPath(); //得到的是C:\test

directory.getAbsolutePath();    //得到的是C:\test\.

direcotry.getPath();                    //得到的是.



File directory = new File("..");

directory.getCanonicalPath(); //得到的是C:\

directory.getAbsolutePath();    //得到的是C:\test\..

direcotry.getPath();                    //得到的是..



## System.getenv()

getenv是获取系统的环境变更，对于windows对在系统属性-->高级-->环境变量中设置的变量将显示在此(对于linux,通过export设置的变量将显示在此) 

System.out.println(System.getenv()); 

## java中的URL类

创建URL对象：

URL gamelan = new URL("http://www.gamelan.com/");

以上是绝对URL对象，也可以创建相对的URL 对象。 

创建相对的URL对象：

相对URL一般用在html文件之中。

在java 程序中，你可以创建如下的相对URL，但是他是基于绝对URL的。

比如：主URL是：http://www.gamelan.com/pages/

其下还有URL ：

        http://www.gamelan.com/pages/Gamelan.game.html

        http://www.gamelan.com/pages/Gamelan.net.html

你就可以创建如下的URL对象：

        URL gamelan = new URL("http://www.gamelan.com/pages/");

        URL gamelanGames = new URL(gamelan, "Gamelan.game.html");

        URL gamelanNetwork = new URL(gamelan, "Gamelan.net.html");

因为，URL类有如下的构造函数：

public URL(String  str);

public URL(URLcontext,    Stringstr)

另外：使用这种相对URL还可以创建到网页内部某个标记的URL对象：

URL gamelanNetworkBottom = new URL(gamelanNetwork, "#BOTTOM");

其他的几种URL构造函数：

new URL("http", "www.gamelan.com", "/pages/Gamelan.net.html");

new URL("http://www.gamelan.com/pages/Gamelan.net.html");

URL gamelan = new URL("http", "www.gamelan.com", 80,

                       "pages/Gamelan.network.html");

（指向：http://www.gamelan.com:80/pages/Gamelan.network.html）

URL 中的含有特殊字符的情况：

有些URL含有特殊字符，比如空格： 

http://foo.com/hello world/

这时的URL就必须进行编码：将空格用%20替代：

URL url = new URL("http://foo.com/hello%20world");

以上URL中只有一个特殊字符，因此手动编码相对简单。

当URL中的特殊字符很多时，或者特殊字符数目不确定时，就不能使用手动编码了，这时需要使用java.net.URI类去自动完成编码： 

URI uri = new URI("http", "foo.com", "/hello world/", "");

然后，将URI转换成URL： 

URL url = uri.toURL();

异常：MalformedURLException

URL构造函数可能会抛出异常，使用如下方法捕获异常: 

try {

    URL myURL = new URL(. . .)

} catch (MalformedURLException e) {

    . . .

    // exception handler code here

    . . .

}

# Java关键字及其作用

## 1. 访问控制

private 私有的

private 关键字是访问控制修饰符，可以应用于类、方法或字段（在类中声明的变量）。 只能在声明private（内部）类、方法或字段的类中引用这些类、方法或字段。在类的外部或者对于子类而言，它们是不可见的。 所有类成员的默认访问范围都是package 访问，也就是说，除非存在特定的访问控制修饰符，否则，可以从同一个包中的任何类访问类成员。

protected 受保护的

protected 关键字是可以应用于类、方法或字段（在类中声明的变量）的访问控制修饰符。可以在声明protected 类、方法或字段的类、同一个包中的其他任何类以及任何子类（无论子类是在哪个包中声明的）中引用这些类、方法或字段。所有类成员的默认访问范围都是 package 访问，也就是说，除非存在特定的访问控制修饰符，否则，可以从同一个包中的任何类访问类成员。

public 公共的

public 关键字是可以应用于类、方法或字段（在类中声明的变量）的访问控制修饰符。 可能只会在其他任何类或包中引用public 类、方法或字段。所有类成员的默认访问范围都是package 访问，也就是说，除非存在特定的访问控制修饰符，否则，可以从同一个包中的任何类访问类成员。

## 2. 类、方法和变量修饰符

1)abstract 声 明抽象

abstract关键字可以修改类或方法。abstract类可以扩展（增加子类），但不能直 接实例化。abstract方法不在声明它的类中实现，但必须在某个子类中重写。采用abstract方法的类本来就是抽象类，并且必须声明为 abstract。

2)class类

class 关键字用来声明新的Java 类，该类是相关变量和/或方法的集合。类是面向对象的程序设计方法的基本构造单位。类通常代表某种实际实体，如几何形状或人。类是对象的模板。每个对象都 是类的一个实例。要使用类，通常使用new 操作符将类的对象实例化，然后调用类的方法来访问类的功能。

3)extends 继承、扩展

extends 关键字用在class 或interface 声明中，用于指示所声明的类或接口是其名称后跟有extends 关键字的类或接口的子类。子类继承父类的所有public 和protected 变量和方法。 子类可以重写父类的任何非final 方法。一个类只能扩展一个其他类。

4)final 最 终、不可改变

final 关键字可以应用于类，以指示不能扩展该类（不能有子类）。final 关键字可以应用于方法，以指示在子类中不能重写此方法。一个类不能同时是abstract 又是final。abstract 意味着必须扩展类，final 意味着不能扩展类。一个方法不能同时是abstract 又是final。abstract 意味着必须重写方法，final 意味着不能重写方法。

5)implements实 现

implements 关键字在class 声明中使用，以指示所声明的类提供了在implements 关键字后面的名称所指定的接口中所声明的所有方法的实现。类必须提供在接口中所声明的所有方法的实现。一个类可以实现多个接口。

6)interface 接口

interface 关键字用来声明新的Java 接口，接口是方法的集合。

接口是Java 语言的一项强大功能。任何类都可声明它实现一个或多个接口，这意味着它实现了在这些接口中所定义的所有方法。

实现了接口的任何类都必须提 供在该接口中的所有方法的实现。一个类可以实现多个接口。

7)native 本地

native 关键字可以应用于方法，以指示该方法是用Java 以外的语言实现的。

8)new 新,创 建

new 关键字用于创建类的新实例。

new 关键字后面的参数必须是类名，并且类名的后面必须是一组构造方法参数（必须带括号）。

参数集合必须与类的构造方法的签名匹配。

= 左侧的变量的类型必须与要实例化的类或接口具有赋值兼容关系。

9)static 静态

static 关键字可以应用于内部类（在另一个类中定义的类）、方法或字段（类的成员变量）。

通常，static 关键字意味着应用它的实体在声明该实体的类的任何特定实例外部可用。

static（内部）类可以被其他类实例化和引用（即使它是顶级 类）。在上面的示例中，另一个类中的代码可以实例化MyStaticClass 类，方法是用包含它的类名来限定其名称，如MyClass.MyStaticClass。

static 字段（类的成员变量）在类的所有实例中只存在一次。

可以从 类的外部调用static 方法，而不用首先实例化该类。这样的引用始终包括类名作为方法调用的限定符。

模式：public final static <type> varName = <value>; 通常用于声明可以在类的外部使用的类常量。在引用这样的类常量时需要用类名加以限定。在上面的示例中，另一个类可以用 MyClass.MAX_OBJECTS 形式来引用MAX_OBJECTS 常量。

10)strictfp 严格,精准

strictfp的意思是FP-strict，也就是说精确浮点的意思。在Java虚拟机进行浮点运算时，如果没有指定 strictfp关键字 时，Java的编译器以及运行环境在对浮点运算的表达式是采取一种近似于我行我素的行为来完成这些操作，以致于得到的结果往往无法令人满意。而一旦使用了 strictfp来声明一个类、接口或者方法时，那么所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。因此如果想 让浮点运算更加精确，而且不会因为不同的硬件平台所执行的结果不一致的话，那就请用关键字strictfp。

可以将一个 类、接口以及方法声明为strictfp，但是不允许对接口中的方法以及构造函数声明strictfp关键字

11)synchronized线程、同步

synchronized 关键字可以应用于方法或语句块，并为一次只应由一个线程执行的关键代码段提供保护。

synchronized 关键字可防止代码的关键代码段一次被多个线程执行。

如果应用于静态方法，那么，当该方法一次由一个线程执行时，整个类将被锁定。

如 果应用于实例方法，那么，当该方法一次由一个线程访问时，该实例将被锁定。

如果应用于对象或数组，当关联的代码块一次由一个线程执行时， 对象或数组将被锁定。

12)transient 短 暂

transient 关键字可以应用于类的成员变量，以便指出该成员变量不应在包含它的类实例已序列化时被序列化。

当一个对象被串行化的时 候，transient型变量的值不包括在串行化的表示中，然而非transient型的变量是被包括进去的。

13)volatile 易失

volatile 关键字用于表示可以被多个线程异步修改的成员变量。

注意：volatile 关键字在许多Java 虚拟机中都没有实现。volatile 的目标用途是为了确保所有线程所看到的指定变量的值都是相同的。

## 3. 程序控制语句

1)break 跳 出，中断

break 关键字用于提前退出for、while 或do 循环，或者在switch 语句中用来结束case 块。

break 总是退出最深层的while、for、do 或switch 语句。

2)continue 继续

continue 关键字用来跳转到for、while 或do 循环的下一个迭代。

continue 总是跳到最深层while、for 或do 语句的下一个迭代。

3)return 返 回

return 关键字会导致方法返回到调用它的方法，从而传递与返回方法的返回类型匹配的值。

如 果方法具有非void 的返回类型，return 语句必须具有相同或兼容类型的参数。

返回值两侧的括号是可选的。

4)do 运行

do 关键字用于指定一个在每次迭代结束时检查其条件的循环。

do 循环体至少执行一次。

条件表达式后面必须有分号。

5)while 循环

while 关键字用于指定一个只要条件为真就会重复的循环。

6)if 如 果

if 关键字指示有条件地执行代码块。条件的计算结果必须是布尔值。

if 语句可以有可选的else 子句，该子句包含条件为false 时将执行的代码。

包含boolean 操作数的表达式只能包含boolean 操作数。

7)else 否 则

else 关键字总是在if-else 语句中与if 关键字结合使用。else 子句是可选的，如果if 条件为false，则执行该子句。

8)for 循环

for 关键字用于指定一个在每次迭代结束前检查其条件的循环。

for 语句的形式为for(initialize; condition; increment)

控件流进入for 语句时，将执行一次initialize 语句。

每次执行循环体之前将计 算condition 的结果。如果condition 为true，则执行循环体。

每次执行循环体之后，在计算下一个迭代的 condition 之前，将执行increment 语句。

9)instanceof 实例

instanceof 关键字用来确定对象所属的类。

10)switch 观察

switch 语句用于基于某个表达式选择执行多个代码块中的某一个。

switch 条件的计算结果必须等于byte、char、short 或int。

case 块没有隐式结束点。break 语句通常在每个case 块末尾使用，用于退出switch 语句。

如 果没有break 语句，执行流将进入所有后面的case 和/或default 块。

11)case 返回观察里的结果

case 用来标记switch 语句中的每个分支。

case 块没有隐式结束点。break 语句通常在每个case 块末尾使用，用于退出switch 语句。

如果没有 break 语句，执行流将进入所有后面的case 和/或default 块。

12)default 默认

default 关键字用来标记switch 语句中的默认分支。

default 块没有隐式结束点。break 语句通常在每个case 或default 块的末尾使用，以便在完成块时退出switch 语句。

如果没有default 语句，其参数与任何case 块都不匹配的switch 语句将不执行任何操作。

## 4. 错误处理

1)try 捕获异常

try 关键字用于包含可能引发异常的语句块。

每 个try 块都必须至少有一个catch 或finally 子句。

如果某个特定异常类未被任何catch 子句处理，该异常将沿着调用栈递归地传播到下一个封闭try 块。如果任何封闭try 块都未捕获到异常，Java 解释器将退出，并显示错误消息和堆栈跟踪信息。

2)catch 处 理异常

catch 关键字用来在try-catch 或try-catch-finally 语句中定义异常处理块。

开始和结束标记{ 和} 是catch 子句语法的一部分，即使该子句只包含一个语句，也不能省略这两个标记。

每个try 块都必须至少有一个catch 或finally 子句。

如果某个特定异常类未被任何catch 子句处理，该异常将沿着调用栈递归地传播到下一个封闭try 块。如果任何封闭try 块都未捕获到异常，Java 解释器将退出，并显示错误消息和堆栈跟踪信息。

3)throw 抛出一个异常对象

throw 关键字用于引发异常。

throw 语句将java.lang.Throwable 作为参数。Throwable 在调用栈中向上传播，直到被适当的catch 块捕获。

引发非RuntimeException 异常的任何方法还必须在方法声明中使用throws 修饰符来声明它引发的异常。

4)throws 声明一个异常可能被抛出

throws 关键字可以应用于方法，以便指出方法引发了特定类型的异常。

throws 关键字将逗号分隔的java.lang.Throwables 列表作为参数。

引发非 RuntimeException 异常的任何方法还必须在方法声明中使用throws 修饰符来声明它引发的异常。

要在try-catch 块中包含带throws 子句的方法的调用，必须提供该方法的调用者。

## 5. 包相关

1)import 引入

import 关键字使一个包中的一个或所有类在当前Java 源文件中可见。可以不使用完全限定的类名来引用导入的类。

当多个包包含同名的类时，许 多Java 程序员只使用特定的import 语句（没有“*”）来避免不确定性。

2)package 包

package 关键字指定在Java 源文件中声明的类所驻留的Java 包。

package 语句（如果出现）必须是Java 源文件中的第一个非注释性文本。

例:java.lang.Object。

如果Java 源文件不包含package 语句，在该文件中定义的类将位于“默认包”中。请注意，不能从非默认包中的类引用默认包中的类。

## 6. 基本类型

1)boolean 布 尔型

boolean 是Java 原始类型。boolean 变量的值可以是true 或false。

boolean 变量只能以true 或false 作为值。boolean 不能与数字类型相互转换。

包 含boolean 操作数的表达式只能包含boolean 操作数。

Boolean 类是boolean 原始类型的包装对象类。

2)byte 字节型

byte 是Java 原始类型。byte 可存储在[-128, 127] 范围以内的整数值。

Byte 类是byte 原始类型的包装对象类。它定义代表此类型的值的范围的MIN_VALUE 和MAX_VALUE 常量。

Java 中的所有整数值都是32 位的int 值，除非值后面有l 或L（如235L），这表示该值应解释为long。

3)char 字符型

char 是Java 原始类型。char 变量可以存储一个Unicode 字符。

可以使用下列char 常量：\b - 空格, \f - 换页, \n - 换行, \r - 回车, \t - 水平制表符, \' - 单引号, \" - 双引号, \\ - 反斜杠, \xxx - 采用xxx 编码的Latin-1 字符。\x 和\xx 均为合法形式，但可能引起混淆。\uxxxx - 采用十六进制编码xxxx 的Unicode 字符。

Character 类包含一些可用来处理char 变量的static 方法，这些方法包括isDigit()、isLetter()、isWhitespace() 和toUpperCase()。

char 值没有符号。

4)double 双精度

double 是Java 原始类型。double 变量可以存储双精度浮点值。

由于浮点数据类型是实际数值的近似值，因此，一般不要对浮点数值进行是否相等的比 较。

Java 浮点数值可代表无穷大和NaN（非数值）。Double 包装对象类用来定义常量MIN_VALUE、MAX_VALUE、NEGATIVE_INFINITY、POSITIVE_INFINITY 和NaN。

5)float 浮点

float 是Java 原始类型。float 变量可以存储单精度浮点值。

使用此关键字时应遵循下列规则：

Java 中的浮点文字始终默认为双精度。要指定单精度文字值，应在数值后加上f 或F，如0.01f。

由于浮点数据类型是实际数值的近似 值，因此，一般不要对浮点数值进行是否相等的比较。

Java 浮点数值可代表无穷大和NaN（非数值）。Float 包装对象类用来定义常量MIN_VALUE、MAX_VALUE、NEGATIVE_INFINITY、POSITIVE_INFINITY 和NaN。

6)int 整型

int 是Java 原始类型。int 变量可以存储32 位的整数值。

Integer 类是int 原始类型的包装对象类。它定义代表此类型的值的范围的MIN_VALUE 和MAX_VALUE 常量。

Java 中的所有整数值都是32 位的int 值，除非值后面有l 或L（如235L），这表示该值应解释为long。

7)long 长整型

long 是Java 原始类型。long 变量可以存储64 位的带符号整数。

Long 类是long 原始类型的包装对象类。它定义代表此类型的值的范围的MIN_VALUE 和MAX_VALUE 常量。

Java 中的所有整数值都是32 位的int 值，除非值后面有l 或L（如235L），这表示该值应解释为long。

8)short 短整型

short 是Java 原始类型。short 变量可以存储16 位带符号的整数。

Short 类是short 原始类型的包装对象类。它定义代表此类型的值的范围的MIN_VALUE 和MAX_VALUE 常量。

Java 中的所有整数值都是32 位的int 值，除非值后面有l 或L（如235L），这表示该值应解释为long。

9)null 空

null 是Java 的保留字，表示无值。

将null 赋给非原始变量相当于释放该变量先前所引用的对象。

不能将null 赋给原始类型（byte、short、int、long、char、float、double、boolean）变量。

10)true 真

true 关键字表示boolean 变量的两个合法值中的一个。

11)false 假

false 关键字代表boolean 变量的两个合法值之一。

## 7. 变量引用

1)super 父类,超 类

super 关键字用于引用使用该关键字的类的超类。

作为独立语句出现的super 表示调用超类的构造方法。

super.<methodName>() 表示调用超类的方法。只有在如下情况中才需要采用这种用法：要调用在该类中被重写的方法，以便指定应当调用在超类中的该方法。

2)this 本类

this 关键字用于引用当前实例。

当引用可能不明确时，可以使用this 关键字来引用当前的实例。

3)void 无返回值

void 关键字表示null 类型。

void 可以用作方法的返回类型，以指示该方法不返回值。

## 8. 保留字

1) goto 跳转

goto 保留关键字，但无任何作用。结构化程序设计完全不需要goto 语句即可完成各种流程，而goto 语句的使用往往会使程序的可读性降低，所以Java 不允许goto 跳转。

2) const 静 态

const 保留字，是一个类型修饰符，使用const声明的对象不能更新。与final某些类似。

# Eclipse相关问题

## Eclipse常用快捷键

### 编辑快捷键

Eclipse的编辑功能非常强大，掌握了Eclipse快捷键功能，能够大大提高开发效率。Eclipse中有如下一些和编辑相关的快捷键。

1. 【ALT+/】

此快捷键为用户编辑的好帮手，能为用户提供内容的辅助，不要为记不全方法和属性名称犯愁，当记不全类、方法和属性的名字时，多体验一下【ALT+/】快捷键带来的好处吧。

2. 【Ctrl+O】

显示类中方法和属性的大纲，能快速定位类的方法和属性，在查找Bug时非常有用。

3. 【Ctrl+/】

快速添加注释，能为光标所在行或所选定行快速添加注释或取消注释，在调试的时候可能总会需要注释一些东西或取消注释，现在好了，不需要每行进行重复的注释。

4. 【Ctrl+D】

删除当前行，这也是笔者的最爱之一，不用为删除一行而按那么多次的删除键。

5. 【Ctrl+M】

窗口最大化和还原，用户在窗口中进行操作时，总会觉得当前窗口小（尤其在编写代码时），现在好了，试试【Ctrl+M】快捷键。

syso +【ALT+/】 = System.out.println();

main +【ALT+/】= main函数

选中要移动的代码后，按Tab键右移，按Shift+Tab键左移

### 查看和定位快捷键：

在程序中，迅速定位代码的位置，快速找到Bug的所在，是非常不容易的事，Eclipse提供了强大的查找功能，可以利用如下的快捷键帮助完成查找定位的工作。

1. 【Ctrl+K】、【Ctrl++Shift+K】

快速向下和向上查找选定的内容，从此不再需要用鼠标单击查找对话框了。

2. 【Ctrl+Shift+T】Open Type

查找工作空间（Workspace）构建路径中的可找到类定义（包括第三方jar包中的类），可以使用“*”、“？”等通配符。

【Ctrl+ T】/F4查看抽象类、接口、方法的具体实现类、方法

3. 【Ctrl+Shift+R】Open Resource

查找工作空间（Workspace）中的所有文件（包括Java文件），也可以使用通配符。

4. 【Ctrl+Shift+G】

查找类、方法和属性的引用。这是一个非常实用的快捷键，例如要修改引用某个方法的代码，可以通过【Ctrl+Shift+G】快捷键迅速定位所有引用此方法的位置。此快捷键也可以通过右键->Reference->Workspace实现

5. 【Ctrl+Shift+O】

快速生成import，当从网上拷贝一段程序后，不知道如何import进所调用的类，试试【Ctrl+Shift+O】快捷键，一定会有惊喜。另外也会删除不需要的包。

6. 【Ctrl+Shift+F】

格式化代码，书写格式规范的代码是每一个程序员的必修之课，当看见某段代码极不顺眼时，选定后按【Ctrl+Shift+F】快捷键可以格式化这段代码，如果不选定代码则默认格式化当前文件（Java文件）。

7. 【ALT+Shift+W】

查找当前文件所在项目中的路径，可以快速定位浏览器视图的位置，如果想查找某个文件所在的包时，此快捷键非常有用（特别在比较大的项目中）。

8. 【Ctrl+L】

定位到当前编辑器的某一行，对非Java文件也有效。

9. 【Alt+←】、【Alt+→】

后退历史记录和前进历史记录，在跟踪代码时非常有用，用户可能查找了几个有关联的地方，但可能记不清楚了，可以通过这两个快捷键定位查找的顺序。

10. 【F3】

快速定位光标位置的某个类、方法和属性。

11. 【F4】

显示类的继承关系，并打开类继承视图。

12. 【ALT+Shift+M】

选中要导入包的类，按此快捷键即可导入需要的包路径。



按住Ctrl，单击方法，属性名等可以进入到方法的实现或者属性的声明中。

按住Ctrl+T，单击接口方法，可以直接进入到方法的实现，而不是进入到方法的声明中。

### 调试快捷键：

Eclipse中有如下一些和运行调试相关的快捷键。

1. 【Ctrl+Shift+B】：在当前行设置断点或取消设置的断点。

2. 【F11】：调试最后一次执行的程序。

3. 【Ctrl+F11】：运行最后一次执行的程序。

4. 【F5】：跟踪到方法中，当程序执行到某方法时，可以按【F5】键跟踪到方法中。

5. 【F6】：单步执行程序。

6. 【F7】：执行完方法，返回到调用此方法的后一条语句。

7. 【F8】：继续执行，到下一个断点或程序结束。

### 常用编辑器快捷键：

通常文本编辑器都提供了一些和编辑相关的快捷键，在Eclipse中也可以通过这些快捷键进行文本编辑。

1. 【Ctrl+C】：复制。

2. 【Ctrl+X】：剪切。

3. 【Ctrl+V】：粘贴。

4. 【Ctrl+S】：保存文件。

5. 【Ctrl+Z】：撤销。

6. 【Ctrl+Y】：重复。

7. 【Ctrl+F】：查找。

### 其他快捷键：

Eclipse中还有很多快捷键，无法一一列举，用户可以通过帮助文档找到它们的使用方式，另外还有几个常用的快捷键如下。

1. 【Ctrl+F6】：切换到下一个编辑器。

2. 【Ctrl+Shift+F6】：切换到上一个编辑器。

3. 【Ctrl+F7】：切换到下一个视图。

4. 【Ctrl+Shift+F7】：切换到上一个视图。

5. 【Ctrl+F8】：切换到下一个透视图。

6. 【Ctrl+Shift+F8】：切换到上一个透视图。

## Eclipse列编辑

其实Eclipse也有列编辑功能，不过要3.5以后的版本。要使用Eclipse的列编辑功能，只需要通过快捷键Alt+Shift+a来打开，关闭也一样。

有了列编辑功能，就可以对一块代码进行编辑了，比如一块代码的缩进，只需要选中代码块按Tab就可以了，又比如想在每行第二个字符前加入一个“test”，那么只需要向下拖动光标，使定位在每行的第二个字符，然后就可以插入啦。当然，还有更多好玩的功能可以使用，摸索一下就知道了.

## Eclipse中修改注释中@author

首先按以下步骤进入要修改的位置：
 
Window-->Preferences-->Java-->Code Style-->Code Templates
点击Comments，找到Types 然后双击填入以下几个东西即可，然后在新建类的时候在Generate comments前面√即可

    /**
     * @author 作者的名字  E-mail: 写自己的Email
     * @version 创建时间：${date}  ${time}
     */

## Eclipse Unable to install breakpoint in XXX 解决办法

我出现的原因是这样：使用ant进行编译，之后就打不了断点，这个是ant的编译eclipse不认。

解决方法：

1.要么删除class文件 重新在eclipse中编译

2.在build.xml里的javac标签里加上一句 debug="true"

## eclipse调试时鼠标移动到变量上不显示值的问题



今天同事问一问题，就说在eclipse中调试时，鼠标移动到变量上不显示值，这个原来自己也遇到过，没注意，反正就使用ctrl+shift+i嘛，也可以的，刚查了一下，解决方法如下：

 

Window->Preferences->Java->Editor->Hovers 将[Variable Values]选择即可，如果第一个[Combined Hover]已经勾选，则将这个勾去掉，勾选[Variable Values]。如果还不行，就只能用ctrl+shift+i快捷键了。

## Eclipse中如何快速替换变量

之前用别的开发工具开发的时候，要替换一个变量，直接“Ctr+H”就好了，可是用Eclipse开发的时候，使用这个快捷键，难用的要死，下面给大家介绍一种更加简便的方法在Eclipse中替换变量。

选中要替换掉的变量，按下组合键“Alt+Shift+R”，直接在键盘上输入要改为的变量，按回车键“Enter”,就可以完成替换了，文件中的所有变量都被替换完毕。

## 如何使用eclipse打开已有工程

在开始使用Eclipse的时候，会发现一个问题，那就是如何打开一个现有的Eclipse工程，开始在菜单中找了好久也没找到。

其实，Eclipse生成的结果不像VC,Jcreator那样可以直接打开，若要打开非workspace文件夹下的其他已有工程，可以打开菜单file->import→general→existing project into space.在select root directory中选中要打开的文件夹即可。此时如果选择copy existing project into workspace就会同时将文件拷贝到workspace下。这里首先要保证要保证Eclipse两个文件.classpath和.project还在，不然无法导入，就是说Eclipse的import只认自己家的东西。

## Eclipse乱码问题

我的eclipse在执行System.out.println("中文出现乱码！");时，控制台上打印的都是乱码，这个是什么问题啊！我整个eclipse的工作空间都设为UTF-8了啊！！！好晕啊！ 对啊，设置为GBK的就没有问题，我用maven跑工程的时候为什么控制台又不是乱码了？maven的那些工程都是设置的UTF-8的。 

把整个工程的“Text file encoding”属性设为GBK，就不会有乱码了。设置方法：在eclipse中右击工程，点击弹出框最下面的“Properties”，然后在弹出的窗口左侧点击“Resource”，便可以在窗口的右部看到“Text file encoding”属性，点击“Other”前的单选框，在下拉列表中选择“GBK”。最后，点击右下部的“Apply”，“OK”退出。这样设置后，你再执行System.out.println("中文出现乱码！");时控制台上就不会是乱码了。

	 

Eclipse 的控制台必须用GBK编码。所以条件1和条件4必须同时满足否则运行的还是乱码。才能保证不是乱码。

条件1，Window  | Preferences  | Workspace  |  Text fileencoding  | GBK编码。

这样定义的是整个工作区间的编码。

这样就把整个工作空间的编码格式定死了，但是如果某一个工程用的是不同的编码格式的话这样单独再解决。如下：

条件2，工程上右键  | Properties  | Resource  |  Text fileencoding  | UTF-8编码。或者适合的编码格式。这样定义的是整个工程的编码。

这样就把整个工程的编码格式定死了，但是如果某一个文件用的是不同的编码格式的话这样单独再解决。如下：

条件3，在某个文件上右键| Properties  | Resource  |  Text fileencoding  | UTF-8编码。或者适合的编码格式。这样定义的是单独某个文件的编码。

这里要说的是文件的实际编码格式优先用的是：第3个，其次再用2，最后先用1。有时候是123，必须满足条件。无论怎样这几种编码格式试一试就全知道了。



条件4，还有运行时编码设置如下：菜单：Run Configuration  | 右侧的选项卡Common 的 Console Encoding 选择GBK编码。这个是用来控制console控制台显示，必须是GBK，就不会乱码。尽管1，2，3条件都不是GBK，只要4是GBK。控制台就不会乱码。

这样保证了工作空间和工程代码编程方式和工程里的单独文件的编码格式的不冲突。

## 如何修改eclipse的默认工作空间 

打开eclipse，选择File菜单，再选择switch workspace，最后选择other，接着你就选择你想要存储的工作区间

## Eclipse中Build path specifies execution environment J2SE-1.5.There are no JREs installed.. 

提示警告：

Description Resource Path Location Type

Build path specifies execution environment J2SE-1.5. There are no JREs installed in the workspace that are strictly compatible with this environment. platform Build path JRE System Library Problem

该如何去掉这个警告?

eclipse 菜单上 window > preference 然后在 Java > Installed JRE 下面的 Execution Environment 中的 J2SE-1.5 中勾中一个 JDK，这表示将这个 JDK 展示成为 J2SE-1.5 的 JDK，以后选择 J2SE-1.5 实际上就选择了这个 JDK，因为 J2SE-1.5 有多种 JDK，我们的eclipse 项目可以仅指定要求 J2SE-1.5 的JDK 而不是 Sun JDK 1.5 或 IBM JDK 1.5 这样的具体类型，这比较方便我们使用不同的厂商的 JDK 而不用复制代码到其它机器时还要安装指定的 JDK 或修改eclipse 设置。它的好处主要体现在项目小组的协作上，很多同事可以使用不同的 JDK，我们的项目设置提交到 CVS/SVN 上之后都不用修改项目设置本身，当大家 JDK 不同时只需要自己修改 eclipse 自己的 JDK 参数，这样你使用 32 位还是 64 位没关系，使用 Sun , IBM 还是 BEA Jrocket 或 Open JDK 都没关系。

## Eclipse使用第三方jar包

1.	右键项目名称，Build Path > Add External Archives

2.	右键项目名称，Properties > Java Build Path > Libraries > Add jars

## Eclipse设置编译文件.class输出路径

### 为项目设置.class设置输出路径

右键项目 > Properties > Java Build Path > Source > Default Output Folder

设置完成后，src中的.java文件编译后生成的.class文件与package所对应的目录一起

存放在classes目录中。

### 设置全局.class文件输出路径

Window > Preferences > Java > Build Path > Source and Output Folder

设置完成后再新建项目的时候会自动的将.class文件放置在你所设置的目录中

## Eclipse 中给项目自动创建ant的build.xml文件

Eclipse 自动生成 Ant的Build.xml 配置文件,生成的方法很隐蔽 

选择你要生成Build.xml文件的项目,右键. Export-> General -> Ant Buildfiles .

点Next,再点Finish.生成完毕.希望使用的可以试试了。总算不用再傻傻的自己编写build.xml了。





## Eclipse中添加Src和JavaDoc

Eclipse有直接查看java文档和类库源码的功能，不过得手工添加才行，下面对如何在Eclipse中添加java文档和类库源码进行总结。



1. Window->Pereferences...打开参数选择对话框，展开Java节点，单击“InstalledJREs"，此时右边窗口会显示已经加载的jre。



2. 选中要设置的jre版本，单击"Edit"，弹出JRE编辑窗口



3. 添加javadoc：将JREsystem libraries下的所有包选中，单击右边的“JavadocLocation”按钮，弹出javadoc设置窗口。选择“JavadocURL”单选框，单击“Browse”按钮，选中docs/api目录，然后点击“OK”



4. 添加source：将JREsystem libraries下的所有包选中，单击右边的“SourceAttachment”按钮，弹出sourceattachment configuration窗口。单击“ExternalFile”按钮，选中java安装目录中的src.zip文件，然后点击“OK”



5.后面就一路OK、确定就行了。



在添加好了javadoc与source后，在eclipse中，使用快捷键"Shift+F2"，可快速调出选中类的api文档；使用快捷建F3（或在类上点击右键，现在查看声明），可打开类的源文件。

## eclipse中禁用javadoc注释的Format功能

在用eclipse进行java开发时，经常需要添加一些必要的javadoc注释。可是每当进行Format操作时（亦即按快捷键：Ctrl+Shift+F时），就会对排版进行自作聪明的调整，但往往这种调整是开发者不愿意看到的。举例如下：

程序员希望的注释格式：

/**

* 根据文件开头的BOM（如果存在的话），判断文件的编码格式。

* 文本文件有各种不同的编码格式，如果判断有误，则会导致显示或保存错误。

* 为了标识文件的编码格式，便于编辑和保存，则在文件开头加入了BOM，用以标识编码格式。

* UTF-8格式：0xef 0xbb 0xbf

* Unicode Little Endian格式：0xff 0xfe

* Unicode Big Endian格式：0xfe 0xff

* 而ANSI格式是没有BOM的。

* 另有一种不含BOM的UTF-8格式的文件，则不易与ANSI相区分，因此未能识别此类格式。

* 

* @param file 待判断的文件

*/

执行Format操作后，注释格式却变为：

/**

 * 根据文件开头的BOM（如果存在的话），判断文件的编码格式。 文本文件有各种不同的编码格式，如果判断有误，则会导致显示或保存错误。

* 为了标识文件的编码格式，便于编辑和保存，则在文件开头加入了BOM，用以标识编码格式。 UTF-8格式：0xef 0xbb 0xbf， Unicode

  * Little Endian格式：0xff 0xfe， Unicode Big Endian格式：0xfe

  * 0xff。而ANSI格式是没有BOM的。另有一种不含BOM的UTF-8格式的文件，则不易与ANSI相区分，因此未能识别此类格式。

* 

  * @param file

  *          待判断的文件

*/

以上2种排版格式，哪一个更直观清晰，相信不用多说。那么如何禁用eclipse对javadoc注释的Format功能呢？其实很简单，操作如下：

依次选择菜单：Window->Preferences...->java->Code Style->Formatter。

如果"Active profile"为默认的profile，则可以选择：New...打开New Profile对话框，输入Profile name为：My-Profile（自定义的名称）

如果"Active profile"为自定义的profile可直接选择Edit...->Comments，去掉"Enable Javadoc comment formatting"的选择->OK。

注：系统默认的profile是不可以直接编辑的，只能新建一个profile，然后才能Edit...。

## eclipse 自动补全的设置，不用按 alt-/ 了

偶然间看到了这个，或许有和我一样不喜欢按 alt-/ 兄弟用得上。不用老去按那个 alt-/ 了，还是方便不少。 

打开 Eclipse -> Window -> Perferences，会打开个Perferences 的设置界面。 

会看到只有一个"."存在。表示：只有输入"."之后才会有代码提示，我们要修改的地方就是这里，可是Eclipse默认只允许输入4个自定义字符。 

不过我们可以把当前的设置导出，保存为一个文件，然后在文件中修改，再导入设置，这样就可以突破Eclipse的限制。 先把上图中"."的地方输入几个随便的字符，例如"asdf"，点最下面的"OK"来保存设置。 然后打开 Eclipse的 File -> Export,在窗口中展开 General -> Perferences-->Export all然后点击 NEXT。然后点击"Browse"选择任意的一个路径，保存配置文件，然后点击"Finish"。 用记事本打开刚才保存的那个配置文件（扩展文件名：*.epf），按"ctrl + F"，输入刚才设置的"asdf"，找到刚才字符串。把"asdf"修改为"abcdefghijklmnopqrstuvwxyz."，然后保存，退出记事本。 打 开Eclipse的 File -> Import 然后在打开的窗口里展开 General -> Perferences，点击NEXT，选中刚才修改过的配置文件，Finish。现在，再打开Window -> Perferences，并依次展开 Java -> Editor -> Content Assist，会发现已经超过了4个字符，也就是说我们输入任何字母和"."都会有代码提示了。 

修改之后，默认是你输入某个字符200毫秒之后出现代码提示，如果出现输入很卡的情况，需要把提示延迟调高一些；如果你嫌它太慢，可以修改成更小的数字，不过数字改的越小，对系统性能的要求就越高，我设置的是50毫秒。现在，Eclipse用起来是不是更加顺手了？

## Eclipse中的classpath拒绝访问

文件是隐藏了，取消隐藏之后就可以了

## 通过Eclipse中的Java Build Path 时报错Could not write file: xx:\xx\.classpath

通过Eclipse的import一个项目到工作台。在通过Java Build Path修改classpath时报错，网上收到解决方法：确保Eclipse说的那个文件不是可读，确保文件不是隐藏的。经过检查我的文件时隐藏，修改属性再试。没问题了。

## eclipse中,把java函数代码折叠/展开

首先在eclipse 中开启设置代码折叠功能

1. windows->perferences->General->Editors->Structured Text Editors

可以看到Enable folding选项，打上勾就可以使用代码折叠功能，但还要在具体的语言中设置。

2、

windows->perferences->Java->Editors->Folding

可以看到Enable folding选项，打上勾就可以使用代码折叠功能。

其次 使用快捷键

下面你就可以用如下快捷键在你的java class 中 折叠或者展开你的代码了.

代码折叠的快捷键，默认是：

    Ctrl+Shift+Numpad_Divede(小键盘的/号)

    Ctrl+Shift+Numpad_Multiply(小键盘的*号)

笔记本没小键盘，于是改成：

    Ctrl+Shift+-

    Ctrl+Shift+=

## Eclipse空心J 实心J

Eclipse中Java文件图标由实心J变成空心J的问题。空心J的java文件，不被包含在项目中进行编译，而是当做资源存在项目中。在网上搜到的两种解决办法：

办法1：

右击该文件 --> BuildPath --> Include

正常实心J时，该选项为 Exclude

方法2：

BuildPath-->configure buildpath--->source中添加需要被包含的代码

没太看懂，最后用类似的方法解决的：

选中工程--右键Properties--Java Build Path--Source

找到出现空心J的Java文件所在的包，展开树，正常情况为：

Included:(All)

Excluded:(None)

Native library location:(None)

我的工程中Exclued项有空心J的Java文件的目录，选中Excluded，点左侧Remove，然后确定.

## eclipse 保存文件时候自动格式化及import 条目优化

在eclipse设置页面，java -> editor-> save actions.进行设置，当你ctrl +s 时候，格式和import 条目优化全搞定

## Eclipse一直building workspace问题解决

在项目右键点击->Properties->Builder->Maven Project Builder取消勾选就可以了。其他保持不变。

## build.properties does not exist 

在导入工程时，老是报：build.properties does not exist错误，不甚其烦，原因是.project文件中设置了:

<nature>org.eclipse.pde.PluginNature</nature>

导致对build.properties的引用，但是build.properties 并不存在。处理办法就是将其注释掉：

<!--<nature>org.eclipse.pde.PluginNature</nature>-->



# C++和Java的不同

作为一名C++程序员，我们早已掌握了面向对象程序设计的基本概念，而且Java的语法无疑是非常熟悉的。事实上，Java本来就是从C++衍生出来的。然而C++和Java之间仍存在一些显著的差异。可以这样说，这些差异代表着技术的极大进步。一旦我们弄清楚了这些差异，就会理解为什么说Java是一种更加优秀的程序设计语言。本文将引导大家认识用于区分Java和C++的一些重要特征。

(1) 最大的障碍在于速度：解释过的Java要比C的执行速度慢上约20倍。无论什么都不能阻止对Java语言进行编译。一些准实时编译器，它们能显著加快速度。当然，我们完全有理由认为会出现适用于更多流行平台的纯固有编译器，但假若没有那些编译器，由于速度的限制，必然有些问题是Java不能解决的。

(2) 和C++一样，Java也提供了两种类型的注释。

(3) 所有东西都必须置入一个类。不存在全局函数或者全局数据。如果想获得与全局函数等价的功能，可考虑将static方法和static数据置入一个类里。注意没有像结构、枚举或者联合这一类的东西，一切只有“类”（Class）。

(4) 所有方法都是在类的主体定义的。所以用C++的眼光看，似乎所有函数都已嵌入，但实情并非如此（嵌入的问题在后面讲述）。

(5) 在Java中，类定义采取几乎和C++一样的形式。但没有标志结束的分号。没有class foo这种形式的类声明，只有类定义。



class aType(){

void aMethod() {/* 方法主体 */}

}

(6) Java中没有作用域范围运算符“::”。Java利用点号(引用符)做所有的事情，但可以不用考虑它，因为只能在一个类里定义元素。即使那些方法定义，也必须在一个类的内部，所以根本没有必要指定作用域的范围。我们注意到的一项差异是对static方法的调用：使用ClassName.methodName()。除此以外，package（包）的名字是用点号建立的，并能用import关键字实现C++的“#include”的一部分功能。例如下面这个语句：

import java.awt.*;

（#include并不直接映射成import，但在使用时有类似的感觉。）

(7) 与C++类似，Java含有一系列“主类型”（Primitive type），以实现更有效率的访问。在Java中，这些类型包括boolean，char，byte，short，int，long，float以及double。所有主类型的大小都是固有的，且与具体的机器无关（考虑到移植的问题）。这肯定会对性能造成一定的影响，具体取决于不同的机器。对类型的检查和要求在Java里变得更苛刻。例如：条件表达式只能是boolean类型，不可使用整数；必须使用象X+Y这样的一个表达式的结果；不能仅仅用“X+Y”来实现“副作用”。

(8) char（字符）类型使用国际通用的16位Unicode字符集，所以能自动表达大多数国家的字符。

(9) 静态引用的字串会自动转换成String对象。和C及C++不同，没有独立的静态字符数组字串可供使用。

(10) Java增添了三个右移位运算符“>>>”，具有与“逻辑”右移位运算符类似的功用，可在最末尾插入零值。“>>”则会在移位的同时插入符号位（即“算术”移位）。

(11) 尽管表面上类似，但与C++相比，Java数组采用的是一个颇为不同的结构，并具有独特的行为。有一个只读的length成员，通过它可知道数组有多大。而且一旦超过数组边界，运行期检查会自动抛出一个异常。所有数组都是在内存“堆”里创建的，我们可将一个数组分配给另一个（只是简单地复制数组句柄）。数组标识符属于第一级对象，它的所有方法通常都适用于其他所有对象。

(12) 对于所有不属于主类型的对象，都只能通过new命令创建。和C++不同，Java没有相应的命令可以“在堆栈上”创建不属于主类型的对象。所有主类型都只能在堆栈上创建，同时不使用new命令。所有主要的类都有自己的“封装（器）”类，所以能够通过new创建等价的、以内存“堆”为基础的对象（主类型数组是一个例外：它们可象C++那样通过集合初始化进行分配，或者使用new）。

(13) Java中不必进行提前声明。若想在定义前使用一个类或方法，只需直接使用它即可——编译器会保证使用恰当的定义。所以和在C++中不同，我们不会碰到任何涉及提前引用的问题。

(14) Java没有预处理机。若想使用另一个库里的类，只需使用import命令，并指定库名即可。不存在类似于预处理机的宏。

(15) Java用包代替了命名空间。由于将所有东西都置入一个类，而且由于采用了一种名为“封装”的机制，它能针对类名进行类似于命名空间分解的操作，所以命名的问题不再进入我们的考虑之列。数据包也会在单独一个库名下收集库的组件。我们只需简单地“import”（导入）一个包，剩下的工作会由编译器自动完成。

(16) 被定义成类成员的对象句柄会自动初始化成null。对基本类数据成员的初始化在Java里得到了可靠的保障。若不明确地进行初始化，它们就会得到一个默认值（零或等价的值）。可对它们进行明确的初始化（显式初始化）：要么在类内定义它们，要么在构建器中定义。采用的语法比C++的语法更容易理解，而且对于static和非static成员来说都是固定不变的。我们不必从外部定义static成员的存储方式，这和C++是不同的。

(17) 在Java里，没有象C和C++那样的指针。用new创建一个对象的时候，会获得一个引用（本书一直将其称作“句柄”）。例如：

String s = new String("howdy");

然而，C++引用在创建时必须进行初始化，而且不可重定义到一个不同的位置。但Java引用并不一定局限于创建时的位置。它们可根据情况任意定义，这便消除了对指针的部分需求。在C和C++里大量采用指针的另一个原因是为了能指向任意一个内存位置（这同时会使它们变得不安全，也是Java不提供这一支持的原因）。指针通常被看作在基本变量数组中四处移动的一种有效手段。Java允许我们以更安全的形式达到相同的目标。解决指针问题的终极方法是“固有方法”（已在附录A讨论）。将指针传递给方法时，通常不会带来太大的问题，因为此时没有全局函数，只有类。而且我们可传递对对象的引用。Java语言最开始声称自己“完全不采用指针！”但随着许多程序员都质问没有指针如何工作？于是后来又声明“采用受到限制的指针”。大家可自行判断它是否“真”的是一个指针。但不管在何种情况下，都不存在指针“算术”。

(18) Java提供了与C++类似的“构建器”，即构造函数（Constructor）。如果不自己定义一个，就会获得一个默认构建器。而如果定义了一个非默认的构建器，就不会为我们自动定义默认构建器。这和C++是一样的。注意没有复制构建器，因为所有自变量都是按引用传递的。

(19) Java中没有“破坏器”（Destructor）。变量不存在“作用域”的问题。一个对象的“存在时间”是由对象的存在时间决定的，并非由垃圾收集器决定。有个finalize()方法是每一个类的成员，它在某种程度上类似于C++的“破坏器”。但finalize()是由垃圾收集器调用的，而且只负责释放“资源”（如打开的文件、套接字、端口、URL等等）。如需在一个特定的地点做某样事情，必须创建一个特殊的方法，并调用它，不能依赖finalize()。而在另一方面，C++中的所有对象都会（或者说“应该”）破坏，但并非Java中的所有对象都会被当作“垃圾”收集掉。由于Java不支持破坏器的概念，所以在必要的时候，必须谨慎地创建一个清除方法。而且针对类内的基础类以及成员对象，需要明确调用所有清除方法。

(20) Java具有方法“过载”机制，它的工作原理与C++函数的过载几乎是完全相同的。

(21) Java不支持默认自变量。

(22) Java中没有goto。它采取的无条件跳转机制是“break 标签”或者“continue 标准”，用于跳出当前的多重嵌套循环。

(23) Java采用了一种单根式的分级结构，因此所有对象都是从根类Object统一继承的。而在C++中，我们可在任何地方启动一个新的继承树，所以最后往往看到包含了大量树的“一片森林”。在Java中，我们无论如何都只有一个分级结构。尽管这表面上看似乎造成了限制，但由于我们知道每个对象肯定至少有一个Object接口，所以往往能获得更强大的能力。C++目前似乎是唯一没有强制单根结构的唯一一种OO语言。

(24) Java没有模板或者参数化类型的其他形式。它提供了一系列集合：Vector（向量），Stack（堆栈）以及Hashtable（散列表），用于容纳Object引用。利用这些集合，我们的一系列要求可得到满足。但这些集合并非是为实现象C++“标准模板库”（STL）那样的快速调用而设计的。Java 1.2中的新集合显得更加完整，但仍不具备正宗模板那样的高效率使用手段。

(25) “垃圾收集”意味着在Java中出现内存漏洞的情况会少得多，但也并非完全不可能（若调用一个用于分配存储空间的固有方法，垃圾收集器就不能对其进行跟踪监视）。然而，内存漏洞和资源漏洞多是由于编写不当的finalize()造成的，或是由于在已分配的一个块尾释放一种资源造成的（“破坏器”在此时显得特别方便）。垃圾收集器是在C++基础上的一种极大进步，使许多编程问题消弥于无形之中。但对少数几个垃圾收集器力有不逮的问题，它却是不大适合的。但垃圾收集器的大量优点也使这一处缺点显得微不足道。

(26) Java内建了对多线程的支持。利用一个特殊的Thread类，我们可通过继承创建一个新线程（放弃了run()方法）。若将synchronized（同步）关键字作为方法的一个类型限制符使用，相互排斥现象会在对象这一级发生。在任何给定的时间，只有一个线程能使用一个对象的synchronized方法。在另一方面，一个synchronized方法进入以后，它首先会“锁定”对象，防止其他任何synchronized方法再使用那个对象。只有退出了这个方法，才会将对象“解锁”。在线程之间，我们仍然要负责实现更复杂的同步机制，方法是创建自己的“监视器”类。递归的synchronized方法可以正常运作。若线程的优先等级相同，则时间的“分片”不能得到保证。

(27) 我们不是象C++那样控制声明代码块，而是将访问限定符（public，private和protected）置入每个类成员的定义里。若未规定一个“显式”（明确的）限定符，就会默认为“友好的”（friendly）。这意味着同一个包里的其他元素也可以访问它（相当于它们都成为C++的“friends”——朋友），但不可由包外的任何元素访问。类——以及类内的每个方法——都有一个访问限定符，决定它是否能在文件的外部“可见”。private关键字通常很少在Java中使用，因为与排斥同一个包内其他类的访问相比，“友好的”访问通常更加有用。然而，在多线程的环境中，对private的恰当运用是非常重要的。Java的protected关键字意味着“可由继承者访问，亦可由包内其他元素访问”。注意Java没有与C++的protected关键字等价的元素，后者意味着“只能由继承者访问”（以前可用“private protected”实现这个目的，但这一对关键字的组合已被取消了）。

(28) 嵌套的类。在C++中，对类进行嵌套有助于隐藏名称，并便于代码的组织（但C++的“命名空间”已使名称的隐藏显得多余）。Java的“封装”或“打包”概念等价于C++的命名空间，所以不再是一个问题。Java 1.1引入了“内部类”的概念，它秘密保持指向外部类的一个句柄——创建内部类对象的时候需要用到。这意味着内部类对象也许能访问外部类对象的成员，毋需任何条件——就好象那些成员直接隶属于内部类对象一样。这样便为回调问题提供了一个更优秀的方案——C++是用指向成员的指针解决的。

(29) 由于存在前面介绍的那种内部类，所以Java里没有指向成员的指针。

(30) Java不存在“嵌入”（inline）方法。Java编译器也许会自行决定嵌入一个方法，但我们对此没有更多的控制权力。在Java中，可为一个方法使用final关键字，从而“建议”进行嵌入操作。然而，嵌入函数对于C++的编译器来说也只是一种建议。

(31) Java中的继承具有与C++相同的效果，但采用的语法不同。Java用extends关键字标志从一个基础类的继承，并用super关键字指出准备在基础类中调用的方法，它与我们当前所在的方法具有相同的名字（然而，Java中的super关键字只允许我们访问父类的方法——亦即分级结构的上一级）。通过在C++中设定基础类的作用域，我们可访问位于分级结构较深处的方法。亦可用super关键字调用基础类构建器。正如早先指出的那样，所有类最终都会从Object里自动继承。和C++不同，不存在明确的构建器初始化列表。但编译器会强迫我们在构建器主体的开头进行全部的基础类初始化，而且不允许我们在主体的后面部分进行这一工作。通过组合运用自动初始化以及来自未初始化对象句柄的异常，成员的初始化可得到有效的保证。

public class Foo extends Bar {

  public Foo(String msg) {

    super(msg); // Calls base constructor

  }

  public baz(int i) { // Override

    super.baz(i); // Calls base method

  }

}

(32) Java中的继承不会改变基础类成员的保护级别。我们不能在Java中指定public，private或者protected继承，这一点与C++是相同的。此外，在衍生类中的优先方法不能减少对基础类方法的访问。例如，假设一个成员在基础类中属于public，而我们用另一个方法代替了它，那么用于替换的方法也必须属于public（编译器会自动检查）。

(33) Java提供了一个interface关键字，它的作用是创建抽象基础类的一个等价物。在其中填充抽象方法，且没有数据成员。这样一来，对于仅仅设计成一个接口的东西，以及对于用extends关键字在现有功能基础上的扩展，两者之间便产生了一个明显的差异。不值得用abstract关键字产生一种类似的效果，因为我们不能创建属于那个类的一个对象。一个abstract（抽象）类可包含抽象方法（尽管并不要求在它里面包含什么东西），但它也能包含用于具体实现的代码。因此，它被限制成一个单一的继承。通过与接口联合使用，这一方案避免了对类似于C++虚拟基础类那样的一些机制的需要。

为创建可进行“例示”（即创建一个实例）的一个interface（接口）的版本，需使用implements关键字。它的语法类似于继承的语法，如下所示：

public interface Face {

  public void smile();

}

public class Baz extends Bar implements Face {

  public void smile( ) {

    System.out.println("a warm smile");

  }

}

(34) Java中没有virtual关键字，因为所有非static方法都肯定会用到动态绑定。在Java中，程序员不必自行决定是否使用动态绑定。C++之所以采用了virtual，是由于我们对性能进行调整的时候，可通过将其省略，从而获得执行效率的少量提升（或者换句话说：“如果不用，就没必要为它付出代价”）。virtual经常会造成一定程度的混淆，而且获得令人不快的结果。final关键字为性能的调整规定了一些范围——它向编译器指出这种方法不能被取代，所以它的范围可能被静态约束（而且成为嵌入状态，所以使用C++非virtual调用的等价方式）。这些优化工作是由编译器完成的。

(35) Java不提供多重继承机制（MI），至少不象C++那样做。与protected类似，MI表面上是一个很不错的主意，但只有真正面对一个特定的设计问题时，才知道自己需要它。由于Java使用的是“单根”分级结构，所以只有在极少的场合才需要用到MI。interface关键字会帮助我们自动完成多个接口的合并工作。

(36) 运行期的类型标识功能与C++极为相似。例如，为获得与句柄X有关的信息，可使用下述代码：

X.getClass().getName();

为进行一个“类型安全”的紧缩造型，可使用：

derived d = (derived)base;

这与旧式风格的C造型是一样的。编译器会自动调用动态造型机制，不要求使用额外的语法。尽管它并不象C++的“new casts”那样具有易于定位造型的优点，但Java会检查使用情况，并丢弃那些“异常”，所以它不会象C++那样允许坏造型的存在。

(37) Java采取了不同的异常控制机制，因为此时已经不存在构建器。可添加一个finally从句，强制执行特定的语句，以便进行必要的清除工作。Java中的所有异常都是从基础类Throwable里继承而来的，所以可确保我们得到的是一个通用接口。

public void f(Obj b) throws IOException {

  myresource mr = b.createResource();

  try {

    mr.UseResource();

  } catch (MyException e) { 

    // handle my exception

  } catch (Throwable e) { 

    // handle all other exceptions

  } finally {

    mr.dispose(); // special cleanup

  }

}

(38) Java的异常规范比C++的出色得多。丢弃一个错误的异常后，不是象C++那样在运行期间调用一个函数，Java异常规范是在编译期间检查并执行的。除此以外，被取代的方法必须遵守那一方法的基础类版本的异常规范：它们可丢弃指定的异常或者从那些异常衍生出来的其他异常。这样一来，我们最终得到的是更为“健壮”的异常控制代码。

(39) Java具有方法过载的能力，但不允许运算符过载。String类不能用+和+=运算符连接不同的字串，而且String表达式使用自动的类型转换，但那是一种特殊的内建情况。

(40) 通过事先的约定，C++中经常出现的const问题在Java里已得到了控制。我们只能传递指向对象的句柄，本地副本永远不会为我们自动生成。若希望使用类似C++按值传递那样的技术，可调用clone()，生成自变量的一个本地副本（尽管clone()的设计依然尚显粗糙——参见第12章）。根本不存在被自动调用的副本构建器。为创建一个编译期的常数值，可象下面这样编码：

static final int SIZE = 255

static final int BSIZE = 8 * SIZE

(41) 由于安全方面的原因，“应用程序”的编程与“程序片”的编程之间存在着显著的差异。一个最明显的问题是程序片不允许我们进行磁盘的写操作，因为这样做会造成从远程站点下载的、不明来历的程序可能胡乱改写我们的磁盘。随着Java 1.1对数字签名技术的引用，这一情况已有所改观。根据数字签名，我们可确切知道一个程序片的全部作者，并验证他们是否已获得授权。Java 1.2会进一步增强程序片的能力。

(42) 由于Java在某些场合可能显得限制太多，所以有时不愿用它执行象直接访问硬件这样的重要任务。Java解决这个问题的方案是“固有方法”，允许我们调用由其他语言写成的函数（目前只支持C和C++）。这样一来，我们就肯定能够解决与平台有关的问题（采用一种不可移植的形式，但那些代码随后会被隔离起来）。程序片不能调用固有方法，只有应用程序才可以。

(43) Java提供对注释文档的内建支持，所以源码文件也可以包含它们自己的文档。通过一个单独的程序，这些文档信息可以提取出来，并重新格式化成HTML。这无疑是文档管理及应用的极大进步。

(44) Java包含了一些标准库，用于完成特定的任务。C++则依靠一些非标准的、由其他厂商提供的库。这些任务包括：连网、数据库连接（通过JDBC）、多线程、分布式对象（通过RMI和CORBA）、压缩、商贸等，由于这些库简单易用，而且非常标准，所以能极大加快应用程序的开发速度。

(45) Java 1.1包含了Java Beans标准，后者可创建在可视编程环境中使用的组件。由于遵守同样的标准，所以可视组件能够在所有厂商的开发环境中使用。由于我们并不依赖一家厂商的方案进行可视组件的设计，所以组件的选择余地会加大，并可提高组件的效能。除此之外，Java Beans的设计非常简单，便于程序员理解；而那些由不同的厂商开发的专用组件框架则要求进行更深入的学习。

(46) 若访问Java句柄失败，就会丢弃一次异常。这种丢弃测试并不一定要正好在使用一个句柄之前进行。根据Java的设计规范，只是说异常必须以某种形式丢弃。许多C++运行期系统也能丢弃那些由于指针错误造成的异常。

(47) Java通常显得更为健壮，为此采取的手段如下：

对象句柄初始化成null（一个关键字）

句柄肯定会得到检查，并在出错时丢弃异常

所有数组访问都会得到检查，及时发现边界违例情况

自动垃圾收集，防止出现内存漏洞

明确、“傻瓜式”的异常控制机制

为多线程提供了简单的语言支持

对网络程序片进行字节码校验

# Java和C++区别

## 概括

JAVA的优势在于：跨平台，开源，有甲骨文、ibm等大公司的强力支持，简单易学。C++最大的优势在于她的通用和全面。

JAVA和C++都是面向对象语言。也就是说，它们都能够实现面向对象思想（封装，继乘，多态）。而由于C++为了照顾大量的C语言使用者，而兼容了C，使得自身仅仅成为了带类的C语言，多多少少影响了其面向对象的彻底性。JAVA则是完全的面向对象语言，它句法更清晰，规模更小，更易学。它是在对多种程序设计语言进行了深入细致研究的基础上，摒弃了其他语言的不足之处，从根本上解决了C++的固有缺陷。 

Java和C++的相似之处多于不同之处，但两种语言有几处主要的不同使得Java更容易学习，并且编程环境更为简单。 我在这里不能完全列出不同之处，仅列出比较显著的区别： 

指针：JAVA语言让编程者无法通过指针来直接访问内存，并且增添了自动的内存管理功能，从而有效地防止了C／C++语言中指针操作失误，如野指针所造成的系统崩溃。但也不是说JAVA没有指针，虚拟机内部还是使用了指针，只是外人不得使用而已。这有利于Java程序的安全。 

多重继承：C++支持多重继承，这是C++的一个特征，它允许多父类派生一个类。尽管多重继承功能很强，但使用复杂，而且会引起许多麻烦，编译程序实现它也很不容易。Java不支持多重继承，但允许一个类继承多个接口(extends+implement)，实现了C++多重继承的功能，又避免了C++中的多重继承实现方式带来的诸多不便。

数据类型及类：Java是完全面向对象的语言，所有函数和变量都必须是类的一部分。除了基本数据类型之外，其余的都作为类对象，包括数组。对象将数据和方法结合起来，把它们封装在类中，这样每个对象都可实现自己的特点和行为。而C++允许将函数和变量定义为全局的。此外，Java中取消了C／C++中的结构和联合，消除了不必要的麻烦。 

自动内存管理：Java程序中所有的对象都是用new操作符建立在内存堆栈上，这个操作符类似于C++的new操作符。下面的语句由一个建立了一个类Read的对象，然后调用该对象的work方法：

Read r＝new Read()；

r.work()；

语句Read r＝new Read()；在堆栈结构上建立了一个Read的实例。Java自动进行无用内存回收操作，不需要程序员进行删除。而C++中必须由程序员释放内存资源，增加了程序设计者的负担。Java中当一个对象不被再用到时，无用内存回收器将给它加上标签以示删除。JAVA里无用内存回收程序是以线程方式在后台运行的，利用空闲时间工作。

操作符重载：Java不支持操作符重载。操作符重载被认为是C++的突出特征，在Java中虽然类大体上可以实现这样的功能，但操作符重载的方便性仍然丢失了不少。Java语言不支持操作符重载是为了保持Java语言尽可能简单。

预处理功能：Java不支持预处理功能。C／C++在编译过程中都有一个预编泽阶段，即众所周知的预处理器。预处理器为开发人员提供了方便，但增加了编译的复杂性。JAVA虚拟机没有预处理器，但它提供的引入语句(import)与C++预处理器的功能类似。 

缺省函数参数：Java不支持缺省函数参数，而C++支持。

函数：在C中，代码组织在函数中，函数可以访问程序的全局变量。C++增加了类，提供了类算法，该算法是与类相连的函数，C++类方法与Java类方法十分相似，然而，由于C++仍然支持C，所以不能阻止C++开发人员使用函数，结果函数和方法混合使用使得程序比较混乱。Java没有函数，作为一个比C++更纯的面向对象的语言，Java强迫开发人员把所有例行程序包括在类中，事实上，用方法实现例行程序可激励开发人员更好地组织编码。 

字符串 ：C和C++不支持字符串变量，在C和C++程序中使用Null终止符代表字符串的结束，在Java中字符串是用类对象(string和stringBuffer)来实现的，这些类对象是Java语言的核心，用类对象实现字符串有以下几个优点：

	在整个系统中建立字符串和访问字符串元素的方法是一致的；

	Java字符串类是作为Java语言的一部分定义的，而不是作为外加的延伸部分； 

	Java字符串执行运行时检空，可帮助排除一些运行时发生的错误；

	可对字符串用“+”进行连接操作。

goto语句：“可怕”的goto语句是C和C++的“遗物”，它是该语言技术上的合法部分，引用goto语句引起了程序结构的混乱，不易理解，goto语句子要用于无条件转移子程序和多结构分支技术。鉴于以广理由，Java不提供goto语句，它虽然指定goto作为关键字，但不支持它的使用，使程序简洁易读。

类型转换：在C和C++中有时出现数据类型的隐含转换，这就涉及了自动强制类型转换问题。例如，在C++中可将一浮点值赋予整型变量，并去掉其尾数。Java不支持C++中的自动强制类型转换，如果需要，必须由程序显式进行强制类型转换。 

异常：JAVA中的异常机制用于捕获例外事件，增强系统容错能力

try{／／可能产生例外的代码

}catch(exceptionType name){ //处理

}

其中exceptionType表示异常类型。而C++则没有如此方便的机制。

## 概括2

Java并不仅仅是C++语言的一个变种，它们在某些本质问题上有根本的不同：

Java比C++程序可靠性更高。有人曾估计每50行C++程序中至少有一个BUG.姑且不去讨论这个数字是否夸张，但是任何一个C++程序员都不得不承认C++语言在提供强大的功能的同时也提高了程序含BUG的可能性。Java语言通过改变语言的特性大大提高了程序的可靠性。

Java语言不需要程序对内存进行分配和回收。Java丢弃了C++ 中很少使用的、很难理解的、令人迷惑的那些特性，如操作符重载、多继承、自动的强制类型转换。特别地，Java语言不使用指针，并提供了自动的废料收集，Examda提示：在Java语言中，内存的分配和回收都是自动进行的，程序员无须考虑内存碎片的问题。

Java语言中没有指针的概念，引入了真正的数组。不同于C++中利用指针实现的“伪数组”，Examda，Java引入了真正的数组，同时将容易造成麻烦的指针从语言中去掉，这将有利于防止在C++程序中常见的因为数组操作越界等指针操作而对系统数据进行非法读写带来的不安全问题。

Java用接口（Interface）技术取代C++程序中的多继承性。接口与多继承有同样的功能，但是省却了多继承在实现和维护上的复杂性。

## 工作中造成的影响

C++开发成本高，C++是微软支持的，比如做一个WEB网站，那么首先你要购买正版的WINDOW系统，加上正版的WEB服务器。这可是笔不小的开销。JAVA的话，操作系统可以使用免费的LINUX，服务器有免费的，当然也有收费的。总体来收开销要远小于C++的.net。

C++比JAVA快，当然这不是绝对的。如果你熟悉JAVA的工作原理就明白了。JAVA是在原有的系统再添加一层虚拟机运行的。而C++会有微软支持（操作系统级别的支持，且无任何中间机制，所以速度要快）。这也就是为什么游戏大部分是采用C++开发的原因。不过随着硬件的速度越来越快，这点最终会被克服。

# Java 序列化

序列化的用处：

	对象需要远程调用（比如说socket）

	对象需要在不同的进程间调用

	对象需要永久存放在硬盘上（脱离对象运行环境，编写成一个以字符串形式存在的对象，需要时，通过获取字符串，反序列化就能实现获取一个对象）

首先说明一下序列化的知识：

	java中的序列化(serialization)机制能够将一个实例对象的状态信息写入到一个字节流中，使其可以通过socket进行传输、或者持久化存储到数据库或文件系统中；然后在需要的时候，可以根据字节流中的信息来重构一个相同的对象。序列化机制在java中有着广泛的应用，EJB、 RMI等技术都是以此为基础的。

序列化机制是通过java.io.ObjectOutputStream类和java.io.ObjectInputStream类来实现的。在 序列化(serialize)一个对象的时候，会先实例化一个ObjectOutputStream对象，然后调用其writeObject()方法；在反序列化(deserialize)的时候，则会实例化一个ObjectInputStream对象，然后调用其readObject()方法。

Java的序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与本地相应实体（类）的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常。 

当实现java.io.Serializable接口的实体（类）没有显式地定义一个名为serialVersionUID，类型为long的变量时，Java序列化机制会根据编译的class自动生成一个serialVersionUID作序列化版本比较用，这种情况下，只有同一次编译生成的 class才会生成相同的serialVersionUID 。 

如果我们不希望通过编译来强制划分软件版本，即实现序列化接口的实体能够兼容先前版本，未作更改的类，就需要显式地定义一个名为serialVersionUID，类型为long的变量，不修改这个变量值的序列化实体都可以相互进行串行化和反串行化。 

设置 serialVersionUID默认的生成方式：

	private static final long serialVersionUID = 545456546548431L; 

serialVersionUID的作用：serialVersionUID 用来表明类的不同版本间的兼容性。如果你修改了此类, 要修改此值。否则以前用老版本的类序列化的类恢复时会出错。 

在JDK中，可以利用JDK的bin目录下的serialver.exe工具产生这个serialVersionUID，对于Test.class，执行命令：serialver Test。

为了在反序列化时，确保类版本的兼容性，最好在每个要序列化的类中加入 private static final long serialVersionUID这个属性，具体数值自己定义。这样，即使某个类在与之对应的对象已经序列化出去后做了修改，该对象依然可以被正确反序列化。否则，如果不显式定义该属性，这个属性值将由JVM根据类的相关信息计算，而修改后的类的计算结果与修改前的类的计算结果往往不同，从而造成对象的反序列化因为类版本不兼容而失败。不显式定义这个属性值的另一个坏处是，不利于程序在不同的JVM之间的移植。因为不同的编译器实现该属性值的计算策略可能不同，从而造成虽然类没有改变，但是因为JVM不同，出现因类版本不兼容而无法正确反序列化的现象出现。

# Java序列化二

当两个进程在进行远程通信时，彼此可以发送各种类型的数据。无论是何种类型的数据，都会以二进制序列的形式在网络上传送。发送方需要把这个Java对象转换为字节序列，才能在网络上传送；接收方则需要把字节序列再恢复为Java对象。 把Java对象转换为字节序列的过程称为对象的序列化。把字节序列恢复为Java对象的过程称为对象的反序列化。 

对象的序列化主要有两种用途： 

1） 把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中； 

2） 在网络上传送对象的字节序列。

## JDK类库中的序列化API

java.io.ObjectOutputStream代表对象输出流，它的writeObject(Object obj)方法可对参数指定的obj对象进行序列化，把得到的字节序列写到一个目标输出流中。 

java.io.ObjectInputStream代表对象输入流，它的readObject()方法从一个源输入流中读取字节序列，再把它们反序列化为一个对象，并将其返回。

只有实现了Serializable和Externalizable接口的类的对象才能被序列化。Externalizable接口继承自 Serializable接口，实现Externalizable接口的类完全由自身来控制序列化的行为，而仅实现Serializable接口的类可以 采用默认的序列化方式 。 

对象序列化包括如下步骤： 

1） 创建一个对象输出流，它可以包装一个其他类型的目标输出流，如文件输出流； 

2） 通过对象输出流的writeObject()方法写对象。 

对象反序列化的步骤如下： 

1） 创建一个对象输入流，它可以包装一个其他类型的源输入流，如文件输入流； 

2） 通过对象输入流的readObject()方法读取对象。 

下面让我们来看一个对应的例子，类的内容如下： 



import java.io.*; 

import java.util.Date; 

public class ObjectSaver {

       public static void main(String[] args) throws Exception {

              ObjectOutputStream out = new ObjectOutputStream

                     (new FileOutputStream("D:""objectFile.obj")); 



              //序列化对象 

              Customer customer = new Customer("阿蜜果", 24); 

              out.writeObject("你好!"); 

              out.writeObject(new Date()); 

              out.writeObject(customer); 

              out.writeInt(123); //写入基本类型数据 

              out.close(); 



              //反序列化对象 

              ObjectInputStream in = new ObjectInputStream

                     (new FileInputStream("D:""objectFile.obj")); 

              System.out.println("obj1=" + (String) in.readObject()); 

              System.out.println("obj2=" + (Date) in.readObject()); 

              Customer obj3 = (Customer) in.readObject(); 

              System.out.println("obj3=" + obj3); 

              int obj4 = in.readInt(); 

              System.out.println("obj4=" + obj4);

              in.close(); 

       }

} 



class Customer implements Serializable { 

       private String name; 

       private int age; 

       public Customer(String name, int age) { 

              this.name = name; 

              this.age = age; 

       } 

       public String toString() { 

              return "name=" + name + ", age=" + age; 

       } 

} 



	输出结果如下： 

	obj1=你好! 

	obj2=Sat Sep 15 22:02:21 CST 2007 

	obj3=name=阿蜜果, age=24 

	obj4=123 

	因此例比较简单，在此不再详述。

## 实现Serializable接口

ObjectOutputStream只能对Serializable接口的类的对象进行序列化。默认情况下，ObjectOutputStream按照默认方式序列化，这种序列化方式仅仅对对象的非transient的实例变量进行序列化，而不会序列化对象 的transient的实例变量，也不会序列化静态变量。

当ObjectOutputStream按照默认方式反序列化时，具有如下特点： 

	如果在内存中对象所属的类还没有被加载，那么会先加载并初始化这个类。如果在classpath中不存在相应的类文件，那么会抛出ClassNotFoundException； 

	在反序列化时不会调用类的任何构造方法。 

如果用户希望控制类的序列化方式，可以在可序列化类中提供以下形式的writeObject()和readObject()方法。



private void writeObject(java.io.ObjectOutputStream out) throws IOException 

private void readObject(java.io.ObjectInputStream in) throws IOException, ClassNotFoundException; 

当ObjectOutputStream对一个Customer对象进行序列化时，如果该对象具有writeObject()方法，那么就会执行这一方法，否则就按默认方式序列化。在该对象的writeObjectt()方法中，可以先调用ObjectOutputStream的 defaultWriteObject()方法，使得对象输出流先执行默认的序列化操作。同理可得出反序列化的情况，不过这次是 defaultReadObject()方法。

有些对象中包含一些敏感信息，这些信息不宜对外公开。如果按照默认方式对它们序列化，那么它们的序列化数据在网络上传输时，可能会被不法份子窃取。对于这类信息，可以对它们进行加密后再序列化，在反序列化时则需要解密，再恢复为原来的信息。 

默认的序列化方式会序列化整个对象图，这需要递归遍历对象图。如果对象图很复杂，递归遍历操作需要消耗很多的空间和时间，它的内部数据结构为双向列表。 

在应用时，如果对某些成员变量都改为transient类型，将节省空间和时间，提高序列化的性能。

## 实现Externalizable接口

Externalizable接口继承自Serializable接口，如果一个类实现了Externalizable接口，那么将完全由这个类控制自身的序列化行为。Externalizable接口声明了两个方法： 

public void writeExternal(ObjectOutput out) throws IOException 

public void readExternal(ObjectInput in) throws IOException , ClassNotFoundException 

	前者负责序列化操作，后者负责反序列化操作。 在对实现了Externalizable接口的类的对象进行反序列化时，会先调用类的不带参数的构造方法，这是有别于默认反序列方式的。如果把类的不带参数的构造方法删除，或者把该构造方法的访问权限设置为private、默认或protected级别，会抛出 java.io.InvalidException: no valid constructor异常。

## 可序列化类的不同版本的序列化兼容性

凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：

private static final long serialVersionUID; 

以上serialVersionUID的取值是Java运行时环境根据类的内部细节自动生成的。如果对类的源代码作了修改，再重新编译，新生成的类文件的serialVersionUID的取值有可能也会发生变化。 

类的serialVersionUID的默认值完全依赖于Java编译器的实现，对于同一个类，用不同的Java编译器编译，有可能会导致不同的 serialVersionUID，也有可能相同。为了提高哦啊serialVersionUID的独立性和确定性，强烈建议在一个可序列化类中显示的定义serialVersionUID，为它赋予明确的值。

显式地定义serialVersionUID有两种用途： 在某些场合，希望类的不同版本对序列化兼容，因此需要确保类的不同版本具有相同的serialVersionUID；在某些场合，不希望类的不同版本对序列化兼容，因此需要确保类的不同版本具有不同的serialVersionUID。

# java中static{}语句块详解

原文地址：http://blog.csdn.net/lubiaopan/article/details/4802430

static{}(即static块)，会在类被加载的时候执行且仅会被执行一次，一般用来初始化静态变量和调用静态方法，下面我们详细的讨论一下该语句块的特性及应用。

## 程序的一次执行过程中，static{}语句块中的内容只执行一次

看下面的示例:

class Test{

        public static int X=100;

		public final static int Y;=200

		public Test(){

		System.out.println("Test构造函数执行");

	}

	static{

		System.out.println("static语句块执行");

	}

	public static void display(){

		System.out.println("静态方法被执行");

	}

	public void display_1(){

		System.out.println("实例方法被执行");

	}

}

public class StaticBlockTest{

	public static void main(String args[]){

		try{

		        Class.forName("Test");   

    		    Class.forName("Test"); 

		} catch(ClassNotFoundException e) {

			e.printStackTrace();

		}

		  

	}	

}

结果：你会发现虽然执行了两条Class.forName("Test")语句，但是，只输出了一条"静态方法被执行"语句；其实第二条Class.forName()语句已经无效了，因为在虚拟机的生命周期中一个类只被加载一次；又因为static{}是伴随类加载执行的，所以，不管你new多少次对象实例，static{}都只执行一次。

## static{}语句块执行的时机(其实就是附录中类加载的时机)

上面说到static{}会在类被加载的时候执行，我们必须准确理解类加载的准确含义，含义如下:

1、用Class.forName()显示加载的时候，如上面的示例一;

2、实例化一个类的时候，如将main()函数的内容改为:Test t=new Test();//这种形式其实和1相比，原理是相同的，都是显示的加载这个类，读者可以验证Test t=new Test();和Test t=(Test)Class.forName().newInstance();这两条语句效果相同。

3、调用类的静态方法的时候，如将main()函数的内容改为:Test.display();

4、调用类的静态变量的时候，如将main()函数的内容改为:System.out.println(Test.X);

总体来说就这四种情况，但是我们特别需要注意一下两点:

1、调用类的静态常量的时候，是不会加载类的，即不会执行static{}语句块，读者可以自己验证一下(将main()函数的内容改为System.out.println(Test.Y);)，你会发现程序只输出了一个200；(这是java虚拟机的规定，当访问类的静态常量时，如果编译器可以计算出常量的值，则不会加载类，否则会加载类)

2、用Class.forName()形式的时候，我们也可以自己设定要不要加载类，如将Class.forName("Test")改为 Class.forName("Test",false,StaticBlockTest.class.getClassLoader())，你会发现程序什么都没有输出，即Test没有被加载，static{}没有被执行。

## static{}语句块的执行次序

 1、当一个类中有多个static{}的时候，按照static{}的定义顺序，从前往后执行；

2、先执行完static{}语句块的内容，才会执行调用语句；

示例二

public class TestStatic{

     static{

         System.out.println(1);

     }

     static {

         System.out.println(2);

     }

     static {

         System.out.println(3);

     }

     public static void main(String args[]){

         System.out.println(5);

     }

     static {

         System.out.println(4);

     }

 }

结果:程序会输出1，2，3，4，5

3、如果静态变量在定义的时候就赋给了初值(如 static int X=100)，那么赋值操作也是在类加载的时候完成的，并且当一个类中既有static{}又有static变量的时候，同样遵循“先定义先执行”的原则；

示例三

 class Test{

  public static int X=300;

  static{

   System.out.println(X);

   X=200;

   System.out.println(X);

  }

 }

public class StaticBlockTest{

  public static void main(String args[]){

   System.out.println(Test.X);

  }

 }

结果:程序会依次输出300，200，200，先执行完X=300，再执行static{}语句块。

## static{}语句块应用

1、JDBC中的应用

熟悉JDBC的读者应该知道，java中有一个DriverManager类，用于管理各种数据库驱动程序、建立新的数据库连接。DriverManager类包含一些列Drivers类，这些Drivers类必须通过调用DriverManager的registerDriver()方法来对自己进行注册，那么注册是什么时候发生的呢？下面会给出答案:

所有Drivers类都必须包含有一个静态方法，利用这个静态方法可以创建该类的实例，然后在加载该实例时向DriverManage类进行注册。我们经常用Class.forName()对驱动程序进行加载，那么注册就发生在这条语句的执行过程中，前面说的Drivers的静态方法是放在static{}中的，当对驱动程序进行加载的时候，会执行该static{}，便完成了注册。

 2、hibernate中的应用

hibernate中的SessionFactory是一个重量级的类，创建该类的对象实例会耗费比较多的系统资源，如果每次需要时都创建一个该类的实例，显然会降低程序的执行效率，所以经常将对该类的实例化放在一个static{}中，只需第一次调用时执行，提高程序的执行效率，如下:

static {

      try {

    configuration.configure(configFile);

    sessionFactory = configuration.buildSessionFactory();

   } catch (Exception e) {

    System.err.println("%%%% Error Creating SessionFactory %%%%");

    e.printStackTrace();

   }

     }

## 附录

类加载:Java命令的作用是启动虚拟机，虚拟机通过输入流，从磁盘上将字节码文件(.class文件)中的内容读入虚拟机，并保存起来的过程就是类加载。

类加载特性 : 在虚拟机的生命周期中一个类只被加载一次。

类加载的原则：延迟加载，能少加载就少加载，因为虚拟机的空间是有限的。      *	类加载的时机：

1）第一次创建对象要加载类.

2）调用静态方法时要加载类,访问静态属性时会加载类。

3）加载子类时必定会先加载父类。

4）创建对象引用不加载类.

5）子类调用父类的静态方法时

6）          (1)当子类没有覆盖父类的静态方法时，只加载父类，不加载子类

7）          (2)当子类有覆盖父类的静态方法时，既加载父类，又加载子类

8）访问静态常量，如果编译器可以计算出常量的值，则不会加载类,例如:public static final int a =123;否则会加载类,例如:public static final int a = math.PI。

# finally和return

这是一道Java面试题：try { }里有一个return语句，那么紧跟在这个try后的finally {}里的code会不会被执行，什么时候被执行，在return前还是后?(如果try后面有个catch块，里面有return语句，那么finally语句会不会执行？)

finally语句块的作用就是为了保证无论出现什么情况，一定要执行的，那么finally里的code肯定会执行，并且是在return前执行。（只要语句执行了，肯定是在return前执行的。 finally中也可以有return，并且会覆盖其他的return）

根据java规范：在try-catch-finally中，如果try-finally或者catch-finally中都有return，则两个return语句都执行并且最终返回到调用者那里的是finally中return的值；而如果finally中没有return，则理所当然的返回的是try或者catch中return的值，但是finally中的代码是必须要执行的，方法在return的时候并不是把它所拥有的那个值给返回了，而是复制一份返回！因此，对于基本类型的数据，在finally中改变return的值对返回值没有任何影响，而对于引用类型的数据，就有影响。

（JAVA中基本类型变量存储在___中，引用类型的对象存储在____中，对象的引用地址存储在____中。

A. 堆   B. 栈   C. 寄存器  D. 静态存储区

BBA

基本类型和对象的引用都放在栈中，new出的对象和数组放在堆中

）

public class FinallyTest 

	{

		public static void main(String[] args) {

			 

			System.out.println("x的值是"+new FinallyTest().test());;

		}



		@SuppressWarnings("finally")

		static int test()

		{

			int x = 1;

			try

			{

				//x++;

				return x;

			}

			finally

			{

				++x;

				System.out.println("x的值当前值是" +x);

				//return x;

			}

		}

	}

执行结果：

x的值当前值是2

x的值是1

若finally中包含return语句

public class FinallyTest 

	{

		public static void main(String[] args) {

			 

			System.out.println("x的值是"+new FinallyTest().test());;

		}



		@SuppressWarnings("finally")

		static int test()

		{

			int x = 1;

			try

			{

				//x++;

				return x;

			}

			finally

			{

				++x;

System.out.println("x的值当前值是" +x);

				return x;

			}

		}

	}

执行结果是：

x的值当前值是2

x的值是2

若引用类型的数据，就有影响，

public class FinallyTest4 {



	public static void main(String[] args) {

		System.out.print("k的最终返回值是： "+tt());

	}

	public static StringBuffer tt() {

	StringBuffer k = new StringBuffer();  

	try {  

	k.append(2);  

		return k;  

	} catch(Exception e){  

		k.append(3);  

		return k;  

	} finally {  

		k.append(5);   

	}  

	}

}

执行结果是：的最终返回值是： 25

2. Java中的return语句总是和方法有密切关系，return语句总是用在方法中，有两个作用，一个是返回方法指定类型的值（这个值总是确定的），一个是结束方法的执行（仅仅一个return语句）。

return结束当前方法,后面语句除了finally语句块都不会执行

break跳出当前语句块,循环则跳出当前循环,也可在多重循环嵌套时跳出指定循环层

System.exit(0)表示关闭虚拟机,即使是finally语句块也不会执行

# java存储数据的地方以及九种基本类型 

寄存器（register）：这是最快的存储区——处理器内部。但是寄存器数量及其有限，所以寄存器由编译器根据需求进行分配，你不能直接控制，也不能在程序中感觉到寄存器存在的任何迹象。

堆栈（stack）：位于通用的RAM中，但通过它的“堆栈指针”可以从处理器哪里获得直接支持。堆栈指针若向下移动，则分配新的内存；若向上移动，则释放那些内存。这是一种快速有效的分配存储方法，仅次于寄存器。创建程序时，Java编译器必须知道存储在堆栈内所有数据的确切大小和生命周期。因为它必须生产相应的代码，以便上下移动堆栈指针。这一约束限制了程序的灵活性，所以虽然某些Java数据存储于堆栈中——特别是对象引用，但是Java对象并不存储于其中。

堆（heap）：一种通用性的内存池（也在RAM区），用于存放所有的Java对象。堆不同于堆栈的好处是：编译器不需要知道要从堆里分配多少存储区域，也不必知道存储的数据在堆里存活多长时间。因此，在堆里分配存储有很大的灵活性。当需要创建一个对象时，只需要new下。执行这行代码时，会自动在堆里进行存储分配。当然，为这种灵活性必须付出相应的代价。用堆进行存储分配比用堆栈进行存储需要更多的时间。

静态存储（static storage）：这里的“静态”是指“在固定的位置”（虽然也在RAM）。静态存储里存放程序运行时一直存在的数据。可以用关键字static来标识一个对象的特定元素是静态的，但Java对象本身从来不会存放在静态存储空间里。

常量存储（constant storage）：常量值通常直接存放在程序代码内部，这样做是安全的，因为他们永远不会被改变。有时，在嵌入式系统中，常量本身会和其它部分隔离开，所以在这种情况下，可以选择将其存放在ROM中。

非RAM存储（non-RAM storage）：如果数据完全存活于程序外，那么它可以不受程序的任何控制，在程序没有运行时也可以存在。其中两个最基本的例子就是“流对象”（stream object）和“持久化对象”（persistent object）。

特例：基本类型(primitive type)：不用new来创建变量，而是创建一个并非是“引用”的“自动”变量。这个变量拥有它的“值”，并置于堆栈中，因此更加高效。要确定每种基本类型所占存储空间的大小。

基本类型 大小 最小值   最大值   包装器类型

boolean   -   -    -   Boolean

char 16bit Unicode 0 Unicode 2(16)-1 Character

byte 8b -128   +127   Byte

short 16b -2(15)   2(15)-1   Short

int 32b -2(31)   2(31)-1   Integer

long 64b -2(63)   2(63)-1   Long

float 32bit IEEE754   IEEE754   Float

double 64b IEEE754   IEEE754   Double

void   - -    -   Void

# 抽象方法不能是static或native或synchroniz

1、abstract是抽象的，指的是方法只有声明而没有实现，他的实现要放入声明该类的子类中实现。

2、static是静态的，是一种属于类而不属于对象的方法或者属性，而我们知道，类其实也是一个对象，他是在class文件加载到虚拟机以后就会产生的对象，通常来说它是单例的，就是整个虚拟机中只有一个这样的类对象（当然，如果用新的类加载器也会生成新的类的对象）。 

3、synchronized 是同步，是一种相对线程的锁。

4、native 本地方法，这种方法和抽象方法及其类似，它也只有方法声明，没有方法实现，但是它与抽象方法不同的是，它把具体实现移交给了本地系统的函数库，而没有通过虚拟机，可以说是java与其它语言通讯的一种机制。

5、那么我们就来谈谈这些关键字为什么不能和abstract混用。

首先abstract与static，其实一看他们的作用和属性就很容易辨别，abstract是没有实现的，而static一定要有实现，因为 abstract的类不能生产对象，但是static是属于类，而类已经是一个存在的对象，这两个关键字在这上面有一个关键的矛盾点。

synchronized 是同步，然而同步是需要有具体操作才能同步的，如果像abstract只有方法声明，那同步一些什么东西就会成为一个问题了，当然抽象方法在被子类继承以后，可以添加同步。

native，这个东西本身就和abstract冲突，他们都是方法的声明，只是一个吧方法实现移交给子类，另一个是移交给本地操作系统。如果同时出现，就相当于即把实现移交给子类，又把实现移交给本地操作系统，那到底谁来实现具体方法呢！

# final、finally和finalize的区别

## final

它可以用于以下四个地方： 定义变量，包括静态的和非静态的；定义方法的参数；定义方法；定义类。 

我们依次来回顾一下每种情况下final的作用。首先来看第一种情况，如果final修饰的是一个基本类型，就表示这个变量被赋予的值是不可变的，即它是个常量；如果final修饰的是一个对象，就表示这个变量被赋予的引用是不可变的，这里需要提醒大家注意的是，不可改变的只是这个变量所保存的引用，并不是这个引用所指向的对象。在第二种情况下，final的含义与第一种情况相同。实际上对于前两种情况，有一种更贴切的表述final的含义的描述，那就是，如果一个变量或方法参数被final修饰，就表示它只能被赋值一次，但是JAVA虚拟机为变量设定的默认值不记作一次赋值。 被final修饰的变量必须被初始化。初始化的方式有以下几种： 在定义的时候初始化；final变量可以在初始化块中初始化，不可以在静态初始化块中初始化；静态final变量可以在静态初始化块中初始化，不可以在初始化块中初始化；final变量还可以在类的构造器中初始化，但是静态final变量不可以。 

通过下面的代码可以验证以上的观点： 



public class FinalTest {   

    // 在定义时初始化   

    public final int A = 10;   

  

    public final int B;   

    // 在初始化块中初始化   

    {   

        B = 20;   

    }   

  

    // 非静态final变量不能在静态初始化块中初始化   

    // public final int C;   

    // static {   

    // C = 30;   

    // }   

  

    // 静态常量，在定义时初始化   

    public static final int STATIC_D = 40;   

  

    public static final int STATIC_E;   

    // 静态常量，在静态初始化块中初始化   

    static {   

        STATIC_E = 50;   

    }   

  

    // 静态变量不能在初始化块中初始化   

    // public static final int STATIC_F;   

    // {   

    // STATIC_F = 60;   

    // }   

  

    public final int G;   

  

    // 静态final变量不可以在构造器中初始化   

    // public static final int STATIC_H;   

  

    // 在构造器中初始化   

    public FinalTest() {   

        G = 70;   

        // 静态final变量不可以在构造器中初始化   

        // STATIC_H = 80;   

  

        // 给final的变量第二次赋值时，编译会报错   

        // A = 99;   

        // STATIC_D = 99;   

    }   

  

    // final变量未被初始化，编译时就会报错   

    // public final int I;   

  

    // 静态final变量未被初始化，编译时就会报错   

    // public static final int STATIC_J;   

}  

我们运行上面的代码之后出了可以发现final变量（常量）和静态final变量（静态常量）未被初始化时，编译会报错。 用final修饰的变量（常量）比非final的变量（普通变量）拥有更高的效率，因此我们在实际编程中应该尽可能多的用常量来代替普通变量，这也是一个很好的编程习惯。 

当final用来定义一个方法时，会有什么效果呢？正如大家所知，它表示这个方法不可以被子类重写，但是它这不影响它被子类继承。我们写段代码来验证一下：

class ParentClass {   

    public final void TestFinal() {   

        System.out.println("父类--这是一个final方法");   

    }   

}   

  

public class SubClass extends ParentClass {   

    /**  

     * 子类无法重写（override）父类的final方法，否则编译时会报错  

     */  

    // public void TestFinal() {   

    // System.out.println("子类--重写final方法");   

    // }   

       

    public static void main(String[] args) {   

        SubClass sc = new SubClass();   

        sc.TestFinal();   

    }   

}  

这里需要特殊说明的是，具有private访问权限的方法也可以增加final修饰，但是由于子类无法继承private方法，因此也无法重写它。编译器在处理private方法时，是按照final方法来对待的，这样可以提高该方法被调用时的效率。不过子类仍然可以定义同父类中的private方法具有同样结构的方法，但是这并不会产生重写的效果，而且它们之间也不存在必然联系。

最后我们再来回顾一下final用于类的情况。这个大家应该也很熟悉了，因为我们最常用的String类就是final的。由于final类不允许被继承，编译器在处理时把它的所有方法都当作final的，因此final类比普通类拥有更高的效率。final的类的所有方法都不能被重写，但这并不表示final的类的属性（变量）值也是不可改变的，要想做到final类的属性值不可改变，必须给它增加final修饰，请看下面的例子：



public final class FinalTest {   

    int i = 10;   

  

    public static void main(String[] args) {   

        FinalTest ft = new FinalTest();   

        ft.i = 99;   

        System.out.println(ft.i);   

    }   

}  

public final class FinalTest {



	int i = 10;



	public static void main(String[] args) {

		FinalTest ft = new FinalTest();

		ft.i = 99;

		System.out.println(ft.i);

	}

}

	运行上面的代码试试看，结果是99，而不是初始化时的10。

## finally

这个就比较简单了，它只能用在try/catch语句中，并且附带着一个语句块，表示这段语句最终总是被执行。请看下面的代码： 

public final class FinallyTest {   

    public static void main(String[] args) {   

        try {   

            throw new NullPointerException();   

        } catch (NullPointerException e) {   

            System.out.println("程序抛出了异常");   

        } finally {   

            System.out.println("执行了finally语句块");   

        }   

    }   

}  



	运行结果说明了finally的作用： 程序抛出了异常并且执行了finally语句块。请大家注意，捕获程序抛出的异常之后，既不加处理，也不继续向上抛出异常，并不是良好的编程习惯，它掩盖了程序执行中发生的错误，这里只是方便演示，请不要学习。 那么有没有一种情况使finally语句块得不到执行呢？大家可能想到了return、continue、break这三个可以打乱代码顺序执行语句的规律。那我们就来试试看，这三个语句是否能影响finally语句块的执行： 

public final class FinallyTest {   

    // 测试return语句   

    public ReturnClass testReturn() {   

        try {   

            return new ReturnClass();   

        } catch (Exception e) {   

            e.printStackTrace();   

        } finally {   

            System.out.println("执行了finally语句");   

        }   

        return null;   

    }   

  

    // 测试continue语句   

    public void testContinue() {   

        for (int i = 0; i < 3; i++) {   

            try {   

                System.out.println(i);   

                if (i == 1) {   

                    continue;   

                }   

            } catch (Exception e) {   

                e.printStackTrace();   

            } finally {   

                System.out.println("执行了finally语句");   

            }   

        }   

    }   

  

    // 测试break语句   

    public void testBreak() {   

        for (int i = 0; i < 3; i++) {   

            try {   

                System.out.println(i);   

                if (i == 1) {   

                    break;   

                }   

            } catch (Exception e) {   

                e.printStackTrace();   

            } finally {   

                System.out.println("执行了finally语句");   

            }   

        }   

    }   

  

    public static void main(String[] args) {   

        FinallyTest ft = new FinallyTest();   

        // 测试return语句   

        ft.testReturn();   

        System.out.println();   

        // 测试continue语句   

        ft.testContinue();   

        System.out.println();   

        // 测试break语句   

        ft.testBreak();   

    }   

}   

  

class ReturnClass {   

    public ReturnClass() {   

        System.out.println("执行了return语句");   

    }   

}  

public final class FinallyTest {



	// 测试return语句

	public ReturnClass testReturn() {

		try {

			return new ReturnClass();

		} catch (Exception e) {

			e.printStackTrace();

		} finally {

			System.out.println("执行了finally语句");

		}

		return null;

	}



	// 测试continue语句

	public void testContinue() {

		for (int i = 0; i < 3; i++) {

			try {

				System.out.println(i);

				if (i == 1) {

					continue;

				}

			} catch (Exception e) {

				e.printStackTrace();

			} finally {

				System.out.println("执行了finally语句");

			}

		}

	}



	// 测试break语句

	public void testBreak() {

		for (int i = 0; i < 3; i++) {

			try {

				System.out.println(i);

				if (i == 1) {

					break;

				}

			} catch (Exception e) {

				e.printStackTrace();

			} finally {

				System.out.println("执行了finally语句");

			}

		}

	}



	public static void main(String[] args) {

		FinallyTest ft = new FinallyTest();

		// 测试return语句

		ft.testReturn();

		System.out.println();

		// 测试continue语句

		ft.testContinue();

		System.out.println();

		// 测试break语句

		ft.testBreak();

	}

}



class ReturnClass {

	public ReturnClass() {

		System.out.println("执行了return语句");

	}

}



上面这段代码的运行结果如下： 

执行了return语句 

执行了finally语句 



0 

执行了finally语句 

1 

执行了finally语句 

2 

执行了finally语句 



0 

执行了finally语句 

1 

执行了finally语句

很明显，return、continue和break都没能阻止finally语句块的执行。从输出的结果来看，return语句似乎在finally语句块之前执行了，事实真的如此吗？我们来想想看，return语句的作用是什么呢？是退出当前的方法，并将值或对象返回。如果finally语句块是在return语句之后执行的，那么return语句被执行后就已经退出当前方法了，finally语句块又如何能被执行呢？因此，正确的执行顺序应该是这样的：编译器在编译return new ReturnClass();时，将它分成了两个步骤，new ReturnClass()和return，前一个创建对象的语句是在finally语句块之前被执行的，而后一个return语句是在finally语句块之后执行的，也就是说finally语句块是在程序退出方法之前被执行的。同样，finally语句块是在循环被跳过（continue）和中断（break）之前被执行的。

## finalize

最后，我们再来看看finalize，它是一个方法，属于java.lang.Object类，它的定义如下：

protected void finalize() throws Throwable { }  

	众所周知，finalize()方法是GC（garbage collector）运行机制的一部分，关于GC的知识我们将在后续的章节中来回顾。 在此我们只说说finalize()方法的作用是什么呢？ finalize()方法是在GC清理它所从属的对象时被调用的，如果执行它的过程中抛出了无法捕获的异常（uncaught exception），GC将终止对改对象的清理，并且该异常会被忽略；直到下一次GC开始清理这个对象时，它的finalize()会被再次调用。 请看下面的示例：

 

public final class FinallyTest {   

    // 重写finalize()方法  

    protected void finalize() throws Throwable {   

        System.out.println("执行了finalize()方法");   

    }   

  

    public static void main(String[] args) {   

        FinallyTest ft = new FinallyTest();   

        ft = null; 

        System.gc();   

    }   

}  



	运行结果： 执行了finalize()方法 

程序调用了java.lang.System类的gc()方法，引起GC的执行，GC在清理ft对象时调用了它的finalize()方法，因此才有了上面的输出结果。调用System.gc()等同于调用下面这行代码： Runtime.getRuntime().gc();  

调用它们的作用只是建议垃圾收集器（GC）启动，清理无用的对象释放内存空间，但是GC的启动并不是一定的，这由JAVA虚拟机来决定。直到JAVA虚拟机停止运行，有些对象的finalize()可能都没有被运行过，那么怎样保证所有对象的这个方法在JAVA虚拟机停止运行之前一定被调用呢？答案是我们可以调用System类的另一个方法：

public static void runFinalizersOnExit(boolean value) {   

    //other code   

}  



	给这个方法传入true就可以保证对象的finalize()方法在JAVA虚拟机停止运行前一定被运行了，不过遗憾的是这个方法是不安全的，它会导致有用的对象finalize()被误调用，因此已经不被赞成使用了。 由于finalize()属于Object类，因此所有类都有这个方法，Object的任意子类都可以重写（override）该方法，在其中释放系统资源或者做其它的清理工作，如关闭输入输出流。

# 在try块中可以抛出异常吗？

Java通过面向对象的方法进行异常处理，把各种不同的异常进行分类，并提供了良好的接口。在Java中，每个异常都是一个对象，它是Throwable类或其它子类的实例。当一个方法出现异常后便抛出一个异常对象，该对象中包含有异常信息，调用这个对象的方法可以捕获到这个异常并进行处理。Java的异常处理是通过5个关键词来实现的：try、catch、throw、throws和finally。一般情况下是用try来执行一段程序，如果出现异常，系统会抛出（throws）一个异常，这时候你可以通过它的类型来捕捉（catch）它，或最后（finally）由缺省处理器来处理。用try来指定一块预防所有”异常”的程序。紧跟在try程序后面，应包含一个catch子句来指定你想要捕捉的”异常”的类型。

throw语句用来明确地抛出一个”异常”。throws用来标明一个成员函数可能抛出的各种”异常”。Finally为确保一段代码不管发生什么”异常”都被执行一段代码。

可以在一个成员函数调用的外面写一个try语句，在这个成员函数内部写另一个try语句保护其他代码。每当遇到一个try语句，”异常”的框架就放到堆栈上面，直到所有的try语句都完成。如果下一级的try语句没有对某种”异常”进行处理，堆栈就会展开，直到遇到有处理这种”异常”的try语句。

# assert断言结构

assert是在J2SE1.4中引入的新特性，assertion就是在代码中包括的布尔型状态，程序员认为这个状态是true。一般来说assert在开发的时候是检查程序的安全性的，在发布的时候通常都不使用assert。在1.4中添加了assert关键字和java.lang.AssertError类的支持。首先，我们有必要从一个例子说起：

public class AssertTest {

	public static void main(String[] args) {

		AssertTest at = new AssertTest();

		at.assertMe(true);

		at.assertMe(false);

	}



	private void assertMe(boolean boo) {

		assert boo ? true : false;

		System.out.println("true condition");

	}

}

要想让assert部分运行的话，要使用java -ea xxx来运行，否则包含assert得行会被忽略。	下面我们运行

javac AssertTest.java

java -ea AssertTest

看看结果的输出是：

true condition

Exception in thread "main" java.lang.AssertionError

at AssertTest.assertMe(AssertTest.java:13)

at AssertTest.main(AssertTest.java:7)

	当我们运行at.assertMe(true)得时候，由于assert boo?true:false相当于 assert true;因此没有任何问题，程序往下执行打印出true condition，但是执行at.assertMe(false)的时候相当于assert false，这个时候解释器就会抛出AssertionError了，程序就终止了。大家必须清楚AssertionError是继承自Error的，因此你可以不再程序中catch它的，当然你也可以在程序中catch它然后程序可以继续执行。例如：

public class AssertTest {

	public static void main(String[] args) {

		AssertTest at = new AssertTest();

		try {

			at.assertMe(true);

			at.assertMe(false);

		} catch (AssertionError ae) {

			System.out.println("AsseriontError catched");

		}

		System.out.println("go on");

	}



	private void assertMe(boolean boo) {

		assert boo ? true : false;

		System.out.println("true condition");

	}

}

	assert还有另外一种表达的方式，就是assert exp1:exp2;其中exp1是个boolean返回值得表达式，而exp2可以是原始的数据类型或者对象，例如：

boolean boo = true;

String str = null;

assert boo = false：str="error";

	我们刚开始讲得assert exp1得形式，当exp1是false得时候，AssertionError得默认构造器会被调用，但是assert exp1:exp2这样的形式，当exp1为true的时候后面exp2被或略，如果false的话，后面的表达式的结果会被计算出来并作为AssertionError得构造器参数。看下面的例子：

public class AssertTest {

	public static void main(String[] args) {

		AssertTest at = new AssertTest();

		at.assertMe(true);

		at.assertMe(false);

	}



	private void assertMe(boolean boo) {

		String s = null;

		assert boo ? true : false : s = "hello world";

		System.out.println("true condition");

	}

}

运行的时候会得到这样的结果：

true condition

Exception in thread "main" java.lang.AssertionError: hello world

at AssertTest.assertMe(AssertTest.java:14)

at AssertTest.main(AssertTest.java:7)

	Assert最好不要滥用，原因是assert并不一定都是enable的，下面两种情况就不应该用assert。

不要在public的方法里面检查参数是不是为null之类的操作，例如：

public int get(String s)

	{

		assert s != null;

	}

	如果需要检查也最好通过if s = null 抛出NullPointerException来检查。

	不要用assert来检查方法操作的返回值来判断方法操作的结果，例如：

assert list.removeAll();这样看起来好像没有问题 但是想想如果assert 被disable呢，那样他就不会被执行了 所以removeAll()操作就没有被执行，可以这样代替：

boolean boo = list.removeAl();

assert boo; 

## eclipse 中怎样设置 参数来 使用 Asset

依次进入eclipse的菜单项Window -> Preferences -> Java -> Compiler -> Compliance and Classfiles，将Compiler Compliance Level to 5.0.    断言在java的JDK1.4版本中添加进来，这个设置告诉编译器识别和允许断言语句，但是还没有开启断言。接下来，进入菜单项Window -> Preferences -> Java -> Compiler -> Compliance and Classfiles，并且设置：Compiler Compliance Level: 5.0    Use default compliance settings unchecked

       Generated .class files compatibility: 5.0

       Source compatibility: 5.0

    Disallow identifiers called 'assert': Error

    Compiler Compliance Level to 5.0选择开启或关闭Assert功能由于我们可以选择开启assertion功能，或者不开启，另外我们还可以开启一部分类或包的assertion功能，所以运行选项变得有些复杂。通过这些选项，我们可以过滤所有我们不关心的类，只选择我们关心的类或包来观察。下面介绍两类参数：

参数 -esa 和 -dsa：

它们含义为开启(关闭)系统类的assertion功能。由于新版本的Java的系统类中，也使了assertion语句，因此如果用户需要观察它们的运行情况，就需要打开系统类的assertion功能，我们可使用-esa参数打开，使用 -dsa参数关闭。

-esa和-dsa的全名为-enablesystemassertions和-disenablesystemassertions，全名和缩写名有同样的功能。

参数 -ea和-ea：

它们含义为开启(关闭)用户类的assertion功能：通过这个参数，用户可以打开某些类或包的assertion功能，同样用户也可以关闭某些类和包的assertion功能。打开assertion功能参数为-ea；如果不带任何参数，表示打开所有用户类；如果带有包名称或者类名称，表示打开这些类或包；如果包名称后面跟有三个点，代表这个包及其子包；如果只有三个点，代表无名包。关闭assertion功能参数为-da，使用方法与-ea类似。

-ea和-da的全名为-enableassertions和-disenableassertions，全名和缩写名有同样的功能。

下面表示了参数及其含义，并有例子说明如何使用。

参数 例子 说明

-ea java -ea 打开所有用户类的assertion

-da java -da 关闭所有用户类的assertion

-ea:<classname> java -ea:MyClass1 打开MyClass1的assertion

-da:<classname> java -da: MyClass1 关闭MyClass1的assertion

-ea:<packagename> java -ea:pkg1 打开pkg1包的assertion

-da:<packagename> java -da:pkg1 关闭pkg1包的assertion

-ea:... java -ea:... 打开缺省包(无名包)的assertion

-da:... java -da:... 关闭缺省包(无名包)的assertion

-ea:<packagename>... java -ea:pkg1... 打开pkg1包和其子包的assertion

-da:<packagename>... java -da:pkg1... 关闭pkg1包和其子包的assertion

-esa java -esa 打开系统类的assertion

-dsa java -dsa 关闭系统类的assertion

	综合使用 java -dsa:MyClass1:pkg1 关闭MyClass1和pkg1包的assertion，其中...代表，此包和其子包的含义。例如我们有两个包为pkg1和pkg1.subpkg。那么pkg1...就代表pkg1和pkg1.subpkg两个包。

另外，Java为了让程序也能够动态开启和关闭某些类和包的assertion功能，Java修该了Class和ClassLoader的实现，增加了几个用于操作assert的API。下面简单说明一下几个API的作用。

	ClassLoader类中的几个相关的API:

　　setDefaultAssertionStatus:用于开启/关闭assertion功能

　　setPackageAssertionStatus:用于开启/关闭某些包的assertion功能

　　setClassAssertionStatus: 用于开启/关闭某些类的assertion功能

　　clearAssertionStatus：用于关闭assertion功能

	最后在Run -> Run... -> Arguments菜单项的VM arguments区域，加上断言开启的标志-enableassertions 或者-ea 就可以了。

## assertion与继承

在本节，我们将考虑assertion与继承的关系，研究assert是如何定位的。如果开启一个子类的assertion，那么它的父类的assertion是否执行？下面的例子将显示如果一个assert语句在父类，而当它的子类调用它时，该assert为false。我们看看在不同的情况下，该assertion是否被处理。

class Base {

	public void baseMethod() {

		assert false : "Assertion failed:This is base ";// 总是assertion失败

		System.out.println("Base Method");

	}

}



class Derived extends Base {

	public void derivedMethod() {

		assert false : "Assertion failed:This is derive";// 总是assertion失败

		System.out.println("Derived Method");

	}



	public static void main(String[] args) {

		try {

			Derived derived = new Derived();

			derived.baseMethod();

			derived.derivedMethod();

		} catch (AssertionError ae) {

			System.out.println(ae);

		}

	}

}

运行命令 含义 结果

Java Derived   不启用assertion   Base Method   Derived Method

Java -ea Derived   开启所有assertion   Java.lang.AssertionError:Assertion Failed:This is base

Java -da Derived   关闭所有assertion   Base Method   Derived Method

Java -ea:Base Derived   仅打开Base的assertion   Java.lang.AssertionError:Assertion Failed:This is base

Java -ea:Derived Derived   仅打开Derived的assertion    Base Method

Java.lang.AssertionError:Assertion Failed:This is derived

	从这个例子我们可以看出，父类的assert语句将只有在父类的assert开启才起作用，如果仅仅开启子类的assert，父类的assert仍然不运行。例如，我们执行java -ea:Derived Derived的时候，Base类的assert语句并不执行。因此，我们可以认为，assert语句不具有继承功能。

assert的用法

# Java通过JNI调用C语言

Java通过JNI（Java Native Interface）调用本地方法，而本地方法是以库文件的形式存放的（在WINDOWS平台上是DLL文件形式，在UNIX机器上是SO文件形式）。通过调用本地的库文件的内部方法，使Java可以实现和本地机器的紧密联系，调用系统级的各接口方法。 简单介绍及应用如下：

## Java中所需要做的工作

public class testdll{

	static {

		System.loadLibrary("testdll"); //声明所调用的库名称

		}

	public native static int get();

	public native static void set(int i);

	public static void main(String[] args) {

		testdll test = new testdll();

		test.set(10);

		System.out.println(test.get());

		}

	}

在Java程序中，首先需要在类中声明所调用的库名称，在这里，库的扩展名字可以不用写出来，究竟是DLL还是SO，由系统自己判断。还需要对将要调用的方法做本地声明，关键字为native。并且只需要声明，而不需要具体实现。然后编译该Java程序文件，生成CLASS，再用JavaH命令，JNI就会生成C/C++的头文件。这个文件需要被C/C++程序调用来生成所需的库文件。

javah -classpath e:\temp\java\Test\src\ testdll

如果有包名，则应该使用javah -classpath e:\temp\java\Test\src\ packagename.testdll

## C/C++中所需要做的工作

　　对于已生成的.h头文件，C/C++所需要做的，就是把它的各个方法具体的实现。然后编译连接成库文件即可。再把库文件拷贝到Java程序的路径下面，就可以用Java调用C/C++所实现的功能了。接上例子。我们先看一下testdll.h文件的内容：

/* DO NOT EDIT THIS FILE - it is machine generated */

#include <jni.h>

/* Header for class testdll */



#ifndef _Included_testdll

#define _Included_testdll

#ifdef __cplusplus

extern "C" {

#endif

/*

 * Class:     testdll

 * Method:    get

 * Signature: ()I

 */

JNIEXPORT jint JNICALL Java_testdll_get

  (JNIEnv *, jclass);



/*

 * Class:     testdll

 * Method:    set

 * Signature: (I)V

 */

JNIEXPORT void JNICALL Java_testdll_set

  (JNIEnv *, jclass, jint);



#ifdef __cplusplus

}

#endif

#endif

　　在具体实现的时候，我们只关心两个函数原型 :

　　JNIEXPORT jint JNICALL Java_testdll_get (JNIEnv *, jclass);

　　JNIEXPORT jint JNICALL Java_testdll_get (JNIEnv *, jclass);

　　这里JNIEXPORT和JNICALL都是JNI的关键字，表示此函数是要被JNI调用的。而jint是以JNI为中介使Java的int类型与本地的int沟通的一种类型，我们可以视而不见，就当做int使用。函数的名称是Java_再加上Java程序的package路径再加函数名组成的。参数中，我们也只需要关心在Java程序中存在的参数，至于JNIEnv*和jclass我们一般没有必要去碰它。下面我们用testdll.cpp文件具体实现这两个函数：

　　public class testdll{

	static {

		System.loadLibrary("libtestdll");

		}

	public native static int get();

	public native static void set(int i);

	public static void main(String[] args) {

		testdll test = new testdll();

		test.set(10);

		System.out.println(test.get());

		}

	}

编译连接成库文件，本例是在Windows(VS2012)下做的，生成的是testdll.dll。(名称要与Java中需要调用的一致)，把testdll.dll拷贝到和test.class相同的目录下，Java testdll运行它，就可以观察到结果了。

# Java的内部类

在java语言中，有一种类叫做内部类(inner class)，也称为嵌入类(nested class)，它是定义在其他类的内部。内部类作为其外部类的一个成员，与其他成员一样，可以直接访问其外部类的数据和方法。只不过相比较外部类只有public和默认的修饰符不同，内部类作为一个成员，可以被任意修饰符修饰。编译器在编译时，内部类的名称为OuterClass$InnerClass.class 。

## 1、内部类访问数据变量

当在某些时候，内部类中定义的变量与外部类中变量名称相同时，如何确保正确地访问每一个变量呢？

1.1在main中直接从外部类调用内部类的方法

class Outer

{

    private int index = 10;

    class Inner 

    {

        private int index = 20;

        void print()

        {

            int index = 30;

            System.out.println(this); // the object created from the Inner

            System.out.println(Outer.this); // the object created from the Outer

            System.out.println(index); // output is 30

            System.out.println(this.index); // output is 20

            System.out.println(Outer.this.index); // output is 10

        }

    }



    void print() 

    {

        Inner inner = new Inner();//得到内部类的引用

        inner.print();

    }

}



class Test 

{

    public static void main(String[] args) 

    {

        Outer outer = new Outer();

        outer.print();

    }

}

在这里内部类Inner中关键字this指向内部类Inner的对象，如果要想指向外部类的对象，必须在this指针前加上外部类名称，表示this是指向外部类构造的实例，如Outer.this 。

1.2在main中显式返回内部类引用

class Outer 

{

    private int index = 10;

    class Inner 

    {

        private int index = 20;

        void print() 

        {

            int index = 30;

            System.out.println(index);

            System.out.println(this.index);

            System.out.println(Outer.this.index);

        }

    }



    Inner getInner() 

    {

        return new Inner();//返回一个内部类的引用

    }

}



class Test 

{

    public static void main(String[] args) 

    {

        Outer outer = new Outer();

        Outer.Inner inner = outer.getInner();

        inner.print();

    }

}

Inner是Outer的内部类，所以在类Test中必须用属性引用符来标识出内部类。

1.3当main方法在Outer类内部

class Outer 

{

        private int index = 10;

        class Inner 

        {

             private int index = 20;

             void print() 

             {

                  int index = 30;

                  System.out.println(index);

                  System.out.println(this.index);

                  System.out.println(Outer.this.index);

             }

        }



        Inner getInner() 

        {

             return new Inner();//返回一个内部类的引用

        }



        public static void main(String[] args) 

        {

             Outer outer = new Outer();

             Inner inner = outer.getInner(); // 注意此处变化

             inner.print();

        }

}

因为main方法在Outer内部，故可以直接引用，不需要属性引用符。

1.4在main方法中直接产生内部类对象

class Test 

{

        public static void main(String[] args) 

        {

             Outer outer = new Outer();

             Outer.Inner inner = outer.new Inner(); // 注意此处变化

             inner.print();

        }

}

在利用new构造方法构造一个外部类对象时，并没有连带着构造一个内部类对象，故需要访问内部类方法时，必须使用new操作符为这个外部类对象再构造一个内部类对象。

## 2、局部内部类

在方法中定义的内部类是局部内部类，它只能访问方法中的final类型的局部变量，因为用final定义的局部变量相当于是一个常量，延长了其生命周期，使得方法在消亡时，其内部类仍可以访问该变量。另外，它同样也可以引用定义在外部类的变量和方法。而且方法体中的局部内部类不允许有访问修饰符。

class Outer

{

        int num=10; 

        public void print(final int aArgs)

        {

             class Inner

             {

                 int num=20;

                 public Inner()

                 {

                     System.out.println("This is Inner.");//此句可看出它与匿名内部类用法的不同。

                 }



                 public void print()

                 {     

                     int num=30;

                     System.out.println(this); // the object created from the local Inner

                     System.out.println(num);

                     System.out.println(this.num);

                     System.out.println(Outer.this.num);

                     System.out.println(aArgs);

                 }

             }

             Inner inner=new Inner();//此句必须放在定义类Inner的后面

             inner.print();

        }



        public static void main(String[] args)

        {

             Outer outer=new Outer();

             outer.print(40);

        }

}

对于局部类的命名，不管是在一个方法中定义多个类还是在几个方法中分别定义类，其编译后命名是：OuterClass$1InnerClass.class

## 3、匿名内部类

匿名内部类作为一种特殊的内部类，除了具有普通内部类的特点，还有自己的一些独有特性：匿名内部类必须扩展一个基类或实现一个接口，但是不能有显式的extends和implements子句；匿名内部类必须实现父类以及接口中的所有抽象方法；匿名内部类总是使用父类的无参构造方法来创建实例。如果是实现了一个接口，则其构造方法是Object()；匿名内部类编译后的命名为：OuterClass$n.class，其中n是一个从1开始的整数，如果在一个类中定义了多个匿名内部类，则按照他们的出现顺序从1开始排号。

abstract class A

{

    abstract public void sayHello();

}



class Outer

{

    public static void main(String[] args)

    {

         new Outer().callInner(new A()

         {

               public void sayHello()

               {

                     System.out.println(this); // the object created from the anonymous Inner

                     System.out.println("Hello!");

               }

         });

    }



    public void callInner(A a)

    {

        a.sayHello();

    }

}

## 4、静态内部类

和非静态内部类相比，区别就在于静态内部类没有了指向外部类的引用。除此之外，在任何非静态内部类中，都不能有静态数据，静态方法或者又一个静态内部类（内部类的嵌套可以不止一层）。不过静态内部类中却可以拥有这一切。这也算是两者的第二个区别吧。一个静态的内部类,才可以声明一个static成员，静态内部类可以访问外围类的静态方法、成员（包括private static的成员）。静态内部类实例化的时候不必先实例化外围类，可以直接实例化内部类。而对于非静态内部类则必须先实例化其外部类，才能再实例化本身。

## 5．内部类的继承

当一个类继承自一个内部类时，缺省的构造器不可用。必须使用如下语法：

class WithInner

{

    class Inner

    {

        public void sayHello()

        {

            System.out.println("Hello.");

        }

    }

}



public class Test extends WithInner.Inner

{

    Test(WithInner wi)

    {

        wi.super();

    }

    public static void main(String[] args)

    {

        WithInner wi=new WithInner();

        Test test=new Test(wi);

        test.sayHello();

    }

} 

因为每一个内部类都有一个指向外部类的引用，在继承一个内部类，必须先创建一个外部类，通过这个外部类引用来调用其内部类的构造方法。如果继承的内部类是一个静态内部类，则就不需要这样，直接super()调用即可；

## 6、内部类的2种特殊用法

一个类从另一个类派生出来，又要实现一个接口。但在接口中定义的方法与父类中定义的方法的意义不同，则可以利用内部类来解决这个问题。

interface Machine

{

    void run();

}



class Person

{     

    void run()

    {

        System.out.println("run");

    }

}



class Robot extends Person

{

    private class MachineHeart implements Machine

    {

        public void run()

        {

            System.out.println("heart run");

        }

    }



    Machine getMachine()

    {

        return new MachineHeart();

    }

}



class Test

{

    public static void main(String[] args)

   {

        Robot robot = new Robot();

        Machine m = robot.getMachine();

        m.run();

        robot.run();

    }

}

在Robot类内部使用内部类MachineHeart来实现接口Machine的run方法。同时Robot类又继承了父类Person的run方法。如果不使用内部类MachineHeart而使Robot直接实现接口Machine，则该如何调用父类的run方法？

利用内部类可解决c++中多重继承所解决的问题

class A

{

    void fn1()

    {

        System.out.println("It' s fn1.");

    }

}



abstract class B

{

    abstract void fn2();

}



class C extends A

{

    B getB()

    {

        return new B() 

        {

            public void fn2()

            {

                System.out.println("It' s fn2.");

            }

        };

    }

}



class Test

{

    public static void main(String[] args)

    {

        C c = new C();

        c.fn1();

        c.getB().fn2();

    }

}

类C既要继承类A又要继承类B，则可将类B的定义放入类C内部，使之成为内部类。

一般情况下 当我们需要在某一情形下实现一个接口，而在另一情形下又不需要实现这个接口时，我们可以使用内部类来解决这一问题。让内部类来实现这个接口。另外一个很好的理由是java内部类加上接口可以有效地实现多重继承。

JAVA 内部类还有一个作用，那就是实现JAVA的多继承。JAVA本身是不允许多继承的，如果我们想一个类继承多个基类，就可以使用内部类。通过内部类分别继承一个基类，外部类创建内部类的对象，并使用内部类的方法，变相地实现了多继承。

# Java 内部类介绍

Java 内部类 分四种：成员内部类、局部内部类、静态内部类和匿名内部类。

## 成员内部类

即作为外部类的一个成员存在，与外部类的属性、方法并列。注意成员内部类中不能定义静态变量，但可以访问外部类的所有成员。

	成员内部类的优点：1、内部类作为外部类的成员，可以访问外部类的私有成员或属性,即使将外部类声明为private，对于其内部类还是可见的。2、用内部类定义在外部类中不可访问的属性。这样就在外部类中实现了比外部类的private还要小的访问权限。

注意：内部类是一个编译时的概念，一旦编译成功，就会成为完全不同的两类。对于一个名为outer的外部类和其内部定义的名为inner的内部类。编译完成后出现outer.class和outer$inner.class两类。

## 局部内部类

即在方法中定义的内部类，与局部变量类似，在局部内部类前不加修饰符public或private，其范围为定义它的代码块。

注意：局部内部类中不可定义静态变量，可以访问外部类的局部变量(即方法内的变量)，但是变量必须是final的；在类外不可直接生成局部内部类（保证局部内部类对外是不可见的）。要想使用局部内部类时需要生成对象，对象调用方法，在方法中才能调用其局部内部类。通过内部类和接口达到一个强制的弱耦合，用局部内部类来实现接口，并在方法中返回接口类型，使局部内部类不可见，屏蔽实现类的可见性。

## 静态内部类

静态内部类定义在类中，任何方法外，用static定义。注意，静态内部类中可以定义静态或者非静态的成员；生成（new）一个静态内部类不需要外部类成员，这是静态内部类和成员内部类的区别。静态内部类的对象可以直接生成：

Outer.Inner in=new Outer.Inner()；

而不需要通过生成外部类对象来生成。这样实际上使静态内部类成为了一个顶级类。静态内部类不可用private来进行定义，例如，对于两个类，拥有相同的方法，此时有一个robot类：class Robot extends People implement Machine：

abstract class People {

	abstract void run();

}



interface Machine {

	void run();

}



public class Robot extends People implements Machine {

	public void run() { // 无法同时实现People和Machine的方法

		System.out.println("A Robot is running!");

	}



	public static void main(String[] argv) {

		Robot robot = new Robot();

		robot.run();

	}

}

此时run()不可直接实现。当类与接口（或者是接口与接口）发生方法命名冲突的时候，必须使用内部类来实现。用接口不能完全地实现多继承，用接口配合内部类才能实现真正的多继承。

## 匿名内部类

匿名内部类是一种特殊的局部内部类，它是通过匿名类实现接口。IA被定义为接口。

IA I=new IA(){};

匿名内部类的特点：

1、一个类用于继承其他类或是实现接口，并不需要增加额外的方法，只是对继承方法的事先或是覆盖。

2、只是为了获得一个对象实例，不需要知道其实际类型。

3、类名没有意义，也就是不需要使用到。

注：一个匿名内部类一定是在new的后面，用其隐含实现一个接口或实现一个类，没有类名，根据多态，我们使用其父类名。因他是局部内部类，那么局部内部类的所有限制都对其生效。匿名内部类是唯一一种无构造方法类。大部分匿名内部类是用于接口回调用的。匿名内部类在编译的时候由系统自动起名Out$1.class。如果一个对象编译时的类型是接口，那么其运行的类型为实现这个接口的类。因匿名内部类无构造方法，所以其使用范围非常的有限。当需要多个对象时使用局部内部类，因此局部内部类的应用相对比较多。匿名内部类中不能定义构造方法。如果一个对象编译时的类型是接口，那么其运行的类型为实现这个接口的类。

## 内部类总结

首先，把内部类作为外部类的一个特殊的成员来看待，因此它有类成员的封闭等级：private ,protected,默认(friendly),public；它有类成员的修饰符:static,final,abstract

非静态内部类nested inner class,内部类隐含有一个外部类的指针this,因此，它可以访问外部类的一切资源（当然包括private）。外部类访问内部类的成员，先要取得内部类的对象,并且取决于内部类成员的封装等级；非静态内部类不能包含任何static成员.

4、静态内部类：static inner class,不再包含外部类的this指针，并且在外部类装载时初始化；静态内部类能包含static或非static成员；静态内部类只能访问外部类static成员；外部类访问静态内部类的成员，循一般类法规。对于static成员，用类名.成员即可访问，对于非static成员，只能用对象.成员进行访问。

5、对于方法中的内部类或块中内部类只能访问块中或方法中的final变量。

6、类成员有两种static , non-static，同样内部类也有这两种：non-static 内部类的实例，必须在外部类的方法中创建或通过外部类的实例来创建(OuterClassInstanceName.new innerClassName(ConstructorParameter)),并且可直接访问外部类的信息,外部类对象可通过OuterClassName.this来引用static 内部类的实例, 直接创建即可，没有对外部类实例的引用。内部类不管static还是non-static都有对外部类的引用；non-static 内部类不允许有static成员

7、方法中的内部类只允许访问方法中的final局部变量和方法的final参数列表，所以说方法中的内部类和内部类没什麽区别。但方法中的内部类不能在方法以外访问，方法中不可以有static内部类

8、匿名内部类如果继承自接口,必须实现指定接口的方法,且无参数 

9、匿名内部类如果继承自类,参数必须按父类的构造函数的参数传递

# WEB-INF目录与META-INF目录的作用

web应用结构

 /WEB-INF/web.xml

Web应用程序配置文件，描述了 servlet 和其他的应用组件配置及命名规则。

 /WEB-INF/classes/

包含了站点所有用的 class 文件，包括 servlet class 和非servlet class，他们不能包含在 .jar文件中。

 /WEB-INF/lib/

存放web应用需要的各种JAR文件，放置仅在这个应用中要求使用的jar文件,如数据库驱动jar文件。

 /WEB-INF/src/

  源码目录，按照包名结构放置各个java文件。

 /WEB-INF/database.properties

  数据库配置文件

 /WEB-INF/tags/

存放了自定义标签文件，该目录并不一定为 tags，可以根据自己的喜好和习惯为自己的标签文件库命名，当使用自定义的标签文件库名称时，在使用标签文件时就必须声明正确的标签文件库路径。例如：当自定义标签文件库名称为 simpleTags 时，在使用 simpleTags 目录下的标签文件时，就必须在 jsp 文件头声明为：<%@ taglibprefix="tags" tagdir="/WEB-INF /simpleTags" % >。

/WEB-INF/jsp/

jsp 1.2 以下版本的文件存放位置。改目录没有特定的声明，同样，可以根据自己的喜好与习惯来命名。此目录主要存放的是 jsp 1.2 以下版本的文件，为区分 jsp 2.0 文件，通常使用 jsp 命名，当然你也可以命名为 jspOldEdition 。

/WEB-INF/jsp2/

与 jsp 文件目录相比，该目录下主要存放 Jsp 2.0 以下版本的文件，当然，它也是可以任意命名的，同样为区别 Jsp 1.2以下版本的文件目录，通常才命名为 jsp2。

META-INF

相当于一个信息包，目录中的文件和目录获得Java 2平台的认可与解释，用来配置应用程序、扩展程序、类加载器和服务 manifest.mf文件，在用jar打包时自动生成。

# FileInputStream和FileReader

## File 类介绍

File 类封装了对用户机器的文件系统进行操作的功能。例如，可以用 File 类获得文件上次修改的时间，移动，或者对文件进行删除、重命名。换句话说，流类关注的是文件内容，而 File 类关注的是文件在磁盘上的存储。File 不属于文件流 , 只能代表一个文件或是目录的路径名而已。

FileInputStream 类或者 FileReader 类的构造函数有多个，其中典型的两个分别为：一个使用 File 对象为参数；而另一个使用表示路径的 String 对象作为参数；那两者有什么区别，或者说哪个更好呢？如果处理文件或者目录名，就应该使用 File 对象，而不是字符串。因为 File 类有一定的封装，比如它知道一些文件系统对大小写是敏感的，并且目录尾的“ / ”字符无关紧要。 但是如果仅是图方便的话直接用String对象作为参数也未尝不可。 

## FileInputStream 类和FileReader类的区别

FileInputStream 与 FileReader 两个类的构造函数的形式和参数都相同，参数为 File 对象或者表示路径的 String ，它们到底有何区别呢？ 

为了弄明白这两者的区别，我们先看一下InputStream和Reader两个类的区别。

java.io.Reader 和 java.io.InputStream 组成了 Java 输入类。Reader 用于读入16位字符，也就是 Unicode 编码的字符；而 InputStream 用于读入 ASCII 字符和二进制数据。

InputStream类及其子类提供的是字节流的读取，而非文本读取，使用InputStream读取出来的是byte数组。Reader类及其子类提供的是字符流的读取，用Reader读取出来的是char数组或者String。

FileReader是Reader的子类，所以将文件按字符流的方式读取，FileInputStream是InputStream的子类，所以字节流的方式读取文件；

InputStreamReader可以将读如Stream转换成字符流方式，是Reader和Stream之间的桥梁

FileInputStream 类以二进制输入 / 输出， I/O 速度快且效率高，但是它的 read()方法读到的是一个字节，很不利于人们阅读。 而 FileReader 类弥补了这个缺陷，可以以文本格式输入/ 输出，非常方便；比如可以使用 while((ch = filereader.read())!=-1 ) 循环来读取文件；可以使用BufferedReader 的 readLine() 方法一行一行的读取文本。 当我们读写文本文件的时候，采用 Reader 是非常方便的，比如 FileReader ， InputStreamReader 和 BufferedReader 。其中最重要的类是 InputStreamReader ，它是字节转换为字符的桥梁。 你可以在构造器中指定编码的方式，如果不指定的话将采用底层操作系统的默认编码方式，例如 GBK 等。 FileReader 与 InputStreamReader 涉及编码转换 ( 指定编码方式或者采用 os 默认编码 ) ，可能在不同的平台上出现乱码现象！而 FileInputStream 以二进制方式处理，不会出现乱码现象 .  如果处理纯文本文件，建议使用 FileReader ，因为更方便，也更适合阅读；但是要注意编码问题!其他情况（处理非纯文本文件），FileInputStream是唯一的选择；FileInputStream是进Socket通讯时会用到很多，如将文件流是Stream的方式传向服务器！

## FileReader 类

FileReader 类介绍： InputStreamReader 类的子类，所有方法（read （）等）都从父类 InputStreamReader 中继承来，该类与它的父类 InputStreamReader 的主要不同在于构造函数。从 InputStreamReader 的构造函数中看到，参数为 InputStream 和编码方式，可以看出，当要指定编码方式时，必须使用 InputStreamReader 类；而 FileReader 构造函数的参数与 FileInputStream 同，为 File 对象或表示 path 的 String ，可以看出当要根据 File 对象或者 String 读取一个文件时，用 FileReader ，我想FileReader 子类的作用也就在于这个小分工吧。 一般用法： 

FileReader fr = new FileReader("ming.txt");

　　 char[] buffer = new char[1024];

　　 int ch = 0;

　　 while((ch = fr.read())!=-1 )

　　 {

　　　 System.out.print((char)ch); 

　　 } 

## InputStreamReader 类

以文本格式输入，可以指定编码格式； 主要方法： getEncoding ()，read(); 一般用法：

 InputStreamReader isr = new InputStreamReader(new FileInputStream("ming.txt"));

　　 while((ch = isr.read())!=-1)

　　 {

　　　 System.out.print((char)ch); 

　　 } 

## BufferedReader 类 

BufferedReader 由Reader类扩展而来，提供通用的缓冲方式文本读取，而且提供了很实用的readLine，读取分行文本很适合，BufferedReader是针对Reader的，不直接针对文件，也不是只针对文件读取。一般用法：

BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream

("ming.txt")));

　　String data = null;

　　while((data = br.readLine())!=null)

　　{

　　　System.out.println(data); 

　　}

      

总结以上内容，得出比较好的规范用法： 

1）

File file = new File ("hello.txt"); 

FileInputStream in=new FileInputStream(file); 

 

2）

File file = new File ("hello.txt");

FileInputStream in=new FileInputStream(file);

InputStreamReader inReader=new InputStreamReader(in);

BufferedReader bufReader=new BufferedReader(inReader);

 

3）    File file = new File ("hello.txt"); 

FileReader fileReader=new FileReader(file); 

BufferedReader bufReader=new BufferedReader(fileReader); 

 

1）

File file = new File ("hello.txt");

FileInputStream in=new FileInputStream(file);

InputStreamReader inReader=new InputStreamReader(in);

BufferedReader bufReader=new BufferedReader(inReader); 

 

2）

FileInputStream in＝null;

File file = new File ("hello.txt");

in=new FileInputStream(file);

BufferedReader bufReader=new BufferedReader(new InputStreamReader(in)); 

 

3）

File file = new File ("hello.txt");

BufferedReader bufReader=new BufferedReader(new InputStreamReader(new FileInputStream

(file)));

 

上述两种写法的微小区别：

第二种方式中把“FileInputStream in＝null;”定义单独放在开始处，说明下面应该还有要用到in对象变量的地方；（BufferedReader处用了）。

第二种方式没有定义InputStreamReader的对象变量，直接在BufferedReader的构造函数中new一个，这种方式与第一种方式的主要区别：InputStreamReader对象只使用一次！这对于在这里只需要使用一次这个InputStreamReader对象的应用来说更好；无需定义InputStreamReader的对象变量，接收由new返回的该对象的引用，因为下面的程序中不需要这个InputStreamReader的对象变量，所以无需定义；所以这种情况下，第二种方式比第一种更好一些。

第三种方式中，典型的三层嵌套委派关系，清晰看出Reader的委派模式（《corejava》12章有图描述该委派关系），FileInputStream和InputStreamReader都没有定义变量，new生成的对象都只是使用一次。

三种方式的区别也就在于FileInputStream和InputStreamReader对象是否都只使用一次，是否需要定义它们的对象变量，以及个人的编码习惯。

但是要注意异常处理，FileInputStream(file)会抛出NotFileFoundException，如果采用surround方式（try&catch）处理，应该用第二种方式，这样可以用System.out.println提示文件未找到；当然在函数名后使用throws Exception，然后用第三种方式也行，但似乎这适合有用户界面的情况，把异常抛出在客户端在处理。

# 关于使用InputStreamReader读取GBK编码文件乱码的有关问题

BufferedReader reader = new BufferedReader(new InputStreamReader(new FileInputStream(packageFilePath)));

当使用此Reader读取GBK编码的文件时，所有的中文都会乱码，因为Reader会将读取到的byte转换成char，如果没有指定转换编码，如果默认值和文件实际编码值不相同，那么读取到的内容就会错误。那么假如读取完毕后进行一次转码是否可以解决乱码问题呢？

比如：

String s = readline();

s = new String(s.getBytes("gbk"), "gbk");

思路是获得字符串的gbk编码，按照gbk编码重新解析一遍，实验证明是不可以的，是什么原因呢？举例说明：

byte ge[] = {(byte)0xb8, (byte)0xf6};

这是汉字‘个’的gbk编码。

String s = new String(ge, "gbk");

此时s不会是乱码。

s.getBytes("utf8") //得到-28，-72，-86。‘个’的utf8编码

s.getBytes("gbk") //得到0xb8,0xf6。‘个’的gbk编码

而如果用一下代码生成s：

String s = new String(ge, "utf8");

此时s已经是乱码。

s.getBytes("utf8") //得到-17,-65,-67,-17,-65,-67

此时s的内容已经完全乱掉了，所以再用

s.getBytes("gbk");

得到的数据也是乱的，无法逆向出真正的内容来。所以要解决这个问题只能是让reader将byte转向char时使用正确的编码，即生成Reader时指定编码，即：

BufferedReader reader = new BufferedReader(new InputStreamReader(new FileInputStream(packageFilePath), "gbk"));

# Java命名规则

代码编写规范目的：能够在编码过程中实现规范化，为以后的程序开发中养成良好的行为习惯。

代码编写规范使用范围：J2EE项目开发。

## 包命名规范：

目的：包的命名规范应当体现出项目资源良好的划分



servlet类所在包命名规范：公司名称.开发组名称.项目名称.web.servlet

例如：net.linkcn.web.servlet



自定义标签类所在包命名规范：公司名称.开发组名称.项目名称.web.tags

例如：net.linkcn.web.tags



过滤器类所在包命名规范：公司名称.开发组名称.项目名称.web.filter

例如：net.linkcn.web.filter



Action类所在包命名规范：公司名称.开发组名称.项目名称.web.struts.action

例如：net.linkcn.web.struts.action



ActionForm类所在包命名规范：公司名称.开发组名称.项目名称.web.struts.form

例如：net.linkcn.web.struts.form



Javabean所在包命名规范：公司名称.开发组名称.项目名称.web.struts.service.impl

例如：net.linkcn.web.service.impl



Javabean实现接口命名规范：公司名称.开发组名称.项目名称.web.service

例如：net.linkcn.web.service



DAO类所在包命名规范：公司名称.开发组名称.项目名称.dao.impl

例如：net.linkcn.dao.impl



DAO类所实现的接口在包中命名规范：公司名称.开发组名称.项目名称.dao

例如：net.linkcn.dao



POJO类与hbm文件所在包命名规范：公司名称.开发组名称.项目名称.dao.hbm

例如：net.linkcn.dao.hbm



全局公共类、接口类所在包命名规范：公司名称.开发组名称.项目名称.global

例如：net.linkcn.global



全局工具类所在包命名规范：公司名称.开发组名称.项目名称.util

例如：net.linkcn.util

## 类命名规范

基本命名规范：



类、接口命名

命名规范：以大写字母开头，如果有多个单词，每个单词头字母大写

例如：StudentInfo

接口命名

命名规范：以大写字母"I"开头，如果有多个单词，每个单词头字母大写

例如：IStudentInfo

接口实现类命名：

命名规范：将实现的接口名称的首字母"I"去掉，以"Impl作为结尾"，如果有多个单词，每个单词头字母大写。

例如：StudentInfoImpl

## J2EE+SSH框架命名规范

servlet类命名：

命名规范：以Servlet单词结尾

例如：LoginServlet



POJO命名：

使用hibernate自动生成的类即可



DAO类命名：

使用hibernate自动生成的类即可



Action类命名：

命名规范：Action的命名以POJO名称来制定，POJO名称Action

例如：

一个POJO名称为Diary，其对应的action为DiaryAction



ActionForm类命名：

命名规范：ActionForm的命名以POJO名称来制定，POJO名称Form

例如：

一个POJO名称为Diary，其对应的actioForm为DiaryForm



业务逻辑接口命名:

命名规范：业务逻辑接口的命名以POJO名称来制定，IPOJO名称Service

例如：

一个POJO名称为Diary，其对应的业务逻辑接口为IDiaryService



业务逻辑实现类命名:

命名规范：业务逻辑接口实现类的命名以POJO名称来制定

例如：

一个POJO名称为Diary，对应的业务逻辑接口实现类名为DiaryServiceImpl

## 类变量命名：

命名规范：变量名首字母必须小写，如果该变量名有多个单词组成，后面的单 词首字母大写，单词与单词之间不要使用"_"做连接，变量名访问控制必须为私有， 可以对其增加setter与getter方法。

例如：

private int studentAge;

public int getStudentAge(){

return studentAge;

}

public void setStudentAge(int studentAge) {

this.studentAge=studentAge;

}



常量命名：

命名规范：所有字母大写，如果有多个单词组成，单词与单词之间以” _“隔开。而 且该变量必须是公共、静态、final类型

例如：public static final String USER_NAME=”userName“;



方法命名

命名规范：首字母必须小写，如果该变量名有多个单词组成，后面的单词首字母 大写，单词与单词之间不要使用"_"做连接。单词不要使用名词。

例如：public int checkLogin（String name,String pwd）{}



注释规范：注释规范是整个开发规范中最为重要的组成部分，必须严格执行。



类的注释：

作用：注释整个类，简单概述该类作用。

书写规范：类的注释必须写在该类的声明语法之前。在注释中要描述该类的基 本作用，作者，日期，版本，公司名称，版权声明。

格式：



类的声明语法



例如：



public class AdminDAO



变量、常量注释：

作用：简单描述该变量的意义。

书写规范：变量注释必须写在变量定义之前，简单描述其代表的意义。

格式：





例如：





public int age;

方法注释：

作用：对该方法功能简单描述，其参数、返回值意义的注解。

书写规范：方法注释必须写在方法定义之前。该注释包括：方法其功能的简单 描述，方法的参数、返回值类型、返回值意义简单的描述。

格式：





例如：



public booleaneditAdminPassword(int adminId,String oldPassword,

String password) throws UserException,ServiceException;



Jsp页面命名：

命名规范：jsp页面名称要以小写字母开头，如果有多个单词组成，后面的单词以 大写字母开头。名称要体现出该页面的意义，最好能够与模块名称联系在一起。

例如：

login.jsp --登录页面

register.jsp --注册页面

message.jsp --客户留言页面



J2EE项目工程文件夹组织规范：

目的：规范学员web应用程序的资源组织形式，形成良好的文件组织习惯。文件的组织形式应当体现模块的划分。



根据eclipse工具的特征，项目的目录结构为：

src

----存放java文件

WebRoot

|--images --存放web程序所需的公共图片

|--css --存放web程序所需的公共样式表

|--js --存放web程序所需的公共js文件

|--commons --存放web程序所需的公共文件

|--功能模块文件夹(存放与某个功能模块相关的资源)

|--images --存放与该功能模块相关的图片

|--css --存放与该模块相关的样式表文件

|--js --存放与该模块相关的js文件

|--jsp、html页面

|--WEB-INF

|--classes

|--lib

|--tld文件



J2EE项目提交规范

项目完成时要将项目作为一个产品交付用户，良好的项目组织规范可以使用户可以方便的找寻项目中需要的资源，同时也是一个公司专业性的体现。项目提交时，要按照下列文件格式进行提交。



项目主文件夹：

作用：存放项目其他资源文件。

命名规范：时间_班级编号_第X小组。

例如：070706_GS2T18_第四小组。

项目主文件夹下面包括以下文件夹和文件：

|--src：保存.java文件。

|--database：保存数据库的脚本文件或者数据库备份文件。

|--source：保存eclipse工程中WebRoot目录下的所有文件。

|--depend：保存编译该程序必须依赖的其他jar文件。

|--javadoc：保存所有类生成的javadoc api文档。

|--war：保存程序的归档文件

|--xx.war：已经打包好的工程文件，可以直接运行。

|--project：保存开发项目原工程代码及文件。

|--产品说明书.doc：图文方式展现该产品使用方法。

|--build.xml：ant脚本，用于生成运行的war文件。

|--项目解说.ppt：进行项目讲解的ppt（ppt仅供在校模拟项目使用，不用于其他商业用途）

注：一个完整的项目中，数据库必须有一定量的有效的测试数据来支持该程序的运行



包的命名　

Java包的名字都是由小写单词组成。但是由于Java面向对象编程的特性，每一名Java程序员都可以编写属于自己的Java包，为了保障每个 Java包命名的唯一性，在最新的Java编程规范中，要求程序员在自己定义的包的名称之前加上唯一的前缀。由于互联网上的域名称是不会重复的，所以程序 员一般采用自己在互联网上的域名称作为自己程序包的唯一前缀。

例如： net.frontfree.javagroup



类的命名

类的名字必须由大写字母开头而单词中的其他字母均为小写；如果类名称由多个单词组成，则每个单词的首字母均应为大写例如TestPage；如果类名 称中包含单词缩写，则这个所写词的每个字母均应大写，如：XMLExample,还有一点命名技巧就是由于类是设计用来代表对象的，所以在命名类时应尽量 选择名词。 　　

例如： Circle



方法的命名

方法的名字的第一个单词应以小写字母作为开头，后面的单词则用大写字母开头。

例如： sendMessge



常量的命名

常量的名字应该都使用大写字母，并且指出该常量完整含义。如果一个常量名称由多个单词组成，则应该用下划线来分割这些单词。

例如： MAX_VALUE



参数的命名

参数的命名规范和方法的命名规范相同，而且为了避免阅读程序时造成迷惑，请在尽量保证参数名称为一个单词的情况下使参数的命名尽可能明确。



Javadoc注释

Java除了可以采用我们常见的注释方式之外，Java语言规范还定义了一种特殊的注释，也就是我们所说的Javadoc注释，它是用来记录我们代 码中的API的。Javadoc注释是一种多行注释，以结束，注释可以包含一些HTML标记符和专门的关键词。使用Javadoc 注释的好处是编写的注释可以被自动转为在线文档，省去了单独编写程序文档的麻烦。

例如：



在每个程序的最开始部分，一般都用Javadoc注释对程序的总体描述以及版权信息，之后在主程序中可以为每个类、接口、方法、字段添加 Javadoc注释，每个注释的开头部分先用一句话概括该类、接口、方法、字段所完成的功能，这句话应单独占据一行以突出其概括作用，在这句话后面可以跟 随更加详细的描述段落。在描述性段落之后还可以跟随一些以Javadoc注释标签开头的特殊段落，例如上面例子中的@auther和@version，这 些段落将在生成文档中以特定方式显示。



变量和常量命名

变量命名的方法采用匈牙利命名法，基本结构为scope_typeVariableName，它使用3字符前缀来表示数据类型，3个字符的前缀必须 小写，前缀后面是由表意性强的一个单词或多个单词组成的名字，而且每个单词的首写字母大写，其它字母小写，这样保证了对变量名能够进行正确的断句。例如， 定义一个整形变量，用来记录文档数量：intDocCount，其中int表明数据类型，后面为表意的英文名，每个单词首字母大写。这样，在一个变量名就 可以反映出变量类型和变量所存储的值的意义两方面内容，这使得代码语句可读性强、更加容易理解。byte、int、char、long、float、 double、boolean和short。

变量类型和首字母对照关系如下表：

数据类型/对象类型 / 变量前缀 / 备注

byte bye

char chr

float flt

boolean bln 做布尔变量时，使用bln

Integer/int int

String str

Single sng

short sht

Long/long lng

Double/double dbl

Currency cur

Variant bln astr obj vnt 做布尔变量用时，用bln，做字符串数组用时，用astr，做为对象使用时，用obj，不确定时，用vnt。

对于数组，在数据类型的前缀前再增加一个a，例如字符串数组为astr。对于在多个函数内都要使用的全局变量，在前面再增加“g_”。例如一个全局的字符串变量：g_strUserInfo。



在变量命名时要注意以下几点：

· 选择有意义的名字，注意每个单词首字母要大写。



· 在一段函数中不使用同一个变量表示前后意义不同的两个数值。



· i、j、k等只作为小型循环的循环索引变量。



· 避免用Flag来命名状态变量。



· 用Is来命名逻辑变量，如：blnFileIsFound。通过这种给布尔变量肯定形式的命名方式，使得其它开发人员能够更为清楚

的理解布尔变量所代表的意义。



· 如果需要的话，在变量最后附加计算限定词，如：curSalesSum。



· 命名不相包含，curSales和curSalesSum。



· Static Final 变量的名字应该都大写，并且指出完整含义。



· 如果需要对变量名进行缩写时，一定要注意整个代码中缩写规则的一致性。例如，如果在代码的某些区域中使用intCnt，而在另一些区域中又使用intCount，就会给代码增加不必要的复杂性。建议变量名中尽量不要出现缩写。



· 通过在结尾处放置一个量词，就可创建更加统一的变量，它们更容易理解，也更容易搜索。例如，请使用 strCustomerFirst和strCustomerLast，而不要使用strFirstCustomer和strLastCustomer。常 用的量词后缀有：First（一组变量中的第一个）、Last（一组变量中的最后一个）、Next（一组变量中的下一个变量）、Prev（一组变量中的上 一个）、Cur（一组变量中的当前变量）。



· 为每个变量选择最佳的数据类型，这样即能减少对内存的需求量，加快代码的执行速度，又会降低出错的可能性。用于变量的数据类型可能会影响该变量进行计算所产生的结果。在这种情况下，编译器不会产生运行期错误，它只是迫使该值符合数据类型的要求。这类问题极难查找。



· 尽量缩小变量的作用域。如果变量的作用域大于它应有的范围，变量可继续存在，并且在不再需要该变量后的很长时间内仍然占用资源。它们的主要问题是，任何类 中的任何方法都能对它们进行修改，并且很难跟踪究竟是何处进行修改的。占用资源是作用域涉及的一个重要问题。对变量来说，尽量缩小作用域将会对应用程序的 可靠性产生巨大的影响。

关于常量的命名方法，在JAVA代码中，无论什么时候，均提倡应用常量取代数字、固定字符串。也就是说，程序中除0，1以外，尽量不应该出现其他数 字。常量可以集中在程序开始部分定义或者更宽的作用域内，名字应该都使用大写字母，并且指出该常量完整含义。如果一个常量名称由多个单词组成，则应该用下 划线“_”来分割这些单词如：NUM_DAYS_IN_WEEK、MAX_VALUE。

# 分词工具比较

IKAnalyzer 

http://code.google.com/p/ik-analyzer/

IKAnalyzer是一个开源的，基于java语言开发的轻量级的中文分词工具包。从2006年12月推出1.0版开始，IKAnalyzer已经推出了3个大版本。最初，它是以开源项目Luence为应用主体的，结合词典分词和文法分析算法的中文分词组件。新版本的IKAnalyzer3.0则发展为面向Java的公用分词组件，独立于Lucene项目，同时提供了对Lucene的默认优化实现。

语言和平台： 基于java 语言开发，最初它是以开源项目Luence 为应用主体的，结合词典分词和文法分析算法的中文分词组件。新版本的IKAnalyzer 3.0 则发展为面向 Java 的公用分词组件，独立于 Lucene 项目，同时提供了对 Lucene 的默认优化实现。 

算法：采用了特有的“正向迭代最细粒度切分算法” 。采用了多子处理器分析模式，支持：英文字母（ IP 地址、Email、URL ）、数字（日期、常用中文数量词、罗马数字、科学计数法），中文词汇（姓名、地名处理）等分词处理。优化的词典存储，更小的内存占用。支持用户词典扩展定义。针对 Lucene 全文检索优化的查询分析器 IKQueryParser ；采用歧义分析算法优化查询关键字的搜索排列组合，能极大的提高 Lucene 检索的命中率。 

性能：60 万字 / 秒 

IKAnalyzer基于lucene2.0版本API开发，实现了以词典分词为基础的正反向全切分算法，是LuceneAnalyzer接口的实现。该算法适合与互联网用户的搜索习惯和企业知识库检索，用户可以用句子中涵盖的中文词汇搜索，如用"人民"搜索含"人民币"的文章，这是大部分用户的搜索思维；不适合用于知识挖掘和网络爬虫技术，全切分法容易造成知识歧义，因为在语义学上"人民"和"人民币"是完全搭不上关系的。

je-anlysis

分词效率： 每秒30万字（测试环境迅驰1.6，第一次分词需要1－2秒加载词典）

运行环境： Lucene 2.0，基于java实现。

免费安装使用传播，无限制商业应用，但暂不开源，也不提供任何保证

优点:全面支持Lucene 2.0；增强了词典维护的API；增加了商品编码的匹配；增加了Mail地址的匹配；实现了词尾消歧算法第二层的过滤；整理优化了词库；

支持词典的动态扩展；支持中文数字的匹配（如：二零零六）；数量词采用“n”；作为数字通配符优化词典结构以便修改调整；支持英文、数字、中文（简体）混合分词；常用的数量和人名的匹配；超过22万词的词库整理；实现正向最大匹配算法；支持分词粒度控制

ICTCLAS

http://www.ictclas.org/index.html

ictclas4j

ictclas4j中文分词系统是sinboy在中科院张华平和刘群老师的研制的FreeICTCLAS的基础上完成的一个java开源分词项目，简化了原分词程序的复杂度，旨在为广大的中文分词爱好者一个更好的学习机会。 

性能：分词速度单机996KB/s ， API 不超过 200KB ，各种词典数据压缩后不到 3M. 

准确率：分词精度98.45% 

语言和平台：ICTCLAS 全部采用 C/C++ 编写，支持 Linux 、 FreeBSD 及 Windows 系列操作系统，支持 C/C++ 、 C# 、 Delphi 、 Java 等主流的开发语言。 

Author：中国科学院计算技术研究所 

主要功能：中文分词；词性标注；命名实体识别；新词识别；未登录词识别;同时支持用户词典；支持繁体中文；支持GBK 、 UTF-8 、 UTF-7 、 UNICODE 等多种编码格式。 

算法：完美PDAT 大规模知识库管理技术（ 200510130690.3 ），在高速度与高精度之间取得了重大突破，该技术可以管理百万级别的词典知识库，单机每秒可以查询 100 万词条，而内存消耗不到知识库大小的 1.5 倍。层叠隐马尔可夫模型（ Hierarchical Hidden Markov Model ） ，该分词系统的主要是思想是先通过 CHMM( 层叠形马尔可夫模型 ) 进行分词 , 通过分层 , 既增加了分词的准确性 , 又保证了分词的效率 . 共分五层 , 如下图所示。基本思路是进行原子切分 , 然后在此基础上进行 N- 最短路径粗切分 , 找出前 N 个最符合的切分结果 , 生成二元分词表 , 然后生成分词结果 , 接着进行词性标注并完成主要分词步骤 .

imdict

imdict-chinese-analyzer是imdict智能词典的智能中文分词模块，算法基于隐马尔科夫模型(Hidden Markov Model，HMM)，是中国科学院计算技术研究所的ictclas中文分词程序的重新实现（基于Java），可以直接为lucene搜索引擎提供简体中文分词支持。 

imdict-chinese-analyzer 是imdict智能词典的智能中文分词模块 

算法：基于隐马尔科夫模型(Hidden Markov Model，HMM)，是中国科学院计算技术研究所的 ictclas 中文分词程序的重新实现（基于Java），可以直接为lucene 搜索引擎提供简体中文分词支持 。

主要功能： 

完全 Unicode 支持：分词核心模块完全采用Unicode 编码，无须各种汉字编码的转换，极大的提升了分词的效率。 

提升搜索效率：根据imdict智能词典的实践，在有智能中文分词的情况下，索引文件比没有中文分词的索引文件小 1/3 

提高搜索准确度：imdict -chinese-analyzer采用了 HHMM 分词模型，极大的提高了分词的准确率，在此基础上的搜索，比对汉字逐个切分要准确得多！ 

更高效的数据结构：为了提高效率，针对常用中文检索的应用场景，imdict-chinese-analyzer 对一些不必要的功能进行了删减，例如词性标注、人名识别、时间识别等等。另外还修改了算法的数据结构，在内存占用量缩减到 1/3 的情况下把效率提升了数倍。

paoding 

http://www.oschina.net/p/paoding/

Paoding's Knives中文分词基于Java的开源中文分词组件，提供lucene和solr 接口，具有极高效率和高扩展性。引入隐喻，采用完全的面向对象设计，构思先进。高效率：在PIII 1G内存个人机器上，1秒可准确分词100万汉字。采用基于不限制个数的词典文件对文章进行有效切分，使能够将对词汇分类定义。能够对未知的词汇进行合理解析。 

语言和平台：Java  提供 lucence  3.0  接口，仅支持 Java 语言。 Paoding（庖丁解牛分词）基于Java的开源中文分词组件，提供lucene和solr 接口，具有极高效率和高扩展性 。引入隐喻，采用完全的面向对象设计，构思先进。 

MMSEG4J

基于Java的开源中文分词组件，提供lucene和solr 接口。

mmseg4j 用 Chih-Hao Tsai 的 MMSeg 算法实现的中文分词器，并实现 lucene 的 analyzer 和 solr 的TokenizerFactory 以方便在Lucene和Solr中使用。

MMSeg 算法有两种分词方法：Simple和Complex，都是基于正向最大匹配。Complex 加了四个规则过虑。官方说：词语的正确识别率达到了98.41% ，mmseg4j 已经实现了这两种分词算法。

# nutch1.8+solr 4 配置过程

Nutch 2.2.1目前性能没有Nutch 1.7好，参考这里，NUTCH FIGHT! 1.7 vs 2.2.1. 所以我目前还是使用的Nutch 1.8。

1 下载已编译好的二进制包，解压

$ wget http://psg.mtu.edu/pub/apache/nutch/1.8/apache-nutch-1.8-bin.tar.gz

$ tar zxf apache-nutch-1.8-bin.tar.gz

2 验证一下

$ cd apache-nutch-1.8

$ bin/nutch

如果出现”Permission denied”请运行下面的命令：

$ chmod +x bin/nutch

如果有Warning说 JAVA_HOME没有设置，请设置一下JAVA_HOME.

3 添加种子URL

mkdir ~/urls

vim ～/urls/seed.txt

http://movie.douban.com/subject/5323968/

4 设置URL过滤规则

如果只想抓取某种类型的URL，可以在 conf/regex-urlfilter.txt设置正则表达式，于是，只有匹配这些正则表达式的URL才会被抓取。

例如，我只想抓取豆瓣电影的数据，可以这样设置：

#注释掉这一行

# skip URLs containing certain characters as probable queries, etc.

#-[?*!@=]

# accept anything else

#注释掉这行

#+.

+^http:\/\/movie\.douban\.com\/subject\/[0-9]+\/(\?.+)?$

5 设置agent名字

conf/nutch-site.xml:

<property>

  <name>http.agent.name</name>

  <value>My Nutch Spider</value>

</property>

这一步是从这本书上看到的，Web Crawling and Data Mining with Apache Nutch，第14页。

6 安装Solr

由于建索引的时候需要使用Solr，因此我们需要安装并启动一个Solr服务器。

参考Nutch Tutorial 第4、5、6步，以及Solr Tutorial。

6.1 下载，解压

wget http://mirrors.cnnic.cn/apache/lucene/solr/4.6.1/solr-4.6.1.tgz

tar -zxf solr-4.6.1.tgz

6.2 运行Solr

cd example

java -jar start.jar

验证是否启动成功

用浏览器打开 

http://localhost:8983/solr/#/

，如果能看到页面，说明启动成功。

6.3 将Nutch与Solr集成在一起

将NUTCH_DIR/conf/schema-solr4.xml拷贝到SOLR_DIR/example/solr/collection1/conf/，重命名为schema.xml，并在<fields>...</fields>最后添加一行(具体解释见Solr 4.2 - what is _version_field?)，

<field name="_version_" type="long" indexed="true" stored="true" multiValued="false"/>

重启Solr，

# Ctrl+C to stop Solr

java -jar start.jar

7 使用crawl脚本一键抓取

Nutch自带了一个脚本，./bin/crawl，把抓取的各个步骤合并成一个命令，看一下它的用法

$ bin/crawl 

Missing seedDir : crawl <seedDir> <crawlDir> <solrURL> <numberOfRounds>

注意，是使用bin/crawl，不是bin/nutch crawl，后者已经是deprecated的了。

7.1 抓取网页

$ bin/crawl urls/ TestCrawl/ http://localhost:8983/solr/ 2

urls/ 是存放了种子url的目录

TestCrawl/ 是存放数据的根目录（在Nutch 2.x中，则表示crawlId，这会在HBase中创建一张以crawlId为前缀的表，例如TestCrawl_Webpage）

http://localhost:8983/solr/ , 这是Solr服务器

2，numberOfRounds，迭代的次数

过了一会儿，屏幕上出现了一大堆url，可以看到爬虫正在抓取！

fetching http://music.douban.com/subject/25811077/ (queue crawl delay=5000ms)

fetching http://read.douban.com/ebook/1919781 (queue crawl delay=5000ms)

fetching http://www.douban.com/online/11670861/ (queue crawl delay=5000ms)

fetching http://book.douban.com/tag/绘本 (queue crawl delay=5000ms)

fetching http://movie.douban.com/tag/科幻 (queue crawl delay=5000ms)

49/50 spinwaiting/active, 56 pages, 0 errors, 0.9 1 pages/s, 332 245 kb/s, 131 URLs in 5 queues

fetching http://music.douban.com/subject/25762454/ (queue crawl delay=5000ms)

fetching http://read.douban.com/reader/ebook/1951242/ (queue crawl delay=5000ms)

fetching http://www.douban.com/mobile/read-notes (queue crawl delay=5000ms)

fetching http://book.douban.com/tag/诗歌 (queue crawl delay=5000ms)

50/50 spinwaiting/active, 61 pages, 0 errors, 0.9 1 pages/s, 334 366 kb/s, 127 URLs in 5 queues

7.2 查看结果

$ bin/nutch readdb TestCrawl/crawldb/ -stats

14/02/14 16:35:47 INFO crawl.CrawlDbReader: Statistics for CrawlDb: TestCrawl/crawldb/

14/02/14 16:35:47 INFO crawl.CrawlDbReader: TOTAL urls: 70

14/02/14 16:35:47 INFO crawl.CrawlDbReader: retry 0:    70

14/02/14 16:35:47 INFO crawl.CrawlDbReader: min score:  0.005

14/02/14 16:35:47 INFO crawl.CrawlDbReader: avg score:  0.03877143

14/02/14 16:35:47 INFO crawl.CrawlDbReader: max score:  1.23

14/02/14 16:35:47 INFO crawl.CrawlDbReader: status 1 (db_unfetched):    59

14/02/14 16:35:47 INFO crawl.CrawlDbReader: status 2 (db_fetched):  11

14/02/14 16:35:47 INFO crawl.CrawlDbReader: CrawlDb statistics: done

8 一步一步使用单个命令抓取网页

上一节为了简单性，一个命令搞定。本节我将严格按照抓取的步骤，一步一步来，揭开爬虫的神秘面纱。感兴趣的读者也可以看看 bin/crawl 脚本里的内容，可以很清楚的看到各个步骤。

先删除第7节产生的数据，

$ rm -rf TestCrawl/

8.1 基本概念

Nutch data is composed of:

The crawl database, or crawldb. This contains information about every URL known to Nutch, including whether it was fetched, and, if so, when.

The link database, or linkdb. This contains the list of known links to each URL, including both the source URL and anchor text of the link.

A set of segments. Each segment is a set of URLs that are fetched as a unit. Segments are directories with the following subdirectories:

a crawl_generate names a set of URLs to be fetched

a crawl_fetch contains the status of fetching each URL

a content contains the raw content retrieved from each URL

a parse_text contains the parsed text of each URL

a parse_data contains outlinks and metadata parsed from each URL

a crawl_parse contains the outlink URLs, used to update the crawldb

8.2 inject:使用种子URL列表，生成crawldb

$ bin/nutch inject TestCrawl/crawldb ~/urls

将根据urls/下的种子URL，生成一个URL数据库，放在crawdb/目录下。

8.3 generate

$ bin/nutch generate TestCrawl/crawldb TestCrawl/segments

这会生成一个 fetch list，存放在一个segments/日期目录下。我们将这个目录的名字保存在shell变量s1里：

$ s1=`ls -d TestCrawl/segments/2* | tail -1`

$ echo $s1



8.4 fetch

$ bin/nutch fetch $s1



将会在 $1 目录下，生成两个子目录, crawl_fetch 和 content。

8.5 parse

$ bin/nutch parse $s1

将会在 $1 目录下，生成3个子目录, crawl_parse, parse_data 和 parse_text 。

8.6 updatedb

$ bin/nutch updatedb TestCrawl/crawldb $s1

这将把crawldb/current重命名为crawldb/old，并生成新的 crawldb/current 。

8.7 查看结果

$ bin/nutch readdb TestCrawl/crawldb/ -stats

8.8 invertlinks

在建立索引之前，我们首先要反转所有的链接，这样我们就可以获得一个页面所有的锚文本，并给这些锚文本建立索引。

$ bin/nutch invertlinks TestCrawl/linkdb -dir TestCrawl/segments

8.9 solrindex, 提交数据给solr，建立索引

$ bin/nutch solrindex http://localhost:8983/solr TestCrawl/crawldb/ -linkdb TestCrawl/linkdb/ TestCrawl/segments/20140203004348/ -filter -normalize

8.10 solrdedup, 给索引去重

有时重复添加了数据，导致索引里有重复数据，我们需要去重，

$bin/nutch solrdedup http://localhost:8983/solr

8.11 solrclean, 删除索引

如果数据过时了，需要在索引里删除，也是可以的。

$ bin/nutch solrclean TestCrawl/crawldb/ http://localhost:8983/solr

# Java 数组的静态初始化和动态初始化

静态初始化是指由程序员自己为数组对象的每个元素赋值，由系统自动计算出数组的长度,例如：

String[] a=new String[]{"Hello","World","Yes"};

动态初始化是指由程序员自己指定数组对象的长度，由系统先自动为其赋值。程序中程序员可以为元素重新赋值,例如：

String [] b=new String[4];

for(int i=0;i<b.length;i++){

b[i]=i+"hello ";

}

通常基本整数类型byte,short,int,long,初始值为0；浮点型float,double,初始值为0.0；boolean类型，初始值为false；引用类型：类、String、数组等均为null；

在使用数组的时候，我们通常有两个步骤：首先，声明数组引用变量，即String[] a,此时的a并不是一个数组对象，而只是一个相当于指针的变量；然后，当我们执行new String[]{"Hello","World","Yes"}以后才真正创建了一个数组对象，此时变量a 才指向了堆内存里面的数组对象。

# String数组初始化

近日，笔者在java编程中因为疏忽对String数组的初始化定义错误，导致程序运行出错。现将所理解的String数组在此进行说明，并对String数组初始化进行分析。



//一维数组

String[] str = new String[5]; //创建一个长度为5的String(字符串)型的一维数组

String[] str = new String[]{"","","","",""};

String[] str = {"","","","",""};

//二维数组

String[][] str = new String[2][2]; //创建一个2行2列的二维数组

String数组初始化区别

String[] str = {"1","2","3"}与String[] str = new String[]{"1","2","3"}在内存里有什么区别？

编译执行结果没有任何区别。更不可能像有些人想当然说的在栈上分配空间，Java的对象都是在堆上分配空间的。这里的区别仅仅是代码书写上的：String[] str = {"1","2","3"}; 这种形式叫数组初始化式（Array Initializer），只能用在声明同时赋值的情况下。而 String[] str = new String[]{"1","2","3"} 是一般形式的赋值，=号的右边叫数组字面量（Array Literal），数组字面量可以用在任何需要一个数组的地方（类型兼容的情况下）。如：

　　String[] str = {"1","2","3"}; // 正确的

　　String[] str = new String[]{"1","2","3"} // 也是正确的

而

　　String[] str;

　　str = {"1","2","3"}; // 编译错误

因为数组初始化式只能用于声明同时赋值的情况下。改为：

　　String[] str;

　　str = new String[] {"1","2","3"}; // 正确了

又如：

　　void f(String[] str) {

　　}

　　f({"1","2","3"}); // 编译错误

正确的应该是：

　　f(new String[] {"1","2","3"});

笔者所犯错误为在初始化数组的时候定义为String[] str = new String[]{}，如此定义相当于创建了创建一个长度为0的String型的一维数组。在后期为其赋值的时候str[0]="A"，就会抛出异常。

# 字符串的各种编码转换 

java中的String类是按照unicode进行编码的，当使用String(byte[] bytes, String encoding)构造字符串时，encoding所指的是bytes中的数据是按照那种方式编码的，而不是最后产生的String是什么编码方式，换句话说，是让系统把bytes中的数据由encoding编码方式转换成unicode编码。如果不指明，bytes的编码方式将由jdk根据操作系统决定。

当我们从文件中读数据时，最好使用InputStream方式，然后采用String(byte[] bytes, String encoding)指明文件的编码方式。不要使用Reader方式，因为Reader方式会自动根据jdk指明的编码方式把文件内容转换成unicode编码。

当我们从数据库中读文本数据时，采用ResultSet.getBytes()方法取得字节数组，同样采用带编码方式的字符串构造方法即可。

ResultSet rs;

bytep[] bytes = rs.getBytes();

String str = new String(bytes, "gb2312");

不要采取下面的步骤：

ResultSet rs;

String str = rs.getString();

str = new String(str.getBytes("iso8859-1"), "gb2312");

这种编码转换方式效率底。之所以这么做的原因是，ResultSet在getString()方法执行时，默认数据库里的数据编码方式为iso8859-1。系统会把数据依照iso8859-1的编码方式转换成unicode。使用str.getBytes("iso8859-1")把数据还原，然后利用new String(bytes, "gb2312")把数据从gb2312转换成unicode，中间多了好多步骤。

从HttpRequest中读参数时，利用reqeust.setCharacterEncoding()方法设置编码方式，读出的内容就是正确的了。

# Java与Unicode

Java的class文件采用utf8的编码方式，JVM运行时采用utf16，Java的字符串是unicode编码的。总之，Java采用了unicode字符集，使之易于国际化。Java支持哪些字符集：即Java能识别哪些字符集并对它进行正确地处理？查看Charset 类，最新的JDK支持160种字符集。可以通过static方法availableCharsets拿到所有Java支持的字符集。

assertEquals(160, Charset.availableCharsets().size());

Set<String> charsetNames = Charset.availableCharsets().keySet();  

assertTrue(charsetNames.contains("utf-8")); 

assertTrue(charsetNames.contains("utf-16"));

assertTrue(charsetNames.contains("gb2312"));

assertTrue(Charset.isSupported("utf-8")); 

需要在哪些时候注意编码问题？

## 从外部资源读取数据

这跟外部资源采取的编码方式有关，我们需要使用外部资源采用的字符集来读取外部数据：

InputStream is = new FileInputStream("res/input2.data");

InputStreamReader streamReader = new InputStreamReader(is, "GB18030"); 

这里可以看到，我们采用了GB18030编码读取外部数据，通过查看streamReader的encoding可以印证：

assertEquals("GB18030", streamReader.getEncoding()); 

正是由于上面我们为外部资源指定了正确的编码，当它转成char数组时才能正确地进行解码（GB18030 -> unicode）：

char[] chars = new char[is.available()]; 

streamReader.read(chars, 0, is.available()); 

但我们经常写的代码就像下面这样：

InputStream is = new FileInputStream("res/input2.data"); 

InputStreamReader streamReader = new InputStreamReader(is); 

这时候InputStreamReader采用什么编码方式读取外部资源呢？Unicode？不是，这时候采用的编码方式是JVM的默认字符集，这个默认字符集在虚拟机启动时决定，通常根据语言环境和底层操作系统的 charset 来确定。可以通过以下方式得到JVM的默认字符集：

Charset.defaultCharset(); 

为什么要这样？因为我们从外部资源读取数据，而外部资源的编码方式通常跟操作系统所使用的字符集一样，所以采用这种默认方式是可以理解的。

好吧，那么我通过我的IDE Ideas创建了一个文件，并以JVM默认的编码方式从这个文件读取数据，但读出来的数据竟然是乱码。为何？其实是因为通过Ideas创建的文件是以utf-8编码的。要得到一个JVM默认编码的文件，通过手工创建一个txt文件试试吧。

## 字符串和字节数组的相互转换

我们通常通过以下代码把字符串转换成字节数组：

"string".getBytes(); 

但你是否注意过这个转换采用的编码呢？其实上面这句代码跟下面这句是等价的：

"string".getBytes(Charset.defaultCharset()); 

也就是说它根据JVM的默认编码（而不是你可能以为的unicode）把字符串转换成一个字节数组。反之，如何从字节数组创建一个字符串呢？

new String("string".getBytes()); 

同样，这个方法使用平台的默认字符集解码字节的指定数组（这里的解码指从一种字符集到unicode）。

字符串编码迷思：

new String(input.getBytes("ISO-8859-1"), "GB18030"); 

上面这段代码代表什么？有人会说： “把input字符串从ISO-8859-1编码方式转换成GB18030编码方式”。如果这种说法正确，那么又如何解释我们刚提到的java字符串都采用unicode编码呢？

这种说法不仅是欠妥的，而且是大错特错的，让我们一一来分析，其实事实是这样的：我们本应该用GB18030的编码来读取数据并解码成字符串，但结果却采用了ISO-8859-1的编码，导致生成一个错误的字符串。要恢复，就要先把字符串恢复成原始字节数组，然后通过正确的编码GB18030再次解码成字符串（即把以GB18030编码的数据转成unicode的字符串）。注意，字符串永远都是unicode编码的。但编码转换并不是负负得正那么简单，这里我们之所以可以正确地转换回来，是因为 ISO8859-1 是单字节编码，所以每个字节被按照原样转换为 String ，也就是说，虽然这是一个错误的转换，但编码没有改变，所以我们仍然有机会把编码转换回来！

## 总结

所以，我们在处理java的编码问题时，要分清楚三个概念：Java采用的编码：unicode，JVM平台默认字符集和外部资源的编码。通过Eclipse下的演示工程,介绍如何打包这样的项目：要导出的类里边用到了别的jar包。

# JAVA调用系统命令或可执行程序  

通过 java.lang.Runtime 类可以方便的调用操作系统命令或者一个可执行程序，下面的小例子在windows和linux分别测试通过。基本原理是首先通过 Runtime.getRuntime() 返回与当前 Java 应用程序相关的运行时对象，然后调用run.exec(cmd)  另启一个进程来执行命令（cmd为要执行的命令）。

## 运行一个可执行程序

执行一个.exe的文件，或通过已安装的软件打开一个特定格式的文件，如word、chm或mp3等等。

在window下可以直接执行一个.exe文件，如执行我在F盘下的tomcat安装文件，将命令写为：

String cmd = "F:\\apache-tomcat-6.0.20.exe";

打开一个word文档。如果系统已经安装了office应用程序，就可以通过调用word的可执行程序来打开一个word文档：

String cmd = "D:\\Program Files\\Microsoft Office\\OFFICE11\\WINWORD.EXE F:\\test.doc";

当然这样写有点麻烦，我们想打开一个word文档时只要双击就可以了，用不着去找WINWORD.EXE。要是打开每一种格式的文件都得去找它的可执行程序，那可累死了，我们可以通过下面的代码，打开任意一个已知格式的文件（只要安装的打开这种文件格式的软件），相当于用鼠标双击一个文件的图标：

String cmd = "cmd.exe /c start F:\\test.doc";

我用C写了一个进程操作的小例子，放在 linux 下编译出的可执行文件叫“fork_wait”，然后把我的java文件编译成TestRunTime.class后扔到 linux 上，在控制台执行 java TestRunTime 命令，TestRunTime 和 fork_wait 程序均运行成功。

String cmd = "./fork_wait";

## 执行一个有标准输出的系统命令

通过调用进程的 getInputStream() 方法，可以获得执行命令的标准输出。在 windows 的cmd控制台窗口和 linux 控制台执行系统名利的格式是一样的，只是输入的命令不同而已。如要执行windows控制台中ping命令，可写为：

String cmd = "ping www.baidu.com";

执行linux的ls命令，可写为：

String cmd = "ls -l";

如果要执行一个带参数的命令，可使用 String 数组形式，如：

String[] cmd=new String[3];

cmd[0]="/bin/sh";

cmd[1]="-c";

cmd[2]="ls -l ./";

下面是我写的小例子：



import java.io.BufferedInputStream;

import java.io.BufferedReader;

import java.io.InputStreamReader;



public class TestRunTime {

	public static void main(String[] args) {

		//windows

//		String cmd = "F:\\apache-tomcat-6.0.20.exe";

//		String cmd = "D:\\Program Files\\Microsoft Office\\OFFICE11\\WINWORD.EXE F:\\test.doc";

//		String cmd = "cmd.exe /c start F:\\test.doc";

		String cmd = "ping www.baidu.com";

		

		//linux

//		String cmd = "./fork_wait";

//		String cmd = "ls -l";

//		String[] cmd=new String[3];

//		cmd[0]="/bin/sh";

//		cmd[1]="-c";

//		cmd[2]="ls -l ./";

		Runtime run = Runtime.getRuntime();//返回与当前 Java 应用程序相关的运行时对象

		try {

			Process p = run.exec(cmd);// 启动另一个进程来执行命令

			BufferedInputStream in = new BufferedInputStream(p.getInputStream());

			BufferedReader inBr = new BufferedReader(new InputStreamReader(in));

			String lineStr;

			while ((lineStr = inBr.readLine()) != null)

				//获得命令执行后在控制台的输出信息

				System.out.println(lineStr);// 打印输出信息

			//检查命令是否执行失败。

			if (p.waitFor() != 0) {

				if (p.exitValue() == 1)//p.exitValue()==0表示正常结束，1：非正常结束

					System.err.println("命令执行失败!");

			}

			inBr.close();

			in.close();

		} catch (Exception e) {

			e.printStackTrace();

		}

	}

}

# Java RMI与RPC，JMS的比较

远程对象方法调用(RMI Remote Method Invocation)并不是新概念，远程过程调用 (RPC Remote Procedure Call) 也已经使用很多年了。远程过程调用被设计为在应用程序间通信的平台中立的方式，它不理会操作系统之间以及语言之间的差异。即 RPC 支持多种语言，而 RMI只支持 Java 写的应用程序。

另外 RMI 调用远程对象方法，允许方法返回 Java 对象以及基本数据类型。而 RPC 不支持对象的概念，传送到 RPC 服务的消息由外部数据表示 (XDR External Data Representation) 语言表示，这种语言抽象了字节序类和数据类型结构之间的差异。只有由 XDR 定义的数据类型才能被传递，RPC 不允许传递对象。可以说 RMI 是面向对象方式的 Java RPC 。

Java 消息服务 ( Java Messaging Service, JMS ) 是一种允许应用程序创建、发送、接受和读取消息的Java API 。 JMS 与 RMI 的区别在于，采用 JMS 服务，对象是在物理上被异步从网络的某个 JVM 上直接移动到另一个 JVM 上。而 RMI 对象是绑定在本地 JVM 中，只有函数参数和返回值是通过网络传送的。

公共对象请求代理体系结构(CORBA  Common Object Request Broker Architecture) 是 90 年代初有 OMG 组织提出的一个分布式互操作标准，属于语言中立的。而 RMI 直接把分布式对象模型嵌入到 Java 语言的内部，使得 Java程序员可以自然的编写分布式程序，不必离开 Java 环境，或者涉及 CORBA IDL 以及 Java 到 CORBA 的类型转换。然而 RMI 不遵守 CORBA 标准，基本上是Java-to-Java 技术，难以实现与其他语言编写的对象之间的互操作。

RMI 和 CORBA 常被视为相互竞争的技术，因为两者都提供对远程分布式对象的透明访问。但这两种技术实际上是相互补充的，一者的长处正好可以弥补另一者的短处。 RMI 和 CORBA 的结合产生了 RMI-IIOP， RMI-IIOP 是企业服务器端 Java 开发的基础。

1997 年， IBM 和 Sun Microsystems 启动了一项旨在促进 Java 作为企业开发技术的发展的合作计划。两家公司特别着力于如何将 Java 用作服务器端语言，生成可以结合进现有体系结构的企业级代码。所需要的就是一种远程传输技术，它兼有 Java 的 RMI较少的资源占用量和更成熟的 CORBA技术的健壮性。出于这一需要， RMI-IIOP问世了，它帮助将 Java 语言推向了目前服务器端企业开发的主流语言的领先地位 。

分布式组件对象模型(DCOM Distributed Component Object Model)是从组件对象模型(COM Component Object Model)改造过来的， COM 这一技术部分是作为规范，定义了对象实现的二进制标准，用于单机上应用之间的通信，对象实现与使用的语言无关。 DCOM 是 COM 的分布式扩展，在 DCE RPC 之上构造对象的远程过程调用层支持对远程对象的访问。一个 DCOM 对象是支持一个或多个接口的组件。DCOM 对象不支持对象 ID ，因此，客户程序不能与某个特定的对象发生联系。

# className.class.getResourceAsStream()与ClassLoader.getSystemResourceAsStream() 的区别

className.class.getResourceAsStream ：

一： 要加载的文件和.class文件在同一目录下，例如：com.x.y 下有类Test.class ,同时有资源文件config.properties

那么，应该有如下代码：



//前面没有“/”代表当前类的目录



InputStream is1 = Test.class.getResourceAsStream("config.properties");

System.out.println(is1);// 不为null



第二：在Test.class目录的子目录下，例如：com.x.y 下有类Test.class ,同时在 com.x.y.prop目录下有资源文件config.properties



那么，应该有如下代码：



//前面没有“/”代表当前类的目录



InputStream is2 = Test.class.getResourceAsStream("prop/config.properties");

System.out.println(is2);//不为null



第三：不在同目录下，也不在子目录下，例如：com.x.y 下有类Test.class ,同时在 com.m.n 目录下有资源文件config.properties



那么，应该有如下代码：



//前面有“/”,代表了工程的根目录



InputStream is3 = Test.class.getResourceAsStream("/com/m/n/config.properties");



System.out.println(is3);//不为null



ClassLoader.getSystemResourceAsStream ：



和className.class.getResourceAsStream 的第三种取得的路径一样，但少了“/”



 



InputStream is4 = ClassLoader.getSystemResourceAsStream("properties/PayManagment_Config.properties");

System.out.println(is4);//不为null

# jps的用法及常见问题介绍 

jps类似linux的ps命令，不同的是ps是用来显示进程，而jps只显示java进程，准确的说是当前用户已启动的部分java进程信息，信息包括进程号和简短的进程command。

现象：用ps -ef|grep java能看到启动的java进程，但是用jps查看却不存在该进程的id。待会儿解释过之后就能知道在该情况下，jconsole、jvisualvm可能无法监控该进程，其他java自带工具也可能无法使用。

分析：java程序启动后，默认会在/tmp/hsperfdata_userName目录下以该进程的id为文件名新建文件，并在该文件中存储jvm运行的相关信息，其中的userName为当前的用户名，/tmp/hsperfdata_userName目录会存放该用户所有已经启动的java进程信息。对于windows机器/tmp用Windows存放临时文件目录代替。而jps、jconsole、jvisualvm等工具的数据来源就是这个文件（/tmp/hsperfdata_userName/pid)。所以当该文件不存在或是无法读取时就会出现jps无法查看该进程号，jconsole无法监控等问题。

原因：

（1）、磁盘读写、目录权限问题

若该用户没有权限写/tmp目录或是磁盘已满，则无法创建/tmp/hsperfdata_userName/pid文件。或该文件已经生成，但用户没有读权限

（2）、临时文件丢失，被删除或是定期清理

对于linux机器，一般都会存在定时任务对临时文件夹进行清理，导致/tmp目录被清空。这也是我第一次碰到该现象的原因。常用的可能定时删除临时目录的工具为crontab、redhat的tmpwatch、ubuntu的tmpreaper等等。这个导致的现象可能会是这样，用jconsole监控进程，发现在某一时段后进程仍然存在，但是却没有监控信息了。

（3）、java进程信息文件存储地址被设置，不在/tmp目录下

上面我们在介绍时说默认会在/tmp/hsperfdata_userName目录保存进程信息，但由于以上1、2所述原因，可能导致该文件无法生成或是丢失，所以java启动时提供了参数(-Djava.io.tmpdir)，可以对这个文件的位置进行设置，而jps、jconsole都只会从/tmp目录读取，而无法从设置后的目录读物信息，这是我第二次碰到该现象的原因。设置该文件位置的参数为-Djava.io.tmpdir

其他：/tmp/hsperfdata_userName/pid文件会在对应java进程退出后被清除。如果java进程非正常退出（如kill -9），那么pid文件会被保留，直到执行一次java命令或是加载了jvm程序的命令（如jps、javac、jstat），会将所有无用的pid文件都清除掉

关于jps更多的介绍，查看oracle介绍 ：

http://download.oracle.com/javase/1.5.0/docs/tooldocs/share/jps.html

# Maven相关

## maven 下载 源码和javadoc命令

Maven命令下载源码和javadocs

当在IDE中使用Maven时如果想要看引用的jar包中类的源码和javadoc需要通过maven命令下载这些源码，然后再进行引入，通过mvn命令能够容易的达到这个目的：

mvn dependency:sources

mvn dependency:resolve -Dclassifier=javadoc

命令使用方法：首先进入到相应的pom.xml目录中，然后执行以上命令：

第一个命令是尝试下载在pom.xml中依赖的文件的源代码。

第二个命令：是尝试下载对应的javadocs

但是有可能一些文件没有源代码或者javadocs

通过配置文件添加

打开maven配置文件 setting.xml文件(.../.m2/settings.xml) 增加如下配置：

<profiles>  

<profile>  

    <id>downloadSources</id>  

    <properties>  

        <downloadSources>true</downloadSources>  

        <downloadJavadocs>true</downloadJavadocs>             

    </properties>  

</profile>  

</profiles>  

  

<activeProfiles>  

  <activeProfile>downloadSources</activeProfile>  

</activeProfiles>  

配置eclipse

Window > Preferences > Maven and checking the "Download Artifact Sources" and "Download Artifact JavaDoc" options



## 杂项

间接依赖的jar包能否直接使用

如果工程依赖A.jar，并用maven设置好依赖，同时A.jar会依赖B.jar，所以maven在下载A.jar的同时会下载B.jar，这时如果项目发现需要使用B.jar中的一些内容，在maven中不必从新设置依赖，可以在工程中直接使用。



把某个本地jar包安装到本地仓库中

mvn install:install-file -DgroupId="edu.jiangxin" -DartifactId=”gcu” -Dversion="1.0.0"

-Dpackaging=”jar” -Dfile="D:\CS\J2EE\lib\edu.jiangxin.gcu-1.0.0.jar"



把某个本地jar包部署到某个远程仓库中

mvn deploy:deploy-file -DgroupId="edu.jiangxin" -DartifactId=”gcu” -Dversion="1.0.0"

-Dpackaging=”jar” -Dfile="D:\CS\J2EE\lib\edu.jiangxin.gcu-1.0.0.jar" -Durl=http://yourlocalrepository:8888/archiva/repository/internal

-DrepositoryId=internal

maven中如何生成javadoc

mvn javadoc:javadoc

# Ant相关

## Ant 编译时 Unable to find a javac compiler的解决

Ant不能和JRE一起使用，而需要使用JDK来作为Runtime JRE,打开菜单：Run--External Tool--External Tools...

在右边打开JRE页，在Separate JRE:中选择JDK，如果没有这个选项的话，单击在旁边的Installed JREs...---单击Add---增加一个JDK项



具体方法为：

输入JRE name:（随意）JDK

找到JDK的安装路径，输入到JRE home directory

完成退出



回到External Tools...的JRE页，确定退出



我的方法是，在JRE Definiton 中 点击 Add External JARS 然后把jre/lib/tools.jar放进去，结果就没出现这个问题了。我觉得这确实算是Eclipse的一个小小的Bug吧，执行Ant的虚拟机 是jre目录，但是ant 的编译功能需要调用tools.jar但是jre里没有，所以需要手动导入。

# Selenium相关

## selenium的版本和firefox不兼容

【Selenium】   -> 【FireFox】

2.25.0        ->  18

2.30.0        ->  19

2.31.0        ->  20

2.42.2        ->  29

2.44.0        ->  33 (不支持31,2014/12/1)

PS：但是selenium-java-2.42.2版本和firefox 29.0.1版本兼容，如果升级到firefox 30+,则浏览器启动失败。可能是selenium还未同步升级，后面估计可以正常支持。切记，关掉forefox的升级功能，否则连本地Windows上的脚本都跑不起来，作者曾经为此还降级了forefox。

升级后，selenium脚本正常启动firefox。

## selenium使用IE 浏览器问题

Started InternetExplorerDriver server (64-bit)

2.25.2.0

Listening on port 40961Exception in thread "main" org.openqa.selenium.WebDriverException: Unexpected error launching Internet Explorer. Protected Mode settings are not the same for all zones. Enable Protected Mode must be set to the same value (enabled or disabled) for all zones. (WARNING: The server did not provide any stacktrace information)

Command duration or timeout: 1.18 seconds

Build info: version: '2.25.0', revision: '17482', time: '2012-07-18 22:18:01'System info: os.name: 'Windows 7', os.arch: 'x86', os.version: '6.1', java.version: '1.6.0_29'Driver info: driver.version: InternetExplorerDriver

Session ID: 01e30b64-e403-440c-bed8-4859ef2128f9

        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)

        at sun.reflect.NativeConstructorAccessorImpl.newInstance(Unknown Source)

        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(Unknown Source)

        at java.lang.reflect.Constructor.newInstance(Unknown Source)

        at org.openqa.selenium.remote.ErrorHandler.createThrowable(ErrorHandler.java:188)

        at org.openqa.selenium.remote.ErrorHandler.throwIfResponseFailed(ErrorHandler.java:145)

        at org.openqa.selenium.remote.RemoteWebDriver.execute(RemoteWebDriver.java:498)

        at org.openqa.selenium.remote.RemoteWebDriver.startSession(RemoteWebDriver.java:182)

        at org.openqa.selenium.remote.RemoteWebDriver.startSession(RemoteWebDriver.java:167)

        at org.openqa.selenium.ie.InternetExplorerDriver.startSession(InternetExplorerDriver.java:133)

        at org.openqa.selenium.ie.InternetExplorerDriver.setup(InternetExplorerDriver.java:106)

        at org.openqa.selenium.ie.InternetExplorerDriver.(InternetExplorerDriver.java:52)

        at com.selenium.test.TempGoogle.main(TempGoogle.java:15)

如果遇到上面的问题



解决方法有两种：

1.是修改掉IE的设置，不要在任何情况下使用保护模式（protected mode）

2.另一种即是前面代码中如下片段在运行时设置IE的Capabilities。

DesiredCapabilities ieCapabilities = DesiredCapabilities.internetExplorer();

ieCapabilities.setCapability

      

(InternetExplorerDriver.INTRODUCE_FLAKINESS_BY_IGNORING_SECURITY_DOMAINS,true);

WebDriver oWebDriver = new InternetExplorerDriver(ieCapabilities);

# 过时date.toLocaleString()的解决方法

System.out.println(new java.util.Date());  

输出：Thu Jan 27 14:43:28 CST 2011

System.out.println(new java.util.Date().toLocaleString());  

输出：2011-1-27 14:45:21

不过现在toLocaleString()方法已过时，由DateFormat.format(Date date)取代。

DateFormat ddf = DateFormat.getDateInstance();  

DateFormat dtf = DateFormat.getTimeInstance();  

DateFormat ddtf = DateFormat.getDateTimeInstance();  

Date date = new Date();  

System.out.println("日期：" + ddf.format(date));  

System.out.println("时间：" + dtf.format(date));  

System.out.println("日期时间：" + ddtf.format(date));  

SimpleDateFormat sdf = (SimpleDateFormat) DateFormat.getDateTimeInstance();  

System.out.println("日期时间：" + sdf.format(date));  

输出：

日期：2011-2-9

时间：11:16:02

日期时间：2011-2-9 11:16:02

日期时间：2011-2-9 11:16:02

 

*************以上是在window系统下，linux系统下不能这么处理***********

linux系统下用以上获取回来的初始时间格式与此不同。

# 关于toString

List list = new ArrayList(); 

list.add("a"); 

list.add(null); 

list.add("b"); 

for(int i=0;i<list.size();i++){ 

     System.out.println(list.get(i).toString()); 

     在遍历第二个null值时就报空指针异常 

但是我写成 

    System.out.println((String)list.get(i));//遍历第二个值等于null时候就没错是为什么？ 

}



public String toString() { 

return getClass().getName() + "@" + Integer.toHexString(hashCode()); 



} 

当一个OBJECT==null的时候，并没有被初始化，没初始化怎么能调用toString方法呢

第二种强制转换(String)null为什么可以，表面理解，(Integer)null,(Map)null都可以，也就是说null可以通过强制转换，转换成任意的对象object,并且指向为空，从深层次理解：以指针的角度来看，它代表着一个对象只有指针，没有指针所对应的地址，所以无论你怎么转换对象，变的都只是定义了一个指针，至于指针是什么类型的，只有在分配地址的时候才有用，也就是new的时候才会用到。在强制转换中null根本没有分配地址，所以系统可以通过，当然深层次是我个人的理解，可能存在偏差，但是概括一点就是，null的强制转换没有对指针所对应的内存地址空间发生变化，所以java可以不抱错

# Html/Xhtml/Html5

<black>使文字呈现闪烁效果



&nbsp; 不断行的空白格,是英文的一个空格

&ensp; 半方大的空白,相当于半个中文字的位置

&emsp; 全方大的空白,相当于一个中文字的位置

## meta标签

meta标签共有两个属性，它们分别是http-equiv属性和name属性，

不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。 　　



⒈name属性 　　name属性主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。 　　

meta标签的name属性语法格式是：<meta name="参数" content="具体的参数值">；。 　



其中name属性主要有以下几种参数：

A、keywords（关键字） 　　

说明：keywords用来告诉搜索引擎你网页的关键字是什么。 　　

举例：<meta name ="keywords" content="science,education,culture,politics,ecnomics,relationships,entertainment,human"> 　　

B、description（网站内容描述） 　　

说明：description用来告诉搜索引擎你的网站主要内容。 　　

网站内容描述（description）的设计要点： 　　

①网页描述为自然语言而不是罗列关键词（与keywords设计正好相反）；　 　　

②尽可能准确地描述网页的核心内容，通常为网页内容的摘要信息，也就是希望搜索引擎在检索结果中展示的摘要信息；　 　　

③网页描述中含有有效关键词；　 　　

④网页描述内容与网页标题内容有高度相关性； 　　

⑤网页描述内容与网页主体内容有高度相关性； 　　

⑥网页描述的文字不必太多，一般不超过搜索引擎检索结果摘要信息的最多字数（通常在100中文字之内，不同搜索引擎略有差异）。 　

举例：<meta name="description" content="This page is about the meaning of science,education,culture."> 　　

C、robots（机器人向导） 　　

说明：robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。 　

举例：<meta name="robots" content="none"> 　　

D、author（作者） 　　

说明：标注网页的作者 　

举例：<meta name="author" content="root,root@21cn.com"> 　　



⒉http-equiv属性 　　http-equiv顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。 　　

meta标签的http-equiv属性语法格式是：<meta http-equiv="参数" content="参数变量值"> ；

其中http-equiv属性主要有以下几种参数： 　　

A、Expires（期限） 　　

说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。 　　

用法：<meta http-equiv="expires" content="Fri,12 Jan 2001 18:18:18 GMT"> 

注意：必须使用GMT的时间格式。 　　

B、Pragma(cache模式） 　　

说明：禁止浏览器从本地计算机的缓存中访问页面内容。 　　

用法：<meta http-equiv="Pragma" content="no-cache"> 

注意：这样设定，访问者将无法脱机浏览。 　　

C、Refresh（刷新） 　　

说明：自动刷新并指向新页面。 　　

用法：<meta http-equiv="Refresh" content="2;URL=http://www.root.net">；（注意后面的引号，分别在秒数的前面和网址的后面） 　　

注意：其中的2是指停留2秒钟后自动刷新到URL网址。  

D、Set-Cookie(cookie设定） 　　

说明：如果网页过期，那么存盘的cookie将被删除。 　　

用法：<meta http-equiv="Set-Cookie" content="cookievalue=xxx; expires=Friday,12-Jan-2001 18:18:18 GMT; path=/"> 　　

注意：必须使用GMT的时间格式。 　　

E、Window-target（显示窗口的设定） 　　

说明：强制页面在当前窗口以独立页面显示。 　　

用法：<meta http-equiv="Window-target" content="_top"> 　　

注意：用来防止别人在框架里调用自己的页面。 　　

F、content-Type（显示字符集的设定） 　　

说明：设定页面使用的字符集。 　　

用法：<meta http-equiv="content-Type" content="text/html; charset=gb2312"> 　　

G、content-Language（显示语言的设定） 　　

用法：<meta http-equiv="Content-Language" content="zh-cn" />

# Javascript

JavaScript利用对象的能力比VBScript强，可以使用JavaScript定义类，是Object-Based的脚本语言。虽然它貌似Java，但语法上和C相似，是一种独立的语言。

## javascript中CDATA的意义

CDATA 内部的所有东西都会被解析器忽略。



假如文本中包含了大量的 "<" 和 "&" 字符 - 就像编程代码中经常出现的情况一样 - 那么这个 XML 元素就可以被定义为一个 CDATA 部分。



CDATA 区段开始于 "<![CDATA["，结束于 "]]>"：



<script type="text/javascript">

<![CDATA[

function compare(a,b)

{

if (a < b)

   {alert("a小于b");}

else if (a>b)

   {alert("a大于b");}

else

   {alert("a等于b");}

}

]]>

</script>



在上面的例子中，在 CDATA 区段中的所有东西都会被解析器忽略。





关于 CDATA 区段的注释:



CDATA 区段不能包含字符串 "]]>"，所以，CDATA 区段的嵌套是不被允许的。



同时也需要确保在 "]]>" 字符串中没有空格或折行。



为什么要使用CDATA:



       XHTML的第二个改变是使用CDATA段。XML中的CDATA段用于声明不应被解析为标签的文本（XHTML也是如此），这样就可以使用特殊字符，如小于（<）、大于（>）、和号（&）和双引号（"），而不必使用它们的字符实体。考虑下面的代码：



<script type="text/javascript">

function compare(a,b)

{

if (a < b)

   {alert("a小于b");}

else if (a>b)

   {alert("a大于b");}

else

   {alert("a等于b");}

}

</script>



这个函数相当简单，它比较数字a和b，然后显示消息说明它们的关系。但是，在XHTML中，这段代码是无效的，因为它使用了三个特殊符号，即小于、大于和双引号。要修正这个问题，必须分别用这三个字符的XML实体&lt;、&gt;和&quot;替换它们：



<script type="text/javascript">

function compare(a,b)

{

if (a &lt;b)

   {alert(&quot;a小于b&quot;);}   

else if (a&gt;b)

   {alert(&quot;a大于b&quot;);}

else

   {alert(&quot;a等于b&quot;);}

}

</script>



这段代码存在两个问题。首先，开发者不习惯用XML实体编写代码。这使代码很难读懂。其次，在JavaScript中，这种代码实际上将视为有语法错，因为解释程序不知道XML实体的意思。用CDATA段即可以以常规形式（即易读的语法）编写JavaScript代码。正式加入CDATA段的方法如下：



<script type="text/javascript">

<![CDATA[

function compare(a,b)

{

if (a < b)

   {alert("a小于b");}

else if (a>b)

   {alert("a大于b");}

else

   {alert("a等于b");}

}

]]>

</script>



虽然这是正式方式，但还要记住，大多数浏览器都不完全支持XHTML，这就带来主要问题，即这在JavaScript中是个语法错误，因为大多数浏览器还不认识CDATA段。



<script type="text/javascript">

//<![CDATA[                                            

function compare(a,b)

{

if (a < b)

   {alert("a小于b");}

else if (a>b)

   {alert("a大于b");}

else

   {alert("a等于b");}

}

//]]>                                      

</script>



当前使用的解决方案模仿了“对旧浏览器隐藏”代码的方法。使用单行的JavaScript注释"//"，可在不影响代码语法的情况下嵌入CDATA段：



现在，这段代码在不支持XHTML的浏览器中也可运行。



但是，为避免CDATA的问题，最好还是用外部文件引入JavaScript代码。



网站建设流程：

定网站的主题

规划网站的内容和结构

收集相关资料

设计网页版面

网页制作

上网发布网站

定期维护网站



页面标记语言：HTML,XML,…

脚本语言：VBScript,JavaScript,…

服务器编程语言：ASP,ASP.NET,ColdFusion标记语言(CFML),JSP,PHP,…



Dreamweaver介绍

MDI：多文档界面



Dreamweaver站点

本地站点 local

远程站点 remote

测试站点 test 测试本地站点、远程站点的质量、功能和一致性等



规划站点结构：

利用不同的文件夹将不同的网页内容分门别类地保存，合理地组织站点结构。使用合理的文件、文件夹名称，避免使用长文件名和中文。对于大型项目可设置多级文件夹结构。

在每个主目录下建立独立的images目录



域名的设计与申请

设计模仿型域名：

yahoo,sohoo(sohu),lohoo,yahoo

ebay,etang,elong,ecord,efun

设计数字型域名：

163,169,263,8848,3721

设计区域性域名：

china.com,hongkong.com,taiwan.com

设计拼音型域名：

zhaodaola.com,rongshu.com,paimai.com,zhaopin.com

设计组合型域名：

51job(无忧),51go,51love,chinaren



国际域名注册规则： 

　　1、只提供英文字母（a-z，不区分大小写）、数字（0-9）、以及"-"（英文中的连词号，即中横线），不能使用空格及特殊字符(如!、$、&、? 等)。 

　　2、"-"不能用作开头和结尾 

　　3、域名最长可达67个字节(包括后缀.com、.net、.org等)。 

中国34个顶级域名之行政区域名 

　　BJ-北京市； SH-上海市； TJ-天津市； CQ-重庆市； HE-河北省； SX-山西省； NM -内蒙古自治区； LN-辽宁省； JL-吉林省； HL-黑龙江省； JS-江苏省； ZJ-浙江省； AH-安徽省； FJ-福建省； JX-江西省； SD-山东省； HA-河南省； HB-湖北省； HN-湖南省； GD-广东省； GX-广西壮族自治区； HI-海南省； SC-四川省； GZ-贵州省； YN -云南省； XZ-西藏自治区； SN-陕西省； GS-甘肃省； QH-青海省； NX-宁夏回族自治区； XJ-新疆维吾尔自治区； TW-台湾； HK-香港； MO-澳门。此外，从2002年12月份开始，CNNIC开放了国内.cn域名下的二级域名注册，可以在.CN下直接注册域名，如Google所注册的国内域名为：Google.cn。 第三类顶级域名，也就是所谓的“新顶级域名”，是ICANN根据互联网发展需要，在2000年11月做出决议，从2001年开始使用的国际顶级域名，也包含7类：biz, info，name，pro，aero, coop, museum。 其中前4个是非限制性域，后3个是限制性域，如aero需是航空业公司注册，museum需是博物馆，coop需是集体企业（非投资人控制，无须利润最大化）注册。这7个顶级域名的含义和注册管理机构如下： .aero，航空运输业专用，由比利时国际航空通信技术协会（SITA）负责； .biz，可以替代.com的通用域名，监督机构是JVTeam； .coop，商业合作社专用，由位于华盛顿的美国全国合作商业协会（NCBA）负责管理； .info，可以替代.net的通用域名，由19个因特网域名注册公司联合成立的Afilias负责；　.museum，博物馆专用，由博物馆域名管理协会（MDMA）监督； .name，是个人网站的专用域名，由英国的“环球姓名注册”（GlobeNameRegistry）负责； .pro，医生和律师等职业专用，监督机构是爱尔兰都柏林的一家网络域名公司“职业注册”（RegistryPro）。 关于ICANN为什么要增加新的7个域的背景资料：　自80年代国际互联网出现以来，.com、.net、.org一直是商家和消费者最热衷的三个通用顶级域。特别是.com域名，更是占据了通用顶级域的80%以上。多年来NSI公司长期垄断对这三个域的注册和管理权。1999年，ICANN、美国商务部终止了这种垄断局面，在REGISTRAR这个层面引入了竞争机制。但是在REGISTRY这个层面上的竞争还是不够，造成了DNS体系多年来没有显著改善。新的7个顶级域的REGISTRY也于2000年11月选定，NSI除了在INFO域REGISTRY的中有少量股份外，与其它各主要新域REGISTRY没有干系。这样，新的顶级域的推出，将会在REGISTRY业内引进竞争机制。新的REGISTRY从技术到运营机制方面都有改进，如：一改今日WHOIS分散在各个REGISGTRAR的局面，实行同一的WHOIS；域名信息（zone file）和WHOIS查询全球范围5分钟更新，此前.COM域下需要24到48小时；更高的系统冗余性、安全性和认证的严密程度。似乎认识到新域带来的严峻挑战，.com域的运营商Verisign Global Registry Service（2000年兼并了NSI）在向ICANN提交的新合同中（新合同在2001年4月2日正式被ICANN批准），主动提出将在未来的几年中投资两亿美金，用于加强.COM域下的基础设施建设。 看了这些有关顶级域名及国内域名后缀的介绍之后，可以发现，很多域名资源可以利用，不过对于商业性公司来说，直到目前为止，最为通用的仍然是.com域名，国内企业或者在国内有经营机构的外国企业则一般同时注册.com.cn域名。自从.cn二级域名开发注册以来，国内网站似乎更青睐用.cn域名。 

国家地区标准代码(国际域名缩写)  

　　国际域名和国内域名两者之间在使用上是否有区别？ 

国际域名是用户可注册的通用顶级域名的俗称。它的后缀为.com、.net或.org。国内域名为后缀为.cn的域名。二者注册机构不同，在使用中基本没有区别。

# 关于层和HTML代码

当您在Web页中插入层时，Dreamweaver将这些层的HTML标签插入到您的代码中。您可以为您的层设置四种不同的标签：div，span，layer和ilayer。其中div和span是最常见的标签，推荐您使用，这样才能有最广泛的受众可以看到您的层。Internet Explorer 4.0和Netscape Navigator 4.0都支持使用div和span标签创建的层。只有Navigator 4.0版本支持使用layer和ilayer创建的层（Netscape在其后续版本浏览器中停止了对这两种标签的支持）。这些浏览器的早期版本都可以显示层的内容，但不能显示其位置。



默认情况下，Dreamweaver使用div标签创建层，并在插入点或页面顶部body标签后面放置层代码。如果您创建嵌套层，Dreamweaver将把代码插入到您定义的父层标签中。若要改变默认标签，请参看设置层参数。



下面是一个单个的层的HTML代码示例（在Dreamweaver中的情况）：



<div id="Layer1" style="position:absolute; visibility:inherit; width:200px; height:115px; z-index:1">

</div>

下面是一个嵌套层的HTML代码示例（在Dreamweaver中的情况）：



<div id="Parent" style="position:absolute; left:56px; top:54px; width:124px; height:158px; z-index:1;">

Content inside the parent layer. 

<div id="Nested" style="position:absolute; left:97px; top:114px; width:54px; height:69px; z-index:1;">

Content inside the nested layer. 

</div>

</div>

您可以设置层在页面上的位置属性。这些属性包括左边和顶部（分别对应x和y坐标），Z轴（也称为堆叠顺序），和可见性。如需要更多信息，请参看设置层属性。

# 清理无用的CSS样式的几个工具

在我们写样式的时候，页面的CSS在经历几个版本的修改之后，可能有些样式已经用不到了，或许将某些样式更名了而原来的忘了删除，总之页面中可能存在着一些无用的样式。这些无用的浪费了一些服务器空间和带宽消耗，也会增大我们的维护成本。那么有没有一些办法来清理那些无用的样式呢？今天就让我们来了解一下几个比较有用的工具。

Dust-Me selectors

Dust-Me是一个很有用也很好用的Firefox插件，它可以分析到你的页面中调用的所有CSS文件并分析那些在页面中没有被用到。支持本地和远程样式文件，包括使用link标签、< ?xml-stylesheet?>处理指令、@import语句等方式引入的样式文件；(但是不支持页面中的style块和内联样式)，支持IE条件注释中引入的样式文件；可以检查一个页面，也可以检查整个网站；支持CSS1选择器、大部分CSS2和CSS3选择器；理解通用的CSS hack，比如 “* html #fuck-ie”将会被认为是”html #fuck-ie”；支持Firefox 3.5和Firefox 3.0，事实上得益于FF 3.5的js引擎的改进，FF 3.5中的性能比FF 3.0要高50%。

Page Speed

Page Speed是Google提供的一个前端性能分析工具，有些类似于YSlow，但是提供了一些比较个性且很有用的工具，比如Remove unused CSS。Page Speed和YSlow一样依赖Firebug。

CSS Redundancy Checker

CSS Redundancy Checker 是一个免费的在线应用，可以检查所有的使用某个CSS文件的页面中无用的样式。可以同时检查某一个样式在多个页面中的使用情况。该工具的不足是虽然一次能检查多个HTML页面，但每次只能检查一个CSS文件，而且还要手动输入。

IntelliJ IDEA

IntelliJ IDEA 这是一个颇强大的IDE，类似于DreamWeaver，不过在国内用的不多。该软件包括一个即时代码分析工具(On-the-fly Code Analysis)，可以分析CSS文件中未用到的class和id。

Expression Web

Expression Web作为微软的新一代网站开发工具，还是有很多人使用的，其CSS Report功能可以检查未用到需要被清除的CSS（我的确没有使用EW开发过网站，希望使用该软件的童鞋可以帮忙确认一下这一点）。

# 网站设计中揪出网页的无效链接

在我们浏览网站的时候，一定都遇到过页面上带红叉的无效图片或者“无法找到网页”的提示，出现如此现象一般都是因为链接文件的位置发生变化、被误删除或者文件名的拼写错误造成的。 为了避免出现无效链接的尴尬，树立良好的网站形象，当我们完成一个网站的设计制作后，一定要认真地检查是否存在失效链接，以便及时修改。将无效链接扼杀在上传前。

为了预防网站上传后出现无效链接，在上传前我们可以使用FrontPage的超链接报表功能来检查整个网站的链接情况，如果遇到无效链接还可以及时编辑修复。首先我们要把需要检查链接的站点设置为FrontPage的网站，运行FrontPage，选择“文件→新建→由一个网页组成的网站”进入“网站模板”窗口，单击“浏览”指定到你的站点目录，“确定”后即可打开整个网站。执行“视图→报表→问题→超链接”，弹出对话框询问是否验证网站中的超链接，单击“是”验证所有超链接，包括指向站内网页的内部链接和指向外部网站的外部链接，稍等一会儿FrontPage就会将验证结果显示出来。验证结果包括链接所在的网页、网页标题、链接目标和类型等。对于无效链接，FrontPage会在“状态”栏下标注“中断”，选中并双击一个“中断”的无效超链接，在弹出的超链接编辑窗口中就可以对错误的超链接进行修复了。我们可以直接键入正确的链接地址或在“浏览”中选择指定到正确的文件，如果在其他网页中也有这个相同的错误链接，我们可以勾选“对所有网页进行更改”，然后点击“替换”按钮即可修复网站中所有包含这个无效链接的网页了。

网站上传运行后，如果网站中引用了大量的外来网站内容的链接，而我们又无法控制外来内容链接的有效性，我们只有经常对网站测试其链接的可靠性，以避免无效链接的出现。若要继续使用FrontPage对网站无效链接进行检查，还需要将网站全部下载到本地，这样会显得很麻烦，这里我们推荐使用一个小工具Xenu Link Sleuth来对网站进行在线检查。打开软件，执行“File→Check URL”打开一个对话窗口，输入你要检查的网站地址，“OK”后软件就会自动访问网站并验证每个链接地址，验证结束后就会将结果显示在验证列表中，对于无效的链接，软件会以红色字体加以区别。在失效链接的右键菜单中选择“Properties”，然后在“Properties”窗口中的“Pages linking to”下可以查看到哪些网页使用了这个无效链接，对这些网页单独下载加以修复就可以了。

提示:验证结束后，软件还可以生成一份详细的无效链接报告，包括无效链接页面以及使用无效链接的页面等以供修复时查阅。

# shortcut icon无法正常显示问题解决

<link rel="shortcut icon" href="favicon.ico" />显示不了图标，ie显示不了小图片,但Firefox能显示出来请教各位,怎么能让IE最好是IE7也能显示出来?谢谢了

解决方法：

1、<link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/> 

2、IE要7以上版本才支持，低于7的，除非用Maxhon之类的壳才能出现该图标。

3、这种问题应该是安装了别的浏览器引起的，比如：我就安装了Firefox.打开注册表找到如下内容：[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.htm\]下的默认值改为htmlfile(比如：我是由FirefoxHTML改为htmlfile.)，问题解决.^_^。最好事先把这个键值导出备份一下。

# Struts2、Spring和Hibernate应用实例

Struts作为MVC 2的Web框架，自推出以来不断受到开发者的追捧，得到广泛的应用。作为最成功的Web框架，Struts自然拥有众多的优点：MVC 2模型的使用、功能齐全的标志库（Tag Library）、开放源代码。而Spring的出现，在某些方面极大的方面了Struts的开发。同时，Hibernate作为对象持久化的框架，能显示的提高软件开发的效率与生产力。这三种流行框架的整合应用，可以发挥它们各自的优势，使软件开发更加的快速与便捷。

struts2发布已经很久了，但关于如何使用它的教程及实例并不多。特别是与Spring及Hibernate等流行框架的集成，并不多见。现在就将笔者使用Myeclipse工具应用struts2 + spring2 + hibernate3 实现CRUD操作的步骤一一纪录下来，为初学者少走弯路略尽绵薄之力！在本文中，笔者将Struts2.0.6、Spring2.0.6和Hibernate3.1进行整合，希望通过这样的整合示例，让读者了解这些框架各自的特点，以便于在自己的项目中，根据实际情况，尽快的过渡到Struts2的时代。本文的内容基于Struts2.0.6。

 

## 一、准备工作

 

spring2与1.x区别不大，可以平滑的过度，笔者也是把spring1.28换成了spring2.0.6，算是升级到spring 2.0了。struts2基本就是webwork2.2，与以前的struts1.x可以说没任何关系了。因为是第一次用struts2，也是第一次用webwork，所以有很多不完善，不规范的地方，还望大家来拍砖。

开发环境：MyEclipse5.0+Eclipse3.2+JDK5.0+

Tomcat5.5+struts2+Spring2.0.6+Hibernate3.1。本示例通过对一个图书进行管理的系统，提供基本的增加、删除、修改、查询等功能。

lib包需要以下右图所示的这些包。其中Struts2.0.6的下载地址为：

http://people.apache.org/builds/struts/2.0.6

Hibernate3.1的下载地址为：

http://www.hibernate.org

spring2.0.6的下载地址为：

http://www.springframework.org

使用的数据库为mysql 5.0，使用的JDBC驱动JAR包为：mysql-connection-java-5.0.4-bin

创建数据表的sql语句为：

create database game 

CREATE TABLE `books` (

`book_id` int(11) NOT NULL default '0',

`book_name` varchar(200) character set gb2312 default NULL,

`book_author` varchar(100) character set gb2312 default NULL,

`book_publish` varchar(100) character set gb2312 default NULL,

`book_date` date default NULL,

`book_isbn` varchar(20) default NULL,

`book_page` int(11) default NULL,

`book_price` decimal(10,2) default NULL,

`book_content` varchar(100) character set gb2312 default NULL,

PRIMARY KEY  (`book_id`)

) ENGINE=InnoDB DEFAULT CHARSET=gbk ROW_FORMAT=COMPRESSED;



## 二、建立公共类 

1、AbstractAction类

Struts2和Struts1.x的差别，最明显的就是Struts2是一个pull-MVC架构。Struts1.x 必须继承org.apache.struts.action.Action或者其子类，表单数据封装在FormBean中。Struts 2无须继承任何类型或实现任何接口，表单数据包含在Action中，通过Getter和Setter获取。

虽然，在理论上Struts2的Action无须实现任何接口或者是继承任何的类，但是，在实际编程过程中，为了更加方便的实现Action，大多数情况下都会继承com.opensymphony.xwork2.ActionSupport类，并且重载（Override）此类里的String execute()方法。因此先建立抽象类，以供其它Action类使用。



package com.sterning.commons;

import com.opensymphony.xwork2.ActionSupport;

public class AbstractAction extends ActionSupport {

}

com.sterning.commons.AbstractAction.java

参考JavaDoc，可知ActionSupport类实现了接口：

com.opensymphony.xwork2.Action

com.opensymphony.xwork2.LoaleProvider

com.opensymphony.xwork2.TextProvider

com.opensymphony.xwork2.Validateable

com.opensymphony.xwork2.ValidationAware

com.uwyn.rife.continuations.ContinuableObject

java.io.Searializable

java.lang.Cloneable



2、Pager分页类

为了增加程序的分页功能，特意建立共用的分页类。



package com.sterning.commons;

import java.math.*;

public class Pager {

private int totalRows; //总行数

    private int pageSize = 5; //每页显示的行数

    private int currentPage; //当前页号

    private int totalPages; //总页数

    private int startRow; //当前页在数据库中的起始行



public Pager() {

}

public Pager(int _totalRows) {

totalRows = _totalRows;

totalPages=totalRows/pageSize;

int mod=totalRows%pageSize;

if(mod>0){

totalPages++;

}

currentPage = 1;

startRow = 0;

}

public int getStartRow() {

return startRow;

}

public int getTotalPages() {

return totalPages;

}

public int getCurrentPage() {

return currentPage;

}

public int getPageSize() {

return pageSize;

}

public void setTotalRows(int totalRows) {

this.totalRows = totalRows;

}

public void setStartRow(int startRow) {

this.startRow = startRow;

}

public void setTotalPages(int totalPages) {

this.totalPages = totalPages;

}

public void setCurrentPage(int currentPage) {

this.currentPage = currentPage;

}

public void setPageSize(int pageSize) {

this.pageSize = pageSize;

}

public int getTotalRows() {

return totalRows;

}

public void first() {

currentPage = 1;

startRow = 0;

}

public void previous() {

if (currentPage == 1) {

return;

}

currentPage--;

startRow = (currentPage - 1) * pageSize;

}

public void next() {

if (currentPage < totalPages) {

currentPage++;

}

startRow = (currentPage - 1) * pageSize;

}

public void last() {

currentPage = totalPages;

startRow = (currentPage - 1) * pageSize;

}

public void refresh(int _currentPage) {

currentPage = _currentPage;

if (currentPage > totalPages) {

last();

}

}

}



com.sterning.commons.Pager.java

同时，采用PagerService类来发布成为分页类服务PagerService，代码如下：



package com.sterning.commons;

public class PagerService {

public Pager getPager(String currentPage,String pagerMethod,int totalRows) {

//    定义pager对象，用于传到页面

        Pager pager = new Pager(totalRows);

//    如果当前页号为空，表示为首次查询该页

//    如果不为空，则刷新pager对象，输入当前页号等信息

        if (currentPage != null) {

pager.refresh(Integer.parseInt(currentPage));

}

//    获取当前执行的方法，首页，前一页，后一页，尾页。

        if (pagerMethod != null) {

if (pagerMethod.equals("first")) {

pager.first();

} else if (pagerMethod.equals("previous")) {

pager.previous();

} else if (pagerMethod.equals("next")) {

pager.next();

} else if (pagerMethod.equals("last")) {

pager.last();

}

}

return pager;

}

}



com.sterning.commons.PagerService.java 



## 三、 建立数据持久化层

 

1、编写实体类Books及books.hbm.xml映射文件。



package com.sterning.books.model;

import java.util.Date;

public class Books {

//    Fields 

    private String bookId;//编号

    private String bookName;//书名

    private String bookAuthor;//作者

    private String bookPublish;//出版社

    private Date bookDate;//出版日期

    private String bookIsbn;//ISBN

    private String bookPage;//页数

    private String bookPrice;//价格

    private String bookContent;//内容提要

//    Constructors

    public Books(){}

//    Property accessors



    public String getBookId() {

return bookId;

}

public void setBookId(String bookId) {

this.bookId = bookId;

}

public String getBookName() {

return bookName;

}

public void setBookName(String bookName) {

this.bookName = bookName;

}

public String getBookAuthor() {

return bookAuthor;

}

public void setBookAuthor(String bookAuthor) {

this.bookAuthor = bookAuthor;

}

public String getBookContent() {

return bookContent;

}

public void setBookContent(String bookContent) {

this.bookContent = bookContent;

}

public Date getBookDate() {

return bookDate;

}

public void setBookDate(Date bookDate) {

this.bookDate = bookDate;

}

public String getBookIsbn() {

return bookIsbn;

}

public void setBookIsbn(String bookIsbn) {

this.bookIsbn = bookIsbn;

}

public String getBookPage() {

return bookPage;

}

public void setBookPage(String bookPage) {

this.bookPage = bookPage;

}

public String getBookPrice() {

return bookPrice;

}

public void setBookPrice(String bookPrice) {

this.bookPrice = bookPrice;

}

public String getBookPublish() {

return bookPublish;

}

public void setBookPublish(String bookPublish) {

this.bookPublish = bookPublish;

}

}



com.sterning.books.model.Books.java

       接下来要把实体类Books的属性映射到books表，编写下面的books.hbm.xml文件：



<?xml version="1.0"?>

<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"

"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">

<hibernate-mapping>

     <class name="com.sterning.books.model.Books" table="books" >

         <id name="bookId" type="string">

            <column name="book_id" length="5" />

            <generator class="assigned" />

        </id>

        <property name="bookName" type="string">

            <column name="book_name" length="100" />

        </property>

         <property name="bookAuthor" type="string">

            <column name="book_author" length="100" />

        </property>

        <property name="bookPublish" type="string">

            <column name="book_publish" length="100" />

        </property>

         <property name="bookDate" type="java.sql.Timestamp">

            <column name="book_date" length="7" />

        </property>

          <property name="bookIsbn" type="string">

            <column name="book_isbn" length="20" />

        </property>

        <property name="bookPage" type="string">

            <column name="book_page" length="11" />

        </property>

        <property name="bookPrice" type="string">

            <column name="book_price" length="4" />

        </property>

<property name="bookContent" type="string">

            <column name="book_content" length="100" />

        </property>

     </class>

</hibernate-mapping>



com.sterning.books.model.books.hbm.xml

2、hibernate.cfg.xml配置文件如下：（注意它的位置在scr/hibernate.cfg.xml）



<?xml version="1.0" encoding="ISO-8859-1"?>

<!DOCTYPE hibernate-configuration PUBLIC

"-//Hibernate/Hibernate Configuration DTD 3.0//EN"

"http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

<session-factory>

    <property name="show_sql">true</property>

    <mapping resource="com/sterning/books/model/books.hbm.xml"></mapping>

</session-factory>

</hibernate-configuration>



Com.sterning.bean.hibernate.hibernate.cfg.xml 



## 四、 建立DAO层

 

DAO访问层负责封装底层的数据访问细节，不仅可以使概念清晰，而且可以提高开发效率。

1、建立DAO的接口类：BooksDao



package com.sterning.books.dao.iface;

import java.util.List;

import com.sterning.books.model.Books;

public interface BooksDao {

List getAll();//获得所有记录

    List getBooks(int pageSize, int startRow);//获得所有记录

    int getRows();//获得总行数

    int getRows(String fieldname,String value);//获得总行数

    List queryBooks(String fieldname,String value);//根据条件查询

    List getBooks(String fieldname,String value,int pageSize, int startRow);//根据条件查询

    Books getBook(String bookId);//根据ID获得记录

    String getMaxID();//获得最大ID值

    void addBook(Books book);//添加记录

    void updateBook(Books book);//修改记录

    void deleteBook(Books book);//删除记录    

}



com.sterning.books.dao.iface.BooksDao.java 



2、实现此接口的类文件，BooksMapDao



package com.sterning.books.dao.hibernate;

import java.sql.SQLException;

import java.util.Iterator;

import java.util.List;

import org.hibernate.HibernateException;

import org.hibernate.Query;

import org.hibernate.Session;

import org.springframework.orm.hibernate3.HibernateCallback;

import org.springframework.orm.hibernate3.support.HibernateDaoSupport;

import com.sterning.books.dao.iface.BooksDao;

import com.sterning.books.model.Books;

import com.sterning.commons.PublicUtil;

/**

* @author cwf

*

*/

public class BooksMapDao extends HibernateDaoSupport implements BooksDao {

public BooksMapDao(){}

/**

* 函数说明：添加信息

* 参数说明：对象

* 返回值：

*/

    public void addBook(Books book) {

this.getHibernateTemplate().save(book);

}

/**

* 函数说明：删除信息

* 参数说明： 对象

* 返回值：

*/

    public void deleteBook(Books book) {

this.getHibernateTemplate().delete(book);

}

/**

* 函数说明：获得所有的信息

* 参数说明：

* 返回值：信息的集合

*/

    public List getAll() {

String sql="FROM Books ORDER BY bookName";

return this.getHibernateTemplate().find(sql);

}

/**

* 函数说明：获得总行数

* 参数说明：

* 返回值：总行数

*/

    public int getRows() {

String sql="FROM Books ORDER BY bookName";

List list=this.getHibernateTemplate().find(sql);

return list.size();

}

/**

* 函数说明：获得所有的信息

* 参数说明：

* 返回值：信息的集合

*/

    public List getBooks(int pageSize, int startRow) throws HibernateException {

final int pageSize1=pageSize;

final int startRow1=startRow;

return this.getHibernateTemplate().executeFind(new HibernateCallback(){

public List doInHibernate(Session session) throws HibernateException, SQLException {

// TODO 自动生成方法存根

                Query query=session.createQuery("FROM Books ORDER BY bookName");

query.setFirstResult(startRow1);

query.setMaxResults(pageSize1);

return query.list();

}

});

}

/**

* 函数说明：获得一条的信息

* 参数说明： ID

* 返回值：对象

*/

    public Books getBook(String bookId) {

return (Books)this.getHibernateTemplate().get(Books.class,bookId);

}

/**

* 函数说明：获得最大ID

* 参数说明：

* 返回值：最大ID

*/

    public String getMaxID() {

String date=PublicUtil.getStrNowDate();

String sql="SELECT MAX(bookId)+1 FROM Books  ";

String noStr = null;

List ll = (List) this.getHibernateTemplate().find(sql);

Iterator itr = ll.iterator();

if (itr.hasNext()) {

Object noint = itr.next();

if(noint == null){

noStr = "1";

}else{

noStr = noint.toString();

}

}

if(noStr.length()==1){

noStr="000"+noStr;

}else if(noStr.length()==2){

noStr="00"+noStr;

}else if(noStr.length()==3){

noStr="0"+noStr;

}else{

noStr=noStr;

}

return noStr;

}

/**

* 函数说明：修改信息

* 参数说明： 对象

* 返回值：

*/

    public void updateBook(Books pd) {

this.getHibernateTemplate().update(pd);

}

/**

* 函数说明：查询信息

* 参数说明： 集合

* 返回值：

*/

    public List queryBooks(String fieldname,String value) {

System.out.println("value: "+value);

String sql="FROM Books where "+fieldname+" like '%"+value+"%'"+"ORDER BY bookName";

return this.getHibernateTemplate().find(sql);

}

/**

* 函数说明：获得总行数

* 参数说明：

* 返回值：总行数

*/

    public int getRows(String fieldname,String value) {

String sql="";

if(fieldname==null||fieldname.equals("")||fieldname==null||fieldname.equals(""))

sql="FROM Books ORDER BY bookName";

else

sql="FROM Books where "+fieldname+" like '%"+value+"%'"+"ORDER BY bookName";

List list=this.getHibernateTemplate().find(sql);

return list.size();

}

/**

* 函数说明：查询信息

* 参数说明： 集合

* 返回值：

*/

 

public List getBooks(String fieldname,String value,int pageSize, int startRow) {

final int pageSize1=pageSize;

final int startRow1=startRow;

final String queryName=fieldname;

final String queryValue=value;

String sql="";

if(queryName==null||queryName.equals("")||queryValue==null||queryValue.equals(""))

sql="FROM Books ORDER BY bookName";

else

sql="FROM Books where "+fieldname+" like '%"+value+"%'"+"ORDER BY bookName";

final String sql1=sql;

return this.getHibernateTemplate().executeFind(new HibernateCallback(){

public List doInHibernate(Session session) throws HibernateException, SQLException {

// TODO 自动生成方法存根

                Query query=session.createQuery(sql1);

query.setFirstResult(startRow1);

query.setMaxResults(pageSize1);

return query.list();

}

});

}

}

## 五、业务逻辑层

 

在业务逻辑层需要认真思考每个业务逻辑所能用到的持久层对象和DAO。DAO层之上是业务逻辑层，DAO类可以有很多个，但业务逻辑类应该只有一个，可以在业务逻辑类中调用各个DAO类进行操作。

1、创建服务接口类IBookService



package com.sterning.books.services.iface;



import java.util.List;



import com.sterning.books.model.Books;



public interface IBooksService ...{

    List getAll();//获得所有记录

    List getBooks(int pageSize, int startRow);//获得所有记录

    int getRows();//获得总行数

    int getRows(String fieldname,String value);//获得总行数

    List queryBooks(String fieldname,String value);//根据条件查询

    List getBooks(String fieldname,String value,int pageSize, int startRow);//根据条件查询

    Books getBook(String bookId);//根据ID获得记录

    String getMaxID();//获得最大ID值

    void addBook(Books pd);//添加记录

    void updateBook(Books pd);//修改记录

    void deleteBook(String bookId);//删除记录    

}

com.sterning.books.services.iface.IBookService.java



2、实现此接口类：BookService：

package com.sterning.books.services;

import java.util.List;

import com.sterning.books.dao.iface.BooksDao;

import com.sterning.books.model.Books;

import com.sterning.books.services.iface.IBooksService;

public class BooksService implements IBooksService{

private BooksDao booksDao;

public BooksService(){}

/**

* 函数说明：添加信息

* 参数说明：对象

* 返回值：

*/

    public void addBook(Books book) {

booksDao.addBook(book);

}

/**

* 函数说明：删除信息

* 参数说明： 对象

* 返回值：

*/

    public void deleteBook(String bookId) {

Books book=booksDao.getBook(bookId);

booksDao.deleteBook(book);

}

/**

* 函数说明：获得所有的信息

* 参数说明：

* 返回值：信息的集合

*/

    public List getAll() {

return booksDao.getAll();

}

/**

* 函数说明：获得总行数

* 参数说明：

* 返回值：总行数

*/

    public int getRows() {

return booksDao.getRows();

}

/**

* 函数说明：获得所有的信息

* 参数说明：

* 返回值：信息的集合

*/

    public List getBooks(int pageSize, int startRow) {

return booksDao.getBooks(pageSize, startRow);

}

/**

* 函数说明：获得一条的信息

* 参数说明： ID

* 返回值：对象

*/

    public Books getBook(String bookId) {

return booksDao.getBook(bookId);

}

/**

* 函数说明：获得最大ID

* 参数说明：

* 返回值：最大ID

*/

    public String getMaxID() {

return booksDao.getMaxID();

}

/**

* 函数说明：修改信息

* 参数说明： 对象

* 返回值：

*/

    public void updateBook(Books book) {

booksDao.updateBook(book);

}

/**

* 函数说明：查询信息

* 参数说明： 集合

* 返回值：

*/

    public List queryBooks(String fieldname,String value) {

return booksDao.queryBooks(fieldname, value);

}

/**

* 函数说明：获得总行数

* 参数说明：

* 返回值：总行数

*/

    public int getRows(String fieldname,String value) {

return booksDao.getRows(fieldname, value);

}

/**

* 函数说明：查询信息

* 参数说明： 集合

* 返回值：

*/

    public List getBooks(String fieldname,String value,int pageSize, int startRow) {

return booksDao.getBooks(fieldname, value,pageSize,startRow);

}

public BooksDao getBooksDao() {

return booksDao;

}

public void setBooksDao(BooksDao booksDao) {

this.booksDao = booksDao;

}

}



## 六、 创建Action类：BookAction 



有Struts 1.x经验的朋友都知道Action是Struts的核心内容，当然Struts 2.0也不例外。不过，Struts 1.x与Struts 2.0的Action模型很大的区别。



  

 Struts 1.x

 Stuts 2.0

 

接口

 必须继承org.apache.struts.action.Action或者其子类

 无须继承任何类型或实现任何接口

 

表单数据

表单数据封装在FormBean中

表单数据包含在Action中，通过Getter和Setter获取



1、建立BookAction类



package com.sterning.books.web.actions;



import java.util.Collection;

import com.sterning.books.model.Books;

import com.sterning.books.services.iface.IBooksService;

import com.sterning.commons.AbstractAction;

import com.sterning.commons.Pager;

import com.sterning.commons.PagerService;



public class BooksAction extends AbstractAction {

    

    private IBooksService booksService;

    private PagerService pagerService;

    private Books book;

    private Pager pager;

    protected Collection availableItems;

    protected String currentPage;

    protected String pagerMethod;

    protected String totalRows;

    protected String bookId;

    protected String queryName;

    protected String queryValue;

    protected String searchName;

    protected String searchValue;

    protected String queryMap;

    

    public String list() throws Exception {

        if(queryMap ==null||queryMap.equals("")){

            

        }else{

            String[] str=queryMap.split("~");

            this.setQueryName(str[0]);

            this.setQueryValue(str[1]);

        }

        

        System.out.println("asd"+this.getQueryValue());

        int totalRow=booksService.getRows(this.getQueryName(),this.getQueryValue());

        pager=pagerService.getPager(this.getCurrentPage(), this.getPagerMethod(), totalRow);

        this.setCurrentPage(String.valueOf(pager.getCurrentPage()));

        this.setTotalRows(String.valueOf(totalRow));

        availableItems=booksService.getBooks(this.getQueryName(),this.getQueryValue(),pager.getPageSize(), pager.getStartRow());

        

        this.setQueryName(this.getQueryName());

        this.setQueryValue(this.getQueryValue());

        

        this.setSearchName(this.getQueryName());

        this.setSearchValue(this.getQueryValue());

        

        return SUCCESS;         

    }

    

    public String load() throws Exception {

        if(bookId!=null)

            book = booksService.getBook(bookId);

        else

            bookId=booksService.getMaxID();

        return SUCCESS;

    }

    

    public String save() throws Exception {

        if(this.getBook().getBookPrice().equals("")){

            this.getBook().setBookPrice("0.0");

        }

        

        String id=this.getBook().getBookId();

        Books book=booksService.getBook(id);

        

        

        

        if(book == null)

            booksService.addBook(this.getBook());

        else

            booksService.updateBook(this.getBook());

        

        this.setQueryName(this.getQueryName());

        this.setQueryValue(this.getQueryValue());

        

        if(this.getQueryName()==null||this.getQueryValue()==null||this.getQueryName().equals("")||this.getQueryValue().equals("")){

            

        }else{

            queryMap=this.getQueryName()+"~"+this.getQueryValue();

        }        

        

        return SUCCESS;

    }

    

    public String delete() throws Exception {

        booksService.deleteBook(this.getBookId());

        

        if(this.getQueryName()==null||this.getQueryValue()==null||this.getQueryName().equals("")||this.getQueryValue().equals("")){

            

        }else{

            queryMap=this.getQueryName()+"~"+this.getQueryValue();

        }

        return SUCCESS;

    }    

    

    public Books getBook() {

        return book;

    }



    public void setBook(Books book) {

        this.book = book;

    }



    public IBooksService getBooksService() {

        return booksService;

    }



    public void setBooksService(IBooksService booksService) {

        this.booksService = booksService;

    }



    public Collection getAvailableItems() {

        return availableItems;

    }



    public String getCurrentPage() {

        return currentPage;

    }



    public void setCurrentPage(String currentPage) {

        this.currentPage = currentPage;

    }



    public String getPagerMethod() {

        return pagerMethod;

    }



    public void setPagerMethod(String pagerMethod) {

        this.pagerMethod = pagerMethod;

    }



    public Pager getPager() {

        return pager;

    }



    public void setPager(Pager pager) {

        this.pager = pager;

    }



    public String getTotalRows() {

        return totalRows;

    }



    public void setTotalRows(String totalRows) {

        this.totalRows = totalRows;

    }

        

    public String getBookId() {

        return bookId;

    }



    public void setBookId(String bookId) {

        this.bookId = bookId;

    }



    public String getQueryName() {

        return queryName;

    }



    public void setQueryName(String queryName) {

        this.queryName = queryName;

    }



    public String getQueryValue() {

        return queryValue;

    }



    public void setQueryValue(String queryValue) {

        this.queryValue = queryValue;

    }

    

    public String getSearchName() {

        return searchName;

    }



    public void setSearchName(String searchName) {

        this.searchName = searchName;

    }



    public String getSearchValue() {

        return searchValue;

    }



    public void setSearchValue(String searchValue) {

        this.searchValue = searchValue;

    }

    

    public String getQueryMap() {

        return queryMap;

    }



    public void setQueryMap(String queryMap) {

        this.queryMap = queryMap;

    }

    

    public PagerService getPagerService() {

        return pagerService;

    }



    public void setPagerService(PagerService pagerService) {

        this.pagerService = pagerService;

    }    

}



com.sterning.books.web.actions.BookAction.java



（1）、默认情况下，当请求bookAction.action发生时(这个会在后面的Spring配置文件中见到的)，Struts运行时（Runtime）根据struts.xml里的Action映射集(Mapping)，实例化com.sterning.books.web.actions.BookAction类，并调用其execute方法。当然，我们可以通过以下两种方法改变这种默认调用。这个功能（Feature）有点类似Struts 1.x中的LookupDispathAction。



在classes/sturts.xml中新建Action，并指明其调用的方法；



访问Action时，在Action名后加上“!xxx”（xxx为方法名）。



（2）、细心的朋友应该可能会发现com.sterning.books.web.actions.BookAction.java中Action方法（execute）返回都是SUCCESS。这个属性变量我并没有定义，所以大家应该会猜到它在ActionSupport或其父类中定义。没错，SUCCESS在接口com.opensymphony.xwork2.Action中定义，另外同时定义的还有ERROR, INPUT, LOGIN, NONE。



此外，我在配置Action时都没有为result定义名字（name），所以它们默认都为success。值得一提的是Struts 2.0中的result不仅仅是Struts 1.x中forward的别名，它可以实现除forward外的很激动人心的功能，如将Action输出到FreeMaker模板、Velocity模板、JasperReports和使用XSL转换等。这些都过result里的type（类型）属性（Attribute）定义的。另外，您还可以自定义result类型。



（3）、使用Struts 2.0，表单数据的输入将变得非常方便，和普通的POJO一样在Action编写Getter和Setter，然后在JSP的UI标志的name与其对应，在提交表单到Action时，我们就可以取得其值。



（4）、Struts 2.0更厉害的是支持更高级的POJO访问，如this.getBook().getBookPrice()。private Books book所引用的是一个关于书的对象类，它可以做为一个属性而出现在BookActoin.java类中。这样对我们开发多层系统尤其有用。它可以使系统结构更清晰。



（5）、有朋友可能会这样问：“如果我要取得Servlet API中的一些对象，如request、response或session等，应该怎么做？这里的execute不像Struts 1.x的那样在参数中引入。”开发Web应用程序当然免不了跟这些对象打交道。在Strutx 2.0中可以有两种方式获得这些对象：非IoC（控制反转Inversion of Control）方式和IoC方式。



非IoC方式



要获得上述对象，关键是Struts 2.0中com.opensymphony.xwork2.ActionContext类。我们可以通过它的静态方法getContext()获取当前Action的上下文对象。另外，org.apache.struts2.ServletActionContext作为辅助类（Helper Class），可以帮助您快捷地获得这几个对象。



HttpServletRequest request = ServletActionContext.getRequest(); 



HttpServletResponse response = ServletActionContext.getResponse(); 



HttpSession session = request.getSession();



如果你只是想访问session的属性（Attribute），你也可以通过ActionContext.getContext().getSession()获取或添加session范围（Scoped）的对象。



IoC方式



要使用IoC方式，我们首先要告诉IoC容器（Container）想取得某个对象的意愿，通过实现相应的接口做到这点。如实现SessionAware, ServletRequestAware, ServletResponseAware接口，从而得到上面的对象。



1、对BookAction类的Save方法进行验证



正如《Writing Secure Code》文中所写的名言All input is evil：“所有的输入都是罪恶的”，所以我们应该对所有的外部输入进行校验。而表单是应用程序最简单的入口，对其传进来的数据，我们必须进行校验。Struts2的校验框架十分简单方便，只在如下两步：



在Xxx-validation.xml文件中的<message>元素中加入key属性；



在相应的jsp文件中的<s:form>标志中加入validate="true"属性，就可以在用Javascript在客户端校验数据。



其验证文件为：BooksAction-save-validation.xml



<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE validators PUBLIC "-//OpenSymphony Group//XWork Validator 1.0//EN" "http://www.opensymphony.com/xwork/xwork-validator-1.0.dtd">

<validators>

    <!-- Field-Validator Syntax -->

    <field name="book.bookName">

        <field-validator type="requiredstring">

            <message key="book.bookName.required"/>

        </field-validator>

    </field>

    <field name="book.bookAuthor">

        <field-validator type="requiredstring">

            <message key="book.bookAuthor.required"/>

        </field-validator>

    </field>

    <field name="book.bookPublish">

        <field-validator type="requiredstring">

            <message key="book.bookPublish.required"/>

        </field-validator>

    </field>

</validators>

 com.sterning.books.web.actions.BooksAction-save-validation.xml 

1、对BookAction类的Save方法进行验证的资源文件



       注意配置文件的名字应该是：配置文件（类名-validation.xml）的格式。BooksAction类的验证资源文件为：BooksAction.properties



book=Books

book.bookName.required=\u8bf7\u8f93\u5165\u4e66\u540d

book.bookAuthor.required=\u8bf7\u8f93\u5165\u4f5c\u8005

book.bookPublish.required=\u8bf7\u8f93\u5165\u51fa\u7248\u793e

format.date={0,date,yyyy-MM-dd}



com.sterning.books.web.actions.BooksAction.properties



       资源文件的查找顺序是有一定规则的。之所以说Struts 2.0的国际化更灵活是因为它可以根据不同需要配置和获取资源（properties）文件。在Struts 2.0中有下面几种方法：



（1）、使用全局的资源文件。这适用于遍布于整个应用程序的国际化字符串，它们在不同的包（package）中被引用，如一些比较共用的出错提示；



（2）、使用包范围内的资源文件。做法是在包的根目录下新建名的package.properties和package_xx_XX.properties文件。这就适用于在包中不同类访问的资源；



（3）、使用Action范围的资源文件。做法为Action的包下新建文件名（除文件扩展名外）与Action类名同样的资源文件。它只能在该Action中访问。如此一来，我们就可以在不同的Action里使用相同的properties名表示不同的值。例如，在ActonOne中title为“动作一”，而同样用title在ActionTwo表示“动作二”，节省一些命名工夫；



（4）、使用<s:i18n>标志访问特定路径的properties文件。在使用这一方法时，请注意<s:i18n>标志的范围。在<s:i18n name="xxxxx">到</s:i18n>之间，所有的国际化字符串都会在名为xxxxx资源文件查找，如果找不到，Struts 2.0就会输出默认值（国际化字符串的名字）。



例如：某个ChildAction中调用了getText("user.title")，Struts 2.0的将会执行以下的操作：



查找ChildAction_xx_XX.properties文件或ChildAction.properties；



查找ChildAction实现的接口，查找与接口同名的资源文件MyInterface.properties；



查找ChildAction的父类ParentAction的properties文件，文件名为ParentAction.properties；



判断当前ChildAction是否实现接口ModelDriven。如果是，调用getModel()获得对象，查找与其同名的资源文件；



查找当前包下的package.properties文件；



查找当前包的父包，直到最顶层包；



在值栈（Value Stack）中，查找名为user的属性，转到user类型同名的资源文件，查找键为title的资源; 



查找在struts.properties配置的默认的资源文件，参考例1; 



输出user.title。



## 七、 Web页面



在这一节中，主要使用到了Struts2的标签库。在这里，会对所用到的主要标签做一个初步的介绍。更多的知识请读者访问Struts的官方网站做更多的学习。在编写Web页面之前，先从总体上，对Struts 1.x与Struts 2.0的标志库（Tag Library）作比较。



 Struts 1.x

 Struts 2.0

 

分类

 将标志库按功能分成HTML、Tiles、Logic和Bean等几部分

 严格上来说，没有分类，所有标志都在URI为“/struts-tags”命名空间下，不过，我们可以从功能上将其分为两大类：非UI标志和UI标志

 

表达式语言（expression languages）

 不支持嵌入语言（EL）

 OGNL、JSTL、Groovy和Velcity



1、主页面：index.jsp，其代码如下：



<%@page pageEncoding="UTF-8" contentType="text/html; charset=UTF-8" %>

<%@ taglib prefix="s" uri="/struts-tags" %>

<html>

<head>

<meta http-equiv="Content-Type" content="text/html; charset=GBK"/>

<title>图书管理系统</title>

</head>

<body>

<p><a href="<s:url action="list" />">进入图书管理系统</a></p>

</body>

</html>



WebRoot/index.jsp



要在JSP中使用Struts 2.0标志，先要指明标志的引入。通过在JSP的代码的顶部加入以下代码可以做到这点。<%@taglib prefix="s" uri="/struts-tags" %>



1、<s:url>标签：该标签用于创建url,可以通过"param"标签提供request参数。当includeParams的值时'all'或者'get', param标签中定义的参数将有优先权,也就是说其会覆盖其他同名参数的值。



2、列表页面：list.jsp



<%@page pageEncoding="gb2312" contentType="text/html; charset=UTF-8" %>

<%@ taglib prefix="s" uri="/struts-tags" %>



<html>

<head><title>图书管理系统</title></head>

    <style type="text/css">

        table {

            border: 1px solid black;

            border-collapse: collapse;

        }

        

        table thead tr th {

            border: 1px solid black;

            padding: 3px;

            background-color: #cccccc;

            background-color: expression(this.rowIndex % 2 == 0 ? "#FFFFFF" : "#EEEEEE");

        }

        

        table tbody tr td {

            border: 1px solid black;

            padding: 3px;

        }

        .trs{

            background-color: expression(this.rowIndex % 2 == 0 ? "#FFFFFF" : "#EEEEEE");

        }

    </style>



    <script language="JavaScript">   

        function doSearch(){

            if(document.all.searchValue.value=="")

            {    

                alert("请输入查询关键字!");

            }else{

                window.location.href="bookAdmin/list.action?queryName="+document.all.searchName.value+"&&queryValue="+document.all.searchValue.value;

             }

        }

    </script>

<body>



<table align="center">

<tr align="center">

    <td>

        <select name="searchName">

            <option value="bookName">书名</option>

            <option value="bookAuthor">作者</option>

            <option value="bookPublish">出版社</option>

            <option value="bookDate">出版日期</option>

            <option value="bookIsbn">ISNB</option>

            <option value="bookPage">页数</option>

        </select>

        <input type="text" name="searchValue" value="" size="10"/>

        <input type="button" value="查询" onClick="doSearch();">

    </td>

</tr>

<tr align="center">    

    <td>

        <a href="<s:url action="list" includeParams="none"/>">全部</a>

        <a href='<s:url action="edit" ></s:url>'>增加</a>

    </td>

</tr>

<tr>

<td>

<table cellspacing="0" align="center">

    <thead>

    <tr>

        <th>书名</th>

        <th>作者</th>

        <th>出版社</th>

        <th>出版日期</th>

        <th>ISNB</th>

        <th>页数</th>

        <th>价格</th>

        <th>内容提要</th>

        <th>删除</th>

    </tr>

    </thead>

    <tbody>

    <s:iterator value="availableItems">

        <tr class="trs">

            <td>

            <a href='<s:url action="edit" ><s:param name="bookId" value="bookId" /></s:url>'>

            <s:property value="bookName"/>

            </a>

            </td>

            <td><s:property value="bookAuthor"/></td>

            <td><s:property value="bookPublish"/></td>

            <td><s:text name="format.date"><s:param value="bookDate"/></s:text></td>     

            <td><s:property value="bookIsbn" /></td>

            <td><s:property value="bookPage" /></td>

            <td><s:property value="bookPrice"/></td>

            <td><s:property value="bookContent"/></td>

            

            <td><a href='<s:url action="delete"><s:param name="bookId" value="bookId" /></s:url>'>删除</a></td>

        </tr>

    </s:iterator>

    <tr align="right">

        <td colspan="9">

            共<s:property value="totalRows"/>行&nbsp;

            第<s:property value="currentPage"/>页&nbsp;

            共<s:property value="pager.getTotalPages()"/>页&nbsp;

            <a href="<s:url value="list.action">

                <s:param name="currentPage" value="currentPage"/>

                <s:param name="pagerMethod" value="'first'"/>

                

            </s:url>">首页</a>

            <a href="<s:url value="list.action">

                <s:param name="currentPage" value="currentPage"/>

                <s:param name="pagerMethod" value="'previous'"/>

            </s:url>">上一页</a>

            <a href="<s:url value="list.action">

                <s:param name="currentPage" value="currentPage"/>

                <s:param name="pagerMethod" value="'next'"/>

            </s:url>">下一页</a>

            <a href="<s:url value="list.action">

                <s:param name="currentPage" value="currentPage"/>

                <s:param name="pagerMethod" value="'last'"/>

            </s:url>">尾页</a>

        </td>

    </tr>    

    </tbody>

</table>

</td>

</tr>

</table>

</body>

</html>



/WebRoot/list.jsp



(1)、<s:property> :得到'value'的属性,如果value没提供,默认为堆栈顶端的元素。其相关的参数及使用如下表所示：



名称

 必需

 默认

 类型

 描述

 

default

 否

  String

 如果属性是null则显示的default值

 

escape

 否

 true

 Booelean

 是否escape HTML

 

value

 否

 栈顶

 Object

 要显示的值

 

id

 否

  Object/String

 用来标识元素的id。在UI和表单中为HTML的id属性

 



(2)、<s:Iterator>：用于遍历集合（java.util.Collection）或枚举值（java.util.Iterator）。其相关的参数及使用如下表所示：  



名称

 必需

 默认

 类型

 描述

 

status

 否

  String

 如果设置此参数，一个IteratorStatus的实例将会压入每个遍历的堆栈

 

value

 否

  Object/String

 要遍历的可枚举的（iteratable）数据源，或者将放入新列表（List）的对象

 

id

 否

  Object/String

 用来标识元素的id。在UI和表单中为HTML的id属性

 



(3)、<s:param>:为其他标签提供参数,比如include标签和bean标签. 参数的name属性是可选的,如果提供，会调用Component的方法addParameter(String, Object), 如果不提供，则外层嵌套标签必须实现UnnamedParametric接口(如TextTag)。 value的提供有两种方式,通过value属性或者标签中间的text,不同之处我们看一下例子:



<param name="color">blue</param><!-- (A) -->



<param name="color" value="blue"/><!-- (B) -->

(A)参数值会以String的格式放入statck. 

(B)该值会以java.lang.Object的格式放入statck.



其相关的参数及使用如下表所示：



名称

 必需

 默认

 类型

 描述

 

name

 否

  String

 参数名

 

value

 否

  String

 value表达式

 

id

 否

  Object/String

 用来标识元素的id。在UI和表单中为HTML的id属性

 



（4）、国际化是商业系统中不可或缺的一部分，所以无论您学习的是什么Web框架，它都是必须掌握的技能。其实，Struts 1.x在此部分已经做得相当不错了。它极大地简化了我们程序员在做国际化时所需的工作，例如，如果您要输出一条国际化的信息，只需在代码包中加入FILE-NAME_xx_XX.properties（其中FILE-NAME为默认资源文件的文件名），然后在struts-config.xml中指明其路径，再在页面用<bean:message>标志输出即可。



不过，所谓“没有最好，只有更好”。Struts 2.0并没有在这部分止步，而是在原有的简单易用的基础上，将其做得更灵活、更强大。



（5）、list.jsp文件中：



<s:text name="format.date"><s:param value="bookDate"/></s:text>，为了正确的输出出版日期的格式，采用在资源文件中定义输出的格式，并在页面上调用。format.date就是在资源文件com.sterning.books.web.actions.BooksAction.properties中定义。当然也可以别的文件，放在别的路径下，但此时需要在web.xml中注册才可以使用它。



正如读者所见，在pojo（本例为Books.java）中将日期字段设置为java.util.Date，在映射文件中（books.hbm.xml）设置为timestamp（包括日期和时间）。为了便于管理，将日期格式保存在国际化资源文件中。如：globalMessages或globalMessages_zh_CN文件。



其内容为：



format.date={0,date,yyyy-MM-dd}



在页面显示日期时间时：<s:text name="format.date"><s:param value="bookDate"/></s:text>。这样就解决了日期（时间）的显示格式化问题。



3、增加/修改页面：editBook.jsp  



<%@page pageEncoding="UTF-8" contentType="text/html; charset=UTF-8" %>

<%@ taglib prefix="s" uri="/struts-tags" %>



<html>

<head>

    <title>编辑图书</title>

    <s:head/>

</head>

<body>

    <h2>

        <s:if test="null == book">

            增加图书

        </s:if>

        <s:else>

            编辑图书

        </s:else>

    </h2>

    <s:form name="editForm" action="save" validate="true">

    

         <s:textfield label="书名" name="book.bookName"/>

         <s:textfield label="作者" name="book.bookAuthor"/>

         <s:textfield label="出版社" name="book.bookPublish"/>

         <s:datetimepicker label="出版日期" name="book.bookDate"></s:datetimepicker>

         <s:textfield label="ISBN" name="book.bookIsbn"/>

         <s:textfield label="页数" name="book.bookPage"/>

         <s:textfield label="价格(元)" name="book.bookPrice"/>

         <s:textfield label="内容摘要" name="book.bookContent"/>

         <s:if test="null == book">

             <s:hidden name="book.bookId" value="%{bookId}"/>

         </s:if>         

         <s:else>

             <s:hidden name="book.bookId" />

         </s:else>

         <s:hidden name="queryName" />

         <s:hidden name="queryValue" />

         <s:submit value="%{getText('保存')}" />

    </s:form>



<p><a href="<s:url action="list"/>">返回</a></p>

</body>

</html>



WebRoot/editBook.jsp



（1）、<s:if>、<s:elseif>和<s:else> ：执行基本的条件流转。 其相关的参数及使用如下表所示：



名称

 必需

 默认

 类型

 描述

 备注

 

test

 是

  

 Boolean

 决定标志里内容是否显示的表达式

 else标志没有这个参数

 

id

 否

  

 Object/String

 用来标识元素的id。在UI和表单中为HTML的id属性

  



（2）、<s:text>：支持国际化信息的标签。国际化信息必须放在一个和当前action同名的resource bundle中,如果没有找到相应message,tag body将被当作默认message,如果没有tag body,message的name会被作为默认message。 其相关的参数及使用如下表所示：



名称

 必需

 默认

 类型

 描述

 

name

 是

  

 String

 资源属性的名字

 

id

 否

  

 Object/String

 用来标识元素的id。在UI和表单中为HTML的id属性 

 

## 八、  配置Struts2



Struts的配置文件都会在web.xml中注册的。



a)   Struts的配置文件如下：



<?xml version="1.0" encoding="UTF-8" ?>

<!DOCTYPE struts PUBLIC

    "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"

    "http://struts.apache.org/dtds/struts-2.0.dtd">



<struts>



    <constant name="struts.enable.DynamicMethodInvocation" value="false" />

    <constant name="struts.devMode" value="true" />

    <constant name="struts.i18n.encoding" value="GBK" />   



    <!-- Add packages here -->



</struts>



Src/struts.xml



b)   struts_book.xml配置文件如下：



<?xml version="1.0" encoding="UTF-8" ?>

<!DOCTYPE struts PUBLIC

        "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"

        "http://struts.apache.org/dtds/struts-2.0.dtd">



<struts>



    <package name="products" extends="struts-default">

        <!--default-interceptor-ref name="validation"/-->

         <!-- Add actions here -->

        <action name="list" class="bookAction" method="list">            

            <result>/list.jsp</result>

        </action>



    <action name="delete" class="bookAction" method="delete">            

            <result type="redirect">list.action?queryMap=${queryMap}</result>

        </action>



        <action name="*" class="com.sterning.commons.AbstractAction">

            <result>/{1}.jsp</result>

        </action>

        

    <action name="edit" class="bookAction" method="load">

            <result>/editBook.jsp</result>

        </action>

       

       <action name="save" class="bookAction" method="save">

           <interceptor-ref name="params"/>

           <interceptor-ref name="validation"/>

            <result name="input">/editBook.jsp</result>

            <result type="redirect">list.action?queryMap=${queryMap}</result>

              

        </action>

    </package>

</struts>

文件中的<interceptor-ref name="params"/>，使用了struts2自己的拦截器，拦截器在AOP（Aspect-Oriented Programming）中用于在某个方法或字段被访问之前，进行拦截然后在之前或之后加入某些操作。拦截是AOP的一种实现策略。



Struts 2已经提供了丰富多样的，功能齐全的拦截器实现。大家可以到struts2-all-2.0.6.jar或struts2-core-2.0.6.jar包的struts-default.xml查看关于默认的拦截器与拦截器链的配置。



在struts-default.xml中已经配置了大量的拦截器。如果您想要使用这些已有的拦截器，只需要在应用程序struts.xml文件中通过“<include file="struts-default.xml" />”将struts-default.xml文件包含进来，并继承其中的struts-default包（package），最后在定义Action时，使用“<interceptor-ref name="xx" />”引用拦截器或拦截器栈（interceptor stack）。一旦您继承了struts-default包（package），所有Action都会调用拦截器栈 ——defaultStack。当然，在Action配置中加入“<interceptor-ref name="xx" />”可以覆盖defaultStack。



作为“框架（framework）”，可扩展性是不可或缺的，因为世上没有放之四海而皆准的东西。虽然，Struts 2为我们提供如此丰富的拦截器实现，但是这并不意味我们失去创建自定义拦截器的能力，恰恰相反，在Struts 2自定义拦截器是相当容易的一件事。所有的Struts 2的拦截器都直接或间接实现接口com.opensymphony.xwork2.interceptor.Interceptor。除此之外，大家可能更喜欢继承类com.opensymphony.xwork2.interceptor.AbstractInterceptor。



## 九、 配置Spring



1、Spring的配置文件如下：



<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">

 

<beans>

    <!-- dataSource config -->

    <bean id ="dataSource" class ="org.apache.commons.dbcp.BasicDataSource" destroy-method="close"> 

        <property name="driverClassName" value="com.mysql.jdbc.Driver" /> 

        <property name="url" value="jdbc:mysql://localhost:3306/game" /> 

        <property name="username" value="root" /> 

        <property name="password" value="root"/> 

    </bean> 

    

    <!-- SessionFactory -->

    <bean id="sessionFactory"

        class="org.springframework.orm.hibernate3.LocalSessionFactoryBean">



        <property name="dataSource">

            <ref bean="dataSource"/>

        </property>

        <property name="configLocation">

            <value>classpath:com\sterning\bean\hibernate\hibernate.cfg.xml</value>

        </property>        

    </bean>

    

    <!-- TransactionManager  不过这里暂时没注入-->

    <bean id="transactionManager"

        class="org.springframework.orm.hibernate3.HibernateTransactionManager">

        <property name="sessionFactory">

            <ref local="sessionFactory"/>

        </property>

    </bean>

    

    <!-- DAO -->

    <bean id="booksDao" class="com.sterning.books.dao.hibernate.BooksMapDao">

        <property name="sessionFactory">

            <ref bean="sessionFactory"/>

        </property>

    </bean>

    

    <!-- Services -->

    <bean id="booksService" class="com.sterning.books.services.BooksService">

        <property name="booksDao">

            <ref bean="booksDao"/>

        </property>

    </bean>

    

    <bean id="pagerService" class="com.sterning.commons.PagerService"/>

    

    <!-- view -->

    <bean id="bookAction" class="com.sterning.books.web.actions.BooksAction" singleton="false">

        <property name="booksService">

            <ref bean="booksService"/>

        </property>

        <property name="pagerService">

            <ref bean="pagerService"/>

        </property>

    </bean>  

    

</beans>



  WebRoot/WEB-INF/srping-content/applicationContent.xml 

2、Struts.properties.xml



本来此文件应该写在struts 配置一节，但主要是考虑这体现了集成spring的配置，所以放在spring的配置这里来讲。



struts.objectFactory = spring  

struts.locale=zh_CN

struts.i18n.encoding = GBK

struts.objectFacto：ObjectFactory 实现了 com.opensymphony.xwork2.ObjectFactory接口（spring）。struts.objectFactory=spring，主要是告知Struts 2运行时使用Spring来创建对象（如Action等）。当然，Spring的ContextLoaderListener监听器，会在web.xml文件中编写，负责Spring与Web容器交互。

struts.locale：The default locale for the Struts application。 默认的国际化地区信息。

struts.i18n.encoding：国际化信息内码。



## 十、Web.xml配置



<?xml version="1.0" encoding="GB2312"?>

<!DOCTYPE web-app

    PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"

    "http://java.sun.com/dtd/web-app_2_3.dtd">



<web-app>

    <display-name>图书管理系统</display-name>

    <context-param>

        <param-name>log4jConfigLocation</param-name>

        <param-value>/WEB-INF/classes/log4j.properties</param-value>

    </context-param>

    <!-- ContextConfigLocation -->

    <context-param>

        <param-name>contextConfigLocation</param-name>

        <param-value>/WEB-INF/spring-context/applicationContext.xml</param-value>

      </context-param>

    

    <filter>

        <filter-name>encodingFilter</filter-name>

        <filter-class>com.sterning.commons.SetCharacterEncodingFilter</filter-class>

        <init-param>

            <param-name>encoding</param-name>

            <param-value>UTF-8</param-value>

        </init-param>

        <init-param>

            <param-name>forceEncoding</param-name>

            <param-value>true</param-value>

        </init-param>

    </filter>

     <filter>

        <filter-name>struts2</filter-name>

        <filter-class>org.apache.struts2.dispatcher.FilterDispatcher</filter-class>

        <init-param>

            <param-name>config</param-name>

            <param-value>struts-default.xml,struts-plugin.xml,struts.xml,struts_books.xml</param-value>

        </init-param>

    </filter>    



    <filter-mapping>

        <filter-name>encodingFilter</filter-name>

        <url-pattern>/*</url-pattern>

    </filter-mapping>

    <filter-mapping>

        <filter-name>struts2</filter-name>

        <url-pattern>/*</url-pattern>

    </filter-mapping>        

    

    <!-- Listener contextConfigLocation -->

      <listener>

        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>

      </listener>

    <!-- Listener log4jConfigLocation -->

      <listener>

        <listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>

      </listener>

 

    <!-- The Welcome File List -->

    <welcome-file-list>

        <welcome-file>index.jsp</welcome-file>

    </welcome-file-list>

</web-app>



public void setQueryName(String queryName) {

this.queryName = queryName;

}

public String getQueryValue() {

return queryValue;

}

public void setQueryValue(String queryValue) {

this.queryValue = queryValue;

}

public String getSearchName() {

return searchName;

}

public void setSearchName(String searchName) {

this.searchName = searchName;

}

public String getSearchValue() {

return searchValue;

}

public void setSearchValue(String searchValue) {

this.searchValue = searchValue;

}

public String getQueryMap() {

return queryMap;

}

public void setQueryMap(String queryMap) {

this.queryMap = queryMap;

}

public PagerService getPagerService() {

return pagerService;

}

public void setPagerService(PagerService pagerService) {

this.pagerService = pagerService;

}

}



com.sterning.books.web.actions.BookAction.java



（1）、默认情况下，当请求bookAction.action发生时(这个会在后面的Spring配置文件中见到的)，Struts运行时（Runtime）根据struts.xml里的Action映射集(Mapping)，实例化com.sterning.books.web.actions.BookAction类，并调用其execute方法。当然，我们可以通过以下两种方法改变这种默认调用。这个功能（Feature）有点类似Struts 1.x中的LookupDispathAction。



在classes/sturts.xml中新建Action，并指明其调用的方法；

访问Action时，在Action名后加上“!xxx”（xxx为方法名）。



（2）、细心的朋友应该可能会发现com.sterning.books.web.actions.BookAction.java中Action方法（execute）返回都是SUCCESS。这个属性变量我并没有定义，所以大家应该会猜到它在ActionSupport或其父类中定义。没错，SUCCESS在接口com.opensymphony.xwork2.Action中定义，另外同时定义的还有ERROR, INPUT, LOGIN, NONE。



此外，我在配置Action时都没有为result定义名字（name），所以它们默认都为success。值得一提的是Struts 2.0中的result不仅仅是Struts 1.x中forward的别名，它可以实现除forward外的很激动人心的功能，如将Action输出到FreeMaker模板、Velocity模板、JasperReports和使用XSL转换等。这些都过result里的type（类型）属性（Attribute）定义的。另外，您还可以自定义result类型。



（3）、使用Struts 2.0，表单数据的输入将变得非常方便，和普通的POJO一样在Action编写Getter和Setter，然后在JSP的UI标志的name与其对应，在提交表单到Action时，我们就可以取得其值。



（4）、Struts 2.0更厉害的是支持更高级的POJO访问，如this.getBook().getBookPrice()。private Books book所引用的是一个关于书的对象类，它可以做为一个属性而出现在BookActoin.java类中。这样对我们开发多层系统尤其有用。它可以使系统结构更清晰。

（5）、有朋友可能会这样问：“如果我要取得Servlet API中的一些对象，如request、response或session等，应该怎么做？这里的execute不像Struts 1.x的那样在参数中引入。”开发Web应用程序当然免不了跟这些对象打交道。在Strutx 2.0中可以有两种方式获得这些对象：非IoC（控制反转Inversion of Control）方式和IoC方式。

# struts2修改struts.xml路径，web.xml中怎么配置才能用？

struts.xml路径为：

WebRoot/config/struts/struts.xml



web.xml写成这样对吗？

	<filter>

		<filter-name>struts2</filter-name>

		<filter-class>org.apache.struts2.dispatcher.FilterDispatcher</filter-class>

			<init-param>   

				<param-name>config</param-name>   

				<param-value>

					struts-default.xml,

					struts-plugin.xml,

					/config/struts/struts2.xml

				</param-value>

			</init-param> 

	</filter>

	<filter-mapping>

		<filter-name>struts2</filter-name>

		<url-pattern>/*</url-pattern>

	</filter-mapping>

如果你的struts.xml路径为：

WebRoot/config/struts/struts.xml



可以这样写

<param-value>

struts-default.xml,

struts-plugin.xml,

../config/struts/struts2.xml

</param-value>  

如果不对请把struts.xml路径改为：WebRoot/web-inf/config/struts/struts.xml



提供另一种方法

假设你的工程下有 admin 和common两个包

common为公共包，包下存放structs.xml 你需要写

<struts>

	<package name="common" extends="struts-default">

                <include file="struts-admin.xml" />

</struts>	



admin  为管理员包，包下存放struts-admin.xml你需要写

<struts>

<package name="admin" extends="common">

</struts>

# struts2关于A web application created a ThreadLocal with key of type 异常解决办法

今天开始学习了struts2， 于是下了最新的版本struts2.2.3.1,在使用的过程中总是报错：A web application created a ThreadLocal with key of type ， 尽管出现了这个错误，但是并不妨碍程序正常运行， 虽然程序虽然能正常运行，但是看的这个错误很是别扭，所以网上搜了一下看看，也就有了下面这篇文章

struts2关于A web application created a ThreadLocal with key of type 异常解决办法 

 



created a ThreadLocal with key of type [com.opensymphony.xwork2.inject.ContainerImpl$10] (value [com.opensymphony.xwork2.inject.ContainerImpl$10@12c74b9]) and a value of type [java.lang.Object[]] (value [[Ljava.lang.Object;@1a34544]) but failed to remove it。。。。



这类问题的解决办法：



       http://confluence.atlassian.com/pages/viewpage.action?pageId=218275753



看看老外的这篇，好像就是在讲这个问题，原因大概是说tomcat 6.025之后引入了一种内存泄露的检查机制，会把不能垃圾收集的对像做日志。



第一种解决办法：



使用低于6版本的tomcat



第二种解决办法：



在tomcat的server.xml文件（在tomcat的安装路径下的conf文件夹里）中把



<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>



这个监听给关了。



就是用<!--。。。-->把下面三句话括起来就可以啦。



<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />

       <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />

       <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

# Web.xml中设置Servlet和Filter时的url-pattern匹配规则

之前一直都对配置文件里面的路径和通配符不是很熟悉，都是复制之前项目里面的，错了就试探性的微调一下，现在专门花点时间整理一下，梳理一下杂乱 无章的知识。

 

一、servlet容器对url的匹配过程：

当一个请求发送到servlet容器的时候，容器先会将请求的url减去当前应用上下文的路径作为servlet的映射url，比如我访问的是http://localhost/test/aaa.html（我的应用上下文是test），容器会将http://localhost/tes去掉，将剩下的/aaa.html部分拿来做servlet的映射匹配，也就是拿这剩下的部分与web.xml中配置的servlet的url-pattern进行匹配。注意：这个映射匹配过程是有一定的规则的，而且每次匹配最终都只匹配一个 servlet。（这一点和filter不同）

 

匹配规则如下：（它的匹配原则就是：找到唯一一个最适合的Servlet）

1. 精确路径匹配。

例子：比如servletA的url-pattern为 /test，servletB的url-pattern为 /* ，这个时候，如果我访问的url为http://localhost/test ，这个时候容器就会先 进行精确路径匹配，发现/test正好被servletA精确匹配，那么就去调用servletA，也不会去理会其他的servlet了。

 

2. 最长路径匹配。

例子：servletA的url-pattern为/test/*，而servletB的url-pattern为/test/a/*，此时访问http://localhost/test/a时，容器会选择路径最长的servlet来匹配，也就是这里的servletB。

 

3. 扩展匹配。

如果url最后一段包含扩展，容器将会根据扩展选择合适的servlet。例子：servletA的url-pattern：*.action（/test/*.action为不合法的url-pattern）

 

4. 如果前面三条规则都没有找到一个servlet，容器会根据url选择对应的请求资源。如果应用定义了一个default servlet，则容器会将请求丢给default servlet（什么是defaultservlet？后面会讲）。

对于filter，不会像servlet那样只匹配一个servlet，因为filter的集合是一个链，所以只会有处理的顺序不同，而不会出现只选择一个filter。Filter的处理顺序和filter-mapping在web.xml中定义的顺序相同。

 

二、url-pattern详解

在web.xml文件中，以下语法用于定义映射：

① 以”/’开头和以”/*”结尾的是用来做路径映射的。

② 以前缀”*.”开头的是用来做扩展映射的。

③ “/” 是用来定义default servlet映射的。

④ 剩下的都是用来定义详细映射的。比如： /aa/bb/cc.action

所以，为什么定义”/*.action”这样一个看起来很正常的匹配会错？因为这个匹配即属于路径映射，也属于扩展映射，导致容器无法判断。



# 检查错误链接

直接查看代码或者使用浏览器debug

JSP 里外部引用CSS样式的路径问题   .

我的工程目录

/WebRoot/manage/css

/WebRoot/manage/js

/WebRoot/manage/images

/WebRoot/manage/mian.jsp

 

 

我之前在 mian.jsp 里引用方式是这样的，但发布的时候找不到样式：

       <link rel="stylesheet" href="css/mian.css" type="text/css" />  

        <script language="javascript" src="js/main.js"> </script>

 

解决方案： 

       <link rel="stylesheet" href="<%=request.getContextPath()%>/manage/css/mian.css" type="text/css" />  

        <script language="javascript" src="<%=request.getContextPath()%>/manage/js/main.js"> </script>

 

<%=request.getConetxtPath%>这句话的意思就是引入你当前的项目的名字 输出出来是“/当前项目的名字”

# jsp,servlet,mysql等jar应从何处下载？

在oracle官网中下载的java_ee_sdk-7u1.zip中包含使用servlet的包，但是没有关于使用jsp的包，在tomcat中同时有这两个包，可以添加目录到classpath，也可以将其复制到Web应用的lib目录下。mysql的JDBC需要在oracle官网中下载。



# myeclipse derby JDBC code

环境: myeclipese 5.5.1



import java.sql.Connection;

import java.sql.DriverManager;

import java.sql.ResultSet;

import java.sql.SQLException;

import java.sql.Statement;



public class Coon {

	public static void main(String[] args) {

		Connection conn=null;

		try {

			Class.forName("org.apache.derby.jdbc.ClientDriver");//from derbyclient.jar

			String url ="jdbc:derby://localhost:1527/MyDbTest;create=true";//create=true必须写，MyDbTest任意名称

			try {

				conn = DriverManager.getConnection(url, "admin", "admin");//用户名密码不能是1，1

				//System.out.println(conn.toString());

				String sql ="select * from myuser";

				Statement stmt  =conn.createStatement();

				ResultSet rs = stmt.executeQuery(sql);

				System.out.println(rs);

			} catch (SQLException e) {

				e.printStackTrace();

			}

		} catch (ClassNotFoundException e) {

			e.printStackTrace();

		}

	}

}

# The markup declarations contained or pointed to by the document type declaration must be well-form

各位大哥小弟用dtd文件限制XML总报这个错误，是什么意思啊，我的XML肯定没错，因为不用DTD可以运行

<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE pets[

<!ELEMENT pets(dogs,penguins)>

<!ELEMENT dogs(dog*)>

<!ELEMENT penguins(penguin+)>

<!ELEMENT dog (name,health,love,strain?)>

<!ATTLIST dog id CDATA #REQUIRED>

<!ELEMENT penguin(name,health,love,sex)>

<!ATTLIST penguin id CDATA #REQUIRED>

<!ELEMENT name(#PCDATA)>

<!ELEMENT health(#PCDATA)>

<!ELEMENT love(#PCDATA)>

<!ELEMENT strain(#PCDATA)>

<!ELEMENT sex(#PCDATA)>

]>



你这个事内部的dtd文件，要放在XML文件中，如果要做成外部dtd，那么要把你的<!DOCTYPE pets[ ]> 去掉。

# 关于重启tomcat问题

修改servlet需要重启tomcat，修改jsp不需要

# Eclipse WebContent WebRoot 

最近在做Web 项目时，新建了一个WEB 项目，如webdemo,eclipse默认的build路径为build, WEB-INF存放于WebContent下面，今改了一个build路径和WebContent名字，发现项目不可用了，



1. 具体修改过程过，把WebContent 改为 WebRoot

2. 把build路径从build/classes 改为 webdemo/WebRoot/WEB-INF/classes



在修改之前原存放于lib下的jar包都存于eclipse项目的Libraries/Web App Libraries目录下面，改后，Web App Libraries 变为空了，而且Tomcat6.x在启动的时候也识别不了了。研究了一下午，终于找出问题所在，今天特发出来，以供后来的朋友参照。



我们打开所建项目目录，在根目录下面有一.settings\org.eclipse.wst.common.component文件，

在刚新建一个项目时，此文件下面的内容如下：



<?xml version="1.0" encoding="UTF-8"?>

<project-modules id="moduleCoreId" project-version="1.5.0">

<wb-module deploy-name="webdemo">

<wb-resource deploy-path="/" source-path="/WebContent"/>

<wb-resource deploy-path="/WEB-INF/classes" source-path="/src"/>

<property name="context-root" value="webdemo"/>

<property name="java-output-path" value="/webdemo/build/classes"/>

</wb-module>

</project-modules>



改后；发现少了一句<wb-resource deploy-path="/" source-path="/WebContent"/>,所以我们要手动把它加下，最后改正后的内容如下：



<?xml version="1.0" encoding="UTF-8"?>

<project-modules id="moduleCoreId" project-version="1.5.0">

<wb-module deploy-name="webdemo">

<wb-resource deploy-path="/" source-path="/WebRoot"/>

<wb-resource deploy-path="/WEB-INF/classes" source-path="/src"/>

<property name="context-root" value="webdemo"/>

<property name="java-output-path" value="/webdemo/build/classes"/>

</wb-module>

</project-modules>



这样我们的eclipse web 项目又可以像以前一样运行，而且所有lib包下的jar也会自动存入Libraries/Web App Libraries目录下面。

# Servlet3中使用@WebFilter注解怎么指定Filter的顺序？

在Servlet3.0当中关于@WebFilter并没有提供顺序的参数。

# Comparable与Comparator的区别

Comparable & Comparator 都是用来实现集合中元素的比较、排序的，只是 Comparable 是在集合内部定义的方法实现的排序，Comparator 是在集合外部实现的排序，所以，如想实现排序，就需要在集合外定义 Comparator 接口的方法或在集合内实现 Comparable 接口的方法。

Comparator位于包java.util下，而Comparable位于包java.lang下

Comparable 是一个对象本身就已经支持自比较所需要实现的接口（如 String、Integer 自己就可以完成比较大小操作，已经实现了Comparable接口）   

自定义的类要在加入list容器中后能够排序，可以实现Comparable接口，在用Collections类的sort方法排序时，如果不指定Comparator，那么就以自然顺序排序，如API所说：

    Sorts the specified list into ascending order, according to the natural ordering of its elements. All elements in the list must implement the Comparable interface

这里的自然顺序就是实现Comparable接口设定的排序方式。

而 Comparator 是一个专用的比较器，当这个对象不支持自比较或者自比较函数不能满足你的要求时，你可以写一个比较器来完成两个对象之间大小的比较。

可以说一个是自已完成比较，一个是外部程序实现比较的差别而已。

用 Comparator 是策略模式（strategy design pattern），就是不改变对象自身，而用一个策略对象（strategy object）来改变它的行为。

比如：你想对整数采用绝对值大小来排序，Integer 是不符合要求的，你不需要去修改 Integer 类（实际上你也不能这么做）去改变它的排序行为，只要使用一个实现了 Comparator 接口的对象来实现控制它的排序就行了。

```java
    // AbsComparator.java     
    import   java.util.*;
    public   class   AbsComparator   implements   Comparator   {     
        public   int   compare(Object   o1,   Object   o2)   {     
          int   v1   =   Math.abs(((Integer)o1).intValue());     
          int   v2   =   Math.abs(((Integer)o2).intValue());     
          return   v1   >   v2   ?   1   :   (v1   ==   v2   ?   0   :   -1);     
        }     
    }
```

可以用下面这个类测试 AbsComparator：     

```java
    import   java.util.*;     
    public   class   Test   {     
        public   static   void   main(String[]   args)   {     
          //产生一个20个随机整数的数组（有正有负）     
          Random   rnd   =   new   Random();     
          Integer[]   integers   =   new   Integer[20];     
          for(int   i   =   0;   i   <   integers.length;   i++)     
          integers[i]   =   new   Integer(rnd.nextInt(100)   *   (rnd.nextBoolean()   ?   1   :   -1));     
          System.out.println("用Integer内置方法排序：");     
          Arrays.sort(integers);     
          System.out.println(Arrays.asList(integers));     

          System.out.println("用AbsComparator排序：");     
          Arrays.sort(integers,   new   AbsComparator());     
          System.out.println(Arrays.asList(integers));     
        }     
    }
```

Collections.sort((List<T> list, Comparator<? super T> c)是用来对list排序的。

如果不是调用sort方法，相要直接比较两个对象的大小，如下：

Comparator定义了俩个方法，分别是   int   compare(T   o1,   T   o2)和   boolean   equals(Object   obj)，

用于比较两个Comparator是否相等

true only if the specified object is also a comparator and it imposes the same ordering as this comparator.

有时在实现Comparator接口时，并没有实现equals方法，可程序并没有报错，原因是实现该接口的类也是Object类的子类，而Object类已经实现了equals方法

 Comparable接口只提供了   int   compareTo(T   o)方法，也就是说假如我定义了一个Person类，这个类实现了   Comparable接口，那么当我实例化Person类的person1后，我想比较person1和一个现有的Person对象person2的大小时，我就可以这样来调用：person1.comparTo(person2),通过返回值就可以判断了；而此时如果你定义了一个   PersonComparator（实现了Comparator接口）的话，那你就可以这样：PersonComparator   comparator=   new   PersonComparator();

comparator.compare(person1,person2);。

# 在多线程中创建单例模式的双重锁定(Double-Check Locking ) 

```java
    public class SingleTon {
        private static SingleTon singleTon = null;
        public SingleTon() {
            // TODO Auto-generated constructor stub
        }
        public static SingleTon getInstance(){
            if (singleTon == null) {
                synchronized (SingleTon.class) {
                    if (singleTon == null) {
                        singleTon = new SingleTon();
                    }
                }
            }
            return singleTon;
        }
    }
```

为何要使用双重检查锁定呢？考虑这样一种情况，就是有两个线程同时到达，即同时调用 getInstance() 方法，此时由于 singleTon == null ，所以很明显，两个线程都可以通过第一重的 singleTon == null ，进入第一重 if 语句后，由于存在锁机制，所以会有一个线程进入 lock 语句并进入第二重 singleTon == null ，而另外的一个线程则会在 lock 语句的外面等待。而当第一个线程执行完 new  SingleTon（）语句后，便会退出锁定区域，此时，第二个线程便可以进入 lock 语句块，此时，如果没有第二重 singleTon == null 的话，那么第二个线程还是可以调用 new  SingleTon （）语句，这样第二个线程也会创建一个 SingleTon实例，这样也还是违背了单例模式的初衷的，所以这里必须要使用双重检查锁定。细心的朋友一定会发现，如果我去掉第一重 singleton == null ，程序还是可以在多线程下完好的运行的，考虑在没有第一重 singleton == null 的情况下，当有两个线程同时到达，此时，由于 lock 机制的存在，第一个线程会进入 lock 语句块，并且可以顺利执行 new SingleTon（），当第一个线程退出 lock 语句块时， singleTon 这个静态变量已不为 null 了，所以当第二个线程进入 lock 时，还是会被第二重 singleton == null 挡在外面，而无法执行 new Singleton（），所以在没有第一重 singleton == null 的情况下，也是可以实现单例模式的？那么为什么需要第一重 singleton == null 呢？这里就涉及一个性能问题了，因为对于单例模式的话，new SingleTon（）只需要执行一次就 OK 了，而如果没有第一重 singleTon == null 的话，每一次有线程进入 getInstance（）时，均会执行锁定操作来实现线程同步，这是非常耗费性能的，而如果我加上第一重 singleTon == null 的话，那么就只有在第一次，也就是 singleTton ==null 成立时的情况下执行一次锁定以实现线程同步，而以后的话，便只要直接返回 Singleton 实例就 OK 了而根本无需再进入 lock 语句块了，这样就可以解决由线程同步带来的性能问题了。如果将方法使用synchronize进行修饰，虽然也可以解决问题，但是会导致性能的下降。

```java
    public class SingleTon {
        private static SingleTon singleTon = null;
        public SingleTon() {
            // TODO Auto-generated constructor stub
        }
        public static synchronized SingleTon getInstance(){
            if (singleTon == null) {
                  singleTon = new SingleTon();
            }
            return singleTon;
        }
    }
```

#  Class类

Class类是为了保存JAVA虚拟机运行时(RTTI)对所有对象进行类型识别的信息而设立的。当然Class也是继承自Object类的,每个类都有Class对象,想得到一个类的Class对象共有三种方法.  

1:调用getClass()   

    Employee emp;  
    Class cls=emp.getClass();  

2:静态方法forName(String  clsName)   

    String className="Employee";  
    Class  cls=Class.forName(className);  

3:class成员变量法 

    Class cls=Employee.class;   

# myeclipse工程结构问题

.myeclipse目录总体是安装了myeclipse插件的目录，而且这个大的myeclipse插件实际是由很多小的插件组成的，比如tomacat插件，spring插件等等。 

    .classpath文件是用来描述程序模块编译的类路径的。 
    .myhibernatedata文件里写了一些资源文件的信息。 
    .myhibernatedata中是hibernate依赖目录描述。 
    .mystrutsdata描述struts的数据信息。 
    .project存储项目的一些基本配置信息的。 
    .springBeans是存储Spring工具的配置信息的，路径不对，工具有可能不能用的。

新建WebRoot文件夹，然后在项目工程目录下找到.mymetadata文件，里面的

    <attributes> 
    <attribute name="<SPAN class=hilite1>webrootdir</SPAN>" value="WebRoot" /> 
    </attributes> 

这句话应该是来设置项目的根目录的

# MyEclipse删除对Struts、Hibernate、Spring的支持

最近碰到添加了SSH的支持，但又发现有些包或配置文件不正确，想重新添加，但MyEclipse没有自动重新加载功能，于是到网上搜索了相关内容，总结如下：

## 撤消MyEclipse对Struts的支持

第一步删除struts-config.xml文件。删除config文件是主要的，否则重新部署struts时MyEclipse会瘫痪。其他由MyEclipse自动生成的struts相关文件可以不去理会，等重新部署的时候如有重名他们将会被自动覆盖。

第二步修改.project文件。用记事本打开.project文件，删除：

    <nature>com.genuitec.eclipse.cross.easystruts.eclipse.easystrutsnature</nature>

保存退出。右键单击项目，选择Refresh让新改的.project文件生效。这时候struts功能又可以使用了，再重新部署struts功能即可。

## 撤消MyEclipse对Hibernate的支持

我是通过菜单MyEclipse->Project Capabilities添加了对Hibernate的支持，添加容易，删除难，菜单里好像没有删除对Hibernate支持的功能，只能手工删除了： 

第一步把项目根目录下文件.myhibernatedata删除 

第二步修改项目根目录下文件.project：删除其中两段内容： 

    <buildCommand>
        <name>com.genuitec.eclipse.hibernate.HibernateBuilder</name>
        <arguments>
        </arguments>
    </buildCommand> 

    <nature>com.genuitec.eclipse.hibernate.hibernatenature</nature> 

第三步删除Hibernate对应的mapping file,class 

## 撤消MyEclipse对Spring的支持

1. 从build path中删除spring libs
2. 手工修改工程目录下的.project文件中相关的内容
3. 删除工程目录下的.springBean文件

刷新工程，在工程右键菜单的myeclipse下面add spring capacity项就又回来了

# 异常：created a ThreadLocal with key of type

异常信息:

    created a ThreadLocal with key of type [com.opensymphony.xwork2.inject.ContainerImpl$10] (value [com.opensymphony.xwork2.inject.ContainerImpl$10@12c74b9]) and a value of type [java.lang.Object[]] (value [[Ljava.lang.Object;@1a34544]) but failed to remove it.

原因大概是说tomcat 6.025之后引入了一种内存泄露的检查机制，会把不能垃圾收集的对像做日志。

第一种解决办法：使用低于6版本的tomcat。

第二种解决办法：在tomcat的server.xml文件（在tomcat的安装路径下的conf文件夹里）中把监听关掉：就是把下面三句话括起来就可以啦。

```xml
    <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
    <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
    <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
```

# 服务器的瞬时 Diffie-Hellman 公共密钥过弱

最新版本的chrome（45.0.2454.85 m）在访问证书时，会报“服务器的瞬时 Diffie-Hellman 公共密钥过弱”。最开始以为是证书制作的问题，百度时看到一个解决方法是通过设置tomcat的机密级别：在<connector>中加入

    ciphers="TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA" 

但在本机测试可以，线上环境却会报："unsupported cipher suite XXX"。经过测试发现，JDK1.6和JDK1.7支持的加密算法是不一样的，测试升级JDK，问题解决。

补充：tomcat最好也换也tomcat7

# Tomcat启动报Error listenerStart错误

今天启动Tomcat启动不了，报以下错： 

    org.apache.catalina.core.StandardContext startInternal 
    SEVERE: Error listenerStart 
    org.apache.catalina.core.StandardContext startInternal 
    SEVERE: Context [/******] startup failed due to previous errors 

Tomcat报的错太含糊了，什么错都没报出来，只提示了Error listenerStart。为了调试，我们要获得更详细的日志。可以在WEB-INF/classes目录下新建一个文件叫logging.properties，内容如下 

```properties
    handlers = org.apache.juli.FileHandler, java.util.logging.ConsoleHandler  
      
    ############################################################  
    # Handler specific properties.  
    # Describes specific configuration info for Handlers.  
    ############################################################  
      
    org.apache.juli.FileHandler.level = FINE  
    org.apache.juli.FileHandler.directory = ${catalina.base}/logs  
    org.apache.juli.FileHandler.prefix = error-debug.  
      
    java.util.logging.ConsoleHandler.level = FINE  
    java.util.logging.ConsoleHandler.formatter = java.util.logging.SimpleFormatter  
```

这样，我们再启动tomcat时，就会在logs目录下生成一个更详细的日志error-debug.2012-05-31.log。我碰到的错误是FileNotFoundException.大家碰到的错应该各式各样都有，所以就要具体问题具体分析了。 tomcat的logging文档具体可参考http://tomcat.apache.org/tomcat-7.0-doc/logging.html 

# 比较好的文章

* 浅析Web工程目录和tomcat目录: http://blog.csdn.net/ystyaoshengting/article/details/6204886
* web.xml配置详解: http://twb.iteye.com/blog/196733
* CSS3美化有序列表: http://www.w3cplus.com/css3/css3-ordered-list-styles
* 简洁纯净的CSS表单设计实例: http://blog.bingo929.com/clean-and-pure-css-form-design.html
* DreamweaverCS5+Tomcat环境配置: http://blog.csdn.net/jnqqls/article/details/7024170
