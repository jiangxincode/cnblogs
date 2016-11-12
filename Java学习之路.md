* 浅析Web工程目录和tomcat目录: http://blog.csdn.net/ystyaoshengting/article/details/6204886
* web.xml配置详解: http://twb.iteye.com/blog/196733
* CSS3美化有序列表: http://www.w3cplus.com/css3/css3-ordered-list-styles
* 简洁纯净的CSS表单设计实例: http://blog.bingo929.com/clean-and-pure-css-form-design.html
* DreamweaverCS5+Tomcat环境配置: http://blog.csdn.net/jnqqls/article/details/7024170

* Java关键字及其作用：http://blog.csdn.net/hfmbook/article/details/7634385
* java中static{}语句块详解: http://blog.csdn.net/lubiaopan/article/details/4802430
* 转一个J2EE开发时的包命名规则，养成良好的开发习惯：http://www.blogjava.net/paulwong/archive/2012/04/15/374675.html
* 对比C++ 和Java: Thinking in java[Java编程思想第4版].pdf
* 舞蹈特点与编程语言特点的联想曲: http://blog.csdn.net/iammerryz/article/details/7661067?_t_t_t=0.3386819043662399
* className.class.getResourceAsStream()与ClassLoader.getSystemResourceAsStream() 的区别：http://www.blogjava.net/icewee/archive/2012/05/04/377371.html
* JAR文件包及jar命令详解: http://blog.donews.com/hitfly/archive/2005/03/25/312851.aspx
* JAVA调用系统命令或可执行程序：http://wuhongyu.iteye.com/blog/461477/
* 过时date.toLocaleString()的解决方法: http://ldl8818.iteye.com/blog/1492301
* Jps介绍以及解决jps无法查看某个已经启动的java进程问题: http://trinea.iteye.com/blog/1196400
* java中Assert的用法：http://lgl669.iteye.com/blog/483271
* Java RMI与RPC，JMS的比较：http://visionsky.blog.51cto.com/733317/438693/
* java存储数据的地方以及九种基本类型：http://blog.sina.com.cn/s/blog_81daf24e0100snj4.html
* FINAL .....FINALLY ...... 和FINALIZE ......区别: http://www.cnblogs.com/wl0000-03/p/5961582.html
* Comparable与Comparator的区别：http://blog.csdn.net/mageshuai/article/details/3849143
* FILE,FILEINPUTSTREAM,FILEREADER,INPUTSTREAMREADER,BUFFEREDREADER的使用和区别: http://www.blogjava.net/flysky19/articles/92286.html
* MyEclipse删除对Struts、Hibernate、Spring的支持：http://www.cnblogs.com/xj626852095/p/3648148.html
* 修改Struts2的struts.xml配置文件位置：http://blog.csdn.net/zht666/article/details/8980451
* Eclipse 开发WEB项目所遇问题 WebContent WebRoot：http://blog.sina.com.cn/s/blog_525960510100jo0j.html



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



## javadoc注意点（原创）

javadoc生成文档时总是报java.lang.IllegalArgumentException错

JavamavenEXTSUNJDK .

javadoc生成文档时总是报java.lang.IllegalArgumentException错误,是classpath里面字符冲突引起的。我在classpath中包含了%JAVA_HOME%\lib;解决方法是重新设置classpath或者删除classpath.要注意设置完成后重启下cmd或者editplus，重启后生效！

见官方参考文档 http://maven.apache.org/plugins/maven-javadoc-plugin/faq.html


javadoc生成时出错：编码GBK的不可映射字符

由于java源代码是用的UTF-8编码，Eclipse中默认编码是GB18030，因此，在生成javadoc的时候，需要手工指定一下编码和字符集。

解决方案是： 主菜单–>Project–>Generate javadoc–>next>next–> 在 “Extra javadoc options”下面的文本框中填入：

-encoding UTF-8 -charset UTF-8


# Java中char到底是多少字节？

貌似一个简单的问题（也许还真是简单的）但是却把曾经自认为弄清楚的我弄得莫名其妙 。char在Java中应该是16个字节 ，byte在Java中应该是8个字节 ，char x = '编'; //这样是合法的，输出也是16个字节 ，但是

String str = "编";

byte[] bytes = str.getBytes(); //我想不明白，为什么这里要占用3个byte呢?

3个byte一共是3*8=24个字节，那么char x怎么又放得下？我坚信char是16个字节， 但是str.getBytes()这个东西到底又怎么回事？

首先，要搞清楚 code point 和 encoding 的区别。Java 是遵循 unicode 4.0 标准的，而内部的 character 以 utf-16 作为 encoding。unicode 4.0 标准包含从 U+0000-U+FFFF 的基本多语言平面和 U+10000-U+10FFFF 的扩展平面的文字，这是 code point。Java 的 char 类型是 16 bit 的，所以单个 char 只支持基本平面内的文字，而扩展平面的文字是由一对 char 来表示的。 而 String.getBytes() 这个方法是按照指定的 encoding 返回字符串，一般中文系统的默认编码是 utf-8 (linux, mac) 或者 gbk/gb18030 (windows)。只要是基本平面内的文字，utf-8码的中文都是3字节的，而 gbk/gbk18030 是2字节的。

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




# 抽象方法不能是static或native或synchroniz

1、abstract是抽象的，指的是方法只有声明而没有实现，他的实现要放入声明该类的子类中实现。

2、static是静态的，是一种属于类而不属于对象的方法或者属性，而我们知道，类其实也是一个对象，他是在class文件加载到虚拟机以后就会产生的对象，通常来说它是单例的，就是整个虚拟机中只有一个这样的类对象（当然，如果用新的类加载器也会生成新的类的对象）。

3、synchronized 是同步，是一种相对线程的锁。

4、native 本地方法，这种方法和抽象方法及其类似，它也只有方法声明，没有方法实现，但是它与抽象方法不同的是，它把具体实现移交给了本地系统的函数库，而没有通过虚拟机，可以说是java与其它语言通讯的一种机制。

5、那么我们就来谈谈这些关键字为什么不能和abstract混用。

首先abstract与static，其实一看他们的作用和属性就很容易辨别，abstract是没有实现的，而static一定要有实现，因为 abstract的类不能生产对象，但是static是属于类，而类已经是一个存在的对象，这两个关键字在这上面有一个关键的矛盾点。

synchronized 是同步，然而同步是需要有具体操作才能同步的，如果像abstract只有方法声明，那同步一些什么东西就会成为一个问题了，当然抽象方法在被子类继承以后，可以添加同步。

native，这个东西本身就和abstract冲突，他们都是方法的声明，只是一个吧方法实现移交给子类，另一个是移交给本地操作系统。如果同时出现，就相当于即把实现移交给子类，又把实现移交给本地操作系统，那到底谁来实现具体方法呢！



# 在try块中可以抛出异常吗？

Java通过面向对象的方法进行异常处理，把各种不同的异常进行分类，并提供了良好的接口。在Java中，每个异常都是一个对象，它是Throwable类或其它子类的实例。当一个方法出现异常后便抛出一个异常对象，该对象中包含有异常信息，调用这个对象的方法可以捕获到这个异常并进行处理。Java的异常处理是通过5个关键词来实现的：try、catch、throw、throws和finally。一般情况下是用try来执行一段程序，如果出现异常，系统会抛出（throws）一个异常，这时候你可以通过它的类型来捕捉（catch）它，或最后（finally）由缺省处理器来处理。用try来指定一块预防所有”异常”的程序。紧跟在try程序后面，应包含一个catch子句来指定你想要捕捉的”异常”的类型。

throw语句用来明确地抛出一个”异常”。throws用来标明一个成员函数可能抛出的各种”异常”。Finally为确保一段代码不管发生什么”异常”都被执行一段代码。

可以在一个成员函数调用的外面写一个try语句，在这个成员函数内部写另一个try语句保护其他代码。每当遇到一个try语句，”异常”的框架就放到堆栈上面，直到所有的try语句都完成。如果下一级的try语句没有对某种”异常”进行处理，堆栈就会展开，直到遇到有处理这种”异常”的try语句。



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

# Servlet3中使用@WebFilter注解怎么指定Filter的顺序？

在Servlet3.0当中关于@WebFilter并没有提供顺序的参数。



## 在多线程中创建单例模式的双重锁定(Double-Check Locking )

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

##  Class类

Class类是为了保存JAVA虚拟机运行时(RTTI)对所有对象进行类型识别的信息而设立的。当然Class也是继承自Object类的,每个类都有Class对象,想得到一个类的Class对象共有三种方法.

```java

    //调用getClass()
    Employee emp;
    Class cls=emp.getClass();

    //静态方法forName(String  clsName)
    String className="Employee";
    Class  cls=Class.forName(className);

    //class成员变量法
    Class cls=Employee.class;
```

## myeclipse工程结构问题

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



## 异常：created a ThreadLocal with key of type

异常信息:

    created a ThreadLocal with key of type [com.opensymphony.xwork2.inject.ContainerImpl$10] (value [com.opensymphony.xwork2.inject.ContainerImpl$10@12c74b9]) and a value of type [java.lang.Object[]] (value [[Ljava.lang.Object;@1a34544]) but failed to remove it.

原因大概是说tomcat 6.025之后引入了一种内存泄露的检查机制，会把不能垃圾收集的对像做日志。第一种解决办法：使用低于6版本的tomcat。第二种解决办法：在tomcat的server.xml文件（在tomcat的安装路径下的conf文件夹里）中把监听关掉：就是把下面三句话括起来就可以啦。

```xml
    <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
    <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
    <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
```

## 服务器的瞬时 Diffie-Hellman 公共密钥过弱

最新版本的chrome（45.0.2454.85 m）在访问证书时，会报“服务器的瞬时 Diffie-Hellman 公共密钥过弱”。最开始以为是证书制作的问题，百度时看到一个解决方法是通过设置tomcat的机密级别：在<connector>中加入

	ciphers="TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA"

但在本机测试可以，线上环境却会报："unsupported cipher suite XXX"。经过测试发现，JDK1.6和JDK1.7支持的加密算法是不一样的，测试升级JDK，问题解决。

补充：tomcat最好也换也tomcat7

## Tomcat启动报Error listenerStart错误

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
