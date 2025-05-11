
# JDK

JDK(Java Development Kit)是一个写Java程序所需的开发环境。它由一个处于操作系统层之上的运行环境，还有开发者编译、调试和运行Java应用程序所需的工具组成。JDK是Sun Microsystems为Java程序员提供的产品。目前JDK已经成为使用最广泛的Java SDK（Software development kit）。 JDK包含的基本组件包括：

* javac: 编译器，将源程序转成字节码
* jar: 打包工具，将相关的类文件打包成一个文件
* jdb: debugger，查错工具

JDK中还包括完整的JRE（Java Runtime Environment，Java运行环境），也被称为private runtime。包括了用于产品环境的各种库类，以及给开发员使用的补充库，如国际化的库、IDL库。 JDK中还包括各种例子程序，用以展示Java API中的各部分。

## 配置JDK环境变量(Windows)

安装JDK以后，需要配置一下环境变量，在我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量(假定你的jdk安装在c:\jdk1.6）:
```
    JAVA_HOME=c:\jdk1.6
```
JAVA_HOME指向的是JDK的安装路径，在这路径下你应该能够找到bin、lib等目录。JDK的安装路径可以选择任意磁盘目录，不过建议你放的目录层次浅一点。
```
    CLASSPATH=. ;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
```
注：.;一定不能少，因为它代表当前路径。

在系统变量里找到Path变量，这是系统自带的，不用新建。你只需修改一下，使他指向JDK的bin目录，这样你在控制台下面编译、执行程序时就不需要再键入一大串路径了。双击Path，在已有的变量后加上(注意前面的分号)：
```
    ;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin
```
注：要以管理员身份运行cmd才可以更改系统变量，JDK 10以及更新版本`PATH`环境变量中不需要添加`%JAVA_HOME%\jre\bin`，JDK11以及更新版本不需要单独设置`CLASSPATH`环境变量。

## 怎样在Linux系统中下载和安装OpenJDK包

Debian, Ubuntu等系统：在命令行中，键入：
```shell
    $sudo apt-get install openjdk-7-jre
    $sudo apt-get install openjdk-6-jre
```
需要注意的是，openjdk-?-jre包只包含Java运行时环境（Java Runtime Environment）。如果是要开发Java应用程序，则需要安装openjdk-?-jdk包。命令如下：
```shell
    $sudo apt-get install openjdk-7-jdk
    $sudo apt-get install openjdk-6-jdk
```
Fedora, OracleLinux, Red Hat Enterprise Linux等系统：在命令行中，键入：
```shell
    $ su -c "yum install java-1.7.0-openjdk"
    $ su -c "yum install java-1.6.0-openjdk"
```
需要注意的是，java-1.?.0-openjdk包只包含Java运行时环境（Java Runtime Environment）。如果是要开发Java应用程序，则需要安装java-1.?.0-openjdk-devel包。命令如下：
```shell
    $ su -c "yum install java-1.7.0-openjdk-devel"
    $ su -c "yum install java-1.6.0-openjdk-devel"
```

# Java中char到底是多少字节？

貌似一个简单的问题（也许还真是简单的）但是却把曾经自认为弄清楚的我弄得莫名其妙 。char在Java中应该是16个字节 ，byte在Java中应该是8个字节 ，char x = '编'; //这样是合法的，输出也是16个字节 ，但是
```
String str = "编";
byte[] bytes = str.getBytes(); //我想不明白，为什么这里要占用3个byte呢?
```
3个byte一共是3*8=24个字节，那么char x怎么又放得下？我坚信char是16个字节， 但是str.getBytes()这个东西到底又怎么回事？

首先，要搞清楚 code point 和 encoding 的区别。Java 是遵循 unicode 4.0 标准的，而内部的 character 以 utf-16 作为 encoding。unicode 4.0 标准包含从 U+0000-U+FFFF 的基本多语言平面和 U+10000-U+10FFFF 的扩展平面的文字，这是 code point。Java 的 char 类型是 16 bit 的，所以单个 char 只支持基本平面内的文字，而扩展平面的文字是由一对 char 来表示的。 而 String.getBytes() 这个方法是按照指定的 encoding 返回字符串，一般中文系统的默认编码是 utf-8 (linux, mac) 或者 gbk/gb18030 (windows)。只要是基本平面内的文字，utf-8码的中文都是3字节的，而 gbk/gbk18030 是2字节的。


# finally和return

这是一道Java面试题：try { }里有一个return语句，那么紧跟在这个try后的finally {}里的code会不会被执行，什么时候被执行，在return前还是后?(如果try后面有个catch块，里面有return语句，那么finally语句会不会执行？)

finally语句块的作用就是为了保证无论出现什么情况，一定要执行的，那么finally里的code肯定会执行，并且是在return前执行。（只要语句执行了，肯定是在return前执行的。 finally中也可以有return，并且会覆盖其他的return）

根据java规范：在try-catch-finally中，如果try-finally或者catch-finally中都有return，则两个return语句都执行并且最终返回到调用者那里的是finally中return的值；而如果finally中没有return，则理所当然的返回的是try或者catch中return的值，但是finally中的代码是必须要执行的，方法在return的时候并不是把它所拥有的那个值给返回了，而是复制一份返回！因此，对于基本类型的数据，在finally中改变return的值对返回值没有任何影响，而对于引用类型的数据，就有影响。

```java
public class FinallyTest{
	public static void main(String[] args) {
		System.out.println("x的值是"+new FinallyTest().test());;
	}
	@SuppressWarnings("finally")
	static int test() {
		int x = 1;
		try {
			//x++;
			return x;
		}
		finally {
			++x;
			System.out.println("x的值当前值是" +x);
			//return x;
		}
	}
}
```
	
执行结果：x的值当前值是2\nx的值是1

若finally中包含return语句
```java
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
```
执行结果是：x的值当前值是2\nx的值是2

若引用类型的数据，就有影响，
```java
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
```
执行结果是：的最终返回值是： 25

2. Java中的return语句总是和方法有密切关系，return语句总是用在方法中，有两个作用，一个是返回方法指定类型的值（这个值总是确定的），一个是结束方法的执行（仅仅一个return语句）。return结束当前方法,后面语句除了finally语句块都不会执行。break跳出当前语句块,循环则跳出当前循环,也可在多重循环嵌套时跳出指定循环层。System.exit(0)表示关闭虚拟机,即使是finally语句块也不会执行


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

# WEB-INF目录与META-INF目录的作用

```
/WEB-INF/web.xml: Web应用程序配置文件，描述了 servlet 和其他的应用组件配置及命名规则。
/WEB-INF/classes/: 包含了站点所有用的 class 文件，包括 servlet class 和非servlet class，他们不能包含在 .jar文件中。
/WEB-INF/lib/: 存放web应用需要的各种JAR文件，放置仅在这个应用中要求使用的jar文件,如数据库驱动jar文件。
/WEB-INF/src/: 源码目录，按照包名结构放置各个java文件。
/WEB-INF/database.properties: 数据库配置文件
/WEB-INF/tags/: 存放了自定义标签文件，该目录并不一定为 tags，可以根据自己的喜好和习惯为自己的标签文件库命名，当使用自定义的标签文件库名称时，在使用标签文件时就必须声明正确的标签文件库路径。例如：当自定义标签文件库名称为 simpleTags 时，在使用 simpleTags 目录下的标签文件时，就必须在 jsp 文件头声明为：<%@ taglibprefix="tags" tagdir="/WEB-INF /simpleTags" % >。
/WEB-INF/jsp/: jsp 1.2 以下版本的文件存放位置。改目录没有特定的声明，同样，可以根据自己的喜好与习惯来命名。此目录主要存放的是 jsp 1.2 以下版本的文件，为区分 jsp 2.0 文件，通常使用 jsp 命名，当然你也可以命名为 jspOldEdition 。
/WEB-INF/jsp2/: 与 jsp 文件目录相比，该目录下主要存放 Jsp 2.0 以下版本的文件，当然，它也是可以任意命名的，同样为区别 Jsp 1.2以下版本的文件目录，通常才命名为 jsp2。
META-INF: 相当于一个信息包，目录中的文件和目录获得Java 2平台的认可与解释，用来配置应用程序、扩展程序、类加载器和服务 manifest.mf文件，在用jar打包时自动生成。
```

# Java 数组的静态初始化和动态初始化

静态初始化是指由程序员自己为数组对象的每个元素赋值，由系统自动计算出数组的长度,例如：

`String[] a=new String[]{"Hello","World","Yes"};`

动态初始化是指由程序员自己指定数组对象的长度，由系统先自动为其赋值。程序中程序员可以为元素重新赋值,例如：
```java
String [] b=new String[4];
for(int i=0;i<b.length;i++){
b[i]=i+"hello ";
}
```
通常基本整数类型byte,short,int,long,初始值为0；浮点型float,double,初始值为0.0；boolean类型，初始值为false；引用类型：类、String、数组等均为null；

在使用数组的时候，我们通常有两个步骤：首先，声明数组引用变量，即String[] a,此时的a并不是一个数组对象，而只是一个相当于指针的变量；然后，当我们执行new String[]{"Hello","World","Yes"}以后才真正创建了一个数组对象，此时变量a 才指向了堆内存里面的数组对象。

# String数组初始化

近日，笔者在java编程中因为疏忽对String数组的初始化定义错误，导致程序运行出错。现将所理解的String数组在此进行说明，并对String数组初始化进行分析。
```java
	//一维数组
	String[] str = new String[5]; //创建一个长度为5的String(字符串)型的一维数组
	String[] str = new String[]{"","","","",""};
	String[] str = {"","","","",""};
	//二维数组
	String[][] str = new String[2][2]; //创建一个2行2列的二维数组
```
String数组初始化区别

String[] str = {"1","2","3"}与String[] str = new String[]{"1","2","3"}在内存里有什么区别？

编译执行结果没有任何区别。更不可能像有些人想当然说的在栈上分配空间，Java的对象都是在堆上分配空间的。这里的区别仅仅是代码书写上的：String[] str = {"1","2","3"}; 这种形式叫数组初始化式（Array Initializer），只能用在声明同时赋值的情况下。而 String[] str = new String[]{"1","2","3"} 是一般形式的赋值，=号的右边叫数组字面量（Array Literal），数组字面量可以用在任何需要一个数组的地方（类型兼容的情况下）。如：
```java
　　String[] str = {"1","2","3"}; // 正确的
　　String[] str = new String[]{"1","2","3"} // 也是正确的
```
而
```java
　　String[] str;
　　str = {"1","2","3"}; // 编译错误
```
因为数组初始化式只能用于声明同时赋值的情况下。改为：
```java
　　String[] str;
　　str = new String[] {"1","2","3"}; // 正确了
```
又如：
```java
　　void f(String[] str) {
　　}
　　f({"1","2","3"}); // 编译错误
```
正确的应该是：
```java
　　f(new String[] {"1","2","3"});
```
笔者所犯错误为在初始化数组的时候定义为String[] str = new String[]{}，如此定义相当于创建了创建一个长度为0的String型的一维数组。在后期为其赋值的时候str[0]="A"，就会抛出异常。

# 字符串的各种编码转换

java中的String类是按照unicode进行编码的，当使用String(byte[] bytes, String encoding)构造字符串时，encoding所指的是bytes中的数据是按照那种方式编码的，而不是最后产生的String是什么编码方式，换句话说，是让系统把bytes中的数据由encoding编码方式转换成unicode编码。如果不指明，bytes的编码方式将由jdk根据操作系统决定。

当我们从文件中读数据时，最好使用InputStream方式，然后采用String(byte[] bytes, String encoding)指明文件的编码方式。不要使用Reader方式，因为Reader方式会自动根据jdk指明的编码方式把文件内容转换成unicode编码。

当我们从数据库中读文本数据时，采用ResultSet.getBytes()方法取得字节数组，同样采用带编码方式的字符串构造方法即可。
```java
ResultSet rs;
bytep[] bytes = rs.getBytes();
String str = new String(bytes, "gb2312");
```
不要采取下面的步骤：
```java
ResultSet rs;
String str = rs.getString();
str = new String(str.getBytes("iso8859-1"), "gb2312");
```
这种编码转换方式效率底。之所以这么做的原因是，ResultSet在getString()方法执行时，默认数据库里的数据编码方式为iso8859-1。系统会把数据依照iso8859-1的编码方式转换成unicode。使用str.getBytes("iso8859-1")把数据还原，然后利用new String(bytes, "gb2312")把数据从gb2312转换成unicode，中间多了好多步骤。

从HttpRequest中读参数时，利用reqeust.setCharacterEncoding()方法设置编码方式，读出的内容就是正确的了。


# Selenium相关

## selenium的版本和firefox不兼容
```
【Selenium】   -> 【FireFox】
2.25.0        ->  18
2.30.0        ->  19
2.31.0        ->  20
2.42.2        ->  29
2.44.0        ->  33 (不支持31,2014/12/1)
```
PS：但是selenium-java-2.42.2版本和firefox 29.0.1版本兼容，如果升级到firefox 30+,则浏览器启动失败。可能是selenium还未同步升级，后面估计可以正常支持。切记，关掉forefox的升级功能，否则连本地Windows上的脚本都跑不起来，作者曾经为此还降级了forefox。

升级后，selenium脚本正常启动firefox。

## selenium使用IE 	
```
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
```
如果遇到上面的问题



解决方法有两种：

1.是修改掉IE的设置，不要在任何情况下使用保护模式（protected mode）

2.另一种即是前面代码中如下片段在运行时设置IE的Capabilities。

DesiredCapabilities ieCapabilities = DesiredCapabilities.internetExplorer();
ieCapabilities.setCapability(InternetExplorerDriver.INTRODUCE_FLAKINESS_BY_IGNORING_SECURITY_DOMAINS,true);
WebDriver oWebDriver = new InternetExplorerDriver(ieCapabilities);


# Html/Xhtml/Html5
```xml
<black>使文字呈现闪烁效果
&nbsp; 不断行的空白格,是英文的一个空格
&ensp; 半方大的空白,相当于半个中文字的位置
&emsp; 全方大的空白,相当于一个中文字的位置
```

# Javascript

JavaScript利用对象的能力比VBScript强，可以使用JavaScript定义类，是Object-Based的脚本语言。虽然它貌似Java，但语法上和C相似，是一种独立的语言。


# 关于层和HTML代码

当您在Web页中插入层时，Dreamweaver将这些层的HTML标签插入到您的代码中。您可以为您的层设置四种不同的标签：div，span，layer和ilayer。其中div和span是最常见的标签，推荐您使用，这样才能有最广泛的受众可以看到您的层。Internet Explorer 4.0和Netscape Navigator 4.0都支持使用div和span标签创建的层。只有Navigator 4.0版本支持使用layer和ilayer创建的层（Netscape在其后续版本浏览器中停止了对这两种标签的支持）。这些浏览器的早期版本都可以显示层的内容，但不能显示其位置。

默认情况下，Dreamweaver使用div标签创建层，并在插入点或页面顶部body标签后面放置层代码。如果您创建嵌套层，Dreamweaver将把代码插入到您定义的父层标签中。若要改变默认标签，请参看设置层参数。

下面是一个单个的层的HTML代码示例（在Dreamweaver中的情况）：
```html
<div id="Layer1" style="position:absolute; visibility:inherit; width:200px; height:115px; z-index:1">
</div>
```
下面是一个嵌套层的HTML代码示例（在Dreamweaver中的情况）：
```html
<div id="Parent" style="position:absolute; left:56px; top:54px; width:124px; height:158px; z-index:1;">
Content inside the parent layer.
<div id="Nested" style="position:absolute; left:97px; top:114px; width:54px; height:69px; z-index:1;">
Content inside the nested layer.
</div>
</div>
```
您可以设置层在页面上的位置属性。这些属性包括左边和顶部（分别对应x和y坐标），Z轴（也称为堆叠顺序），和可见性。如需要更多信息，请参看设置层属性。



# 网站设计中揪出网页的无效链接

在我们浏览网站的时候，一定都遇到过页面上带红叉的无效图片或者“无法找到网页”的提示，出现如此现象一般都是因为链接文件的位置发生变化、被误删除或者文件名的拼写错误造成的。 为了避免出现无效链接的尴尬，树立良好的网站形象，当我们完成一个网站的设计制作后，一定要认真地检查是否存在失效链接，以便及时修改。将无效链接扼杀在上传前。

为了预防网站上传后出现无效链接，在上传前我们可以使用FrontPage的超链接报表功能来检查整个网站的链接情况，如果遇到无效链接还可以及时编辑修复。首先我们要把需要检查链接的站点设置为FrontPage的网站，运行FrontPage，选择“文件→新建→由一个网页组成的网站”进入“网站模板”窗口，单击“浏览”指定到你的站点目录，“确定”后即可打开整个网站。执行“视图→报表→问题→超链接”，弹出对话框询问是否验证网站中的超链接，单击“是”验证所有超链接，包括指向站内网页的内部链接和指向外部网站的外部链接，稍等一会儿FrontPage就会将验证结果显示出来。验证结果包括链接所在的网页、网页标题、链接目标和类型等。对于无效链接，FrontPage会在“状态”栏下标注“中断”，选中并双击一个“中断”的无效超链接，在弹出的超链接编辑窗口中就可以对错误的超链接进行修复了。我们可以直接键入正确的链接地址或在“浏览”中选择指定到正确的文件，如果在其他网页中也有这个相同的错误链接，我们可以勾选“对所有网页进行更改”，然后点击“替换”按钮即可修复网站中所有包含这个无效链接的网页了。

网站上传运行后，如果网站中引用了大量的外来网站内容的链接，而我们又无法控制外来内容链接的有效性，我们只有经常对网站测试其链接的可靠性，以避免无效链接的出现。若要继续使用FrontPage对网站无效链接进行检查，还需要将网站全部下载到本地，这样会显得很麻烦，这里我们推荐使用一个小工具Xenu Link Sleuth来对网站进行在线检查。打开软件，执行“File→Check URL”打开一个对话窗口，输入你要检查的网站地址，“OK”后软件就会自动访问网站并验证每个链接地址，验证结束后就会将结果显示在验证列表中，对于无效的链接，软件会以红色字体加以区别。在失效链接的右键菜单中选择“Properties”，然后在“Properties”窗口中的“Pages linking to”下可以查看到哪些网页使用了这个无效链接，对这些网页单独下载加以修复就可以了。

提示:验证结束后，软件还可以生成一份详细的无效链接报告，包括无效链接页面以及使用无效链接的页面等以供修复时查阅。

# shortcut icon无法正常显示问题解决

`<link rel="shortcut icon" href="favicon.ico" />`显示不了图标，ie显示不了小图片,但Firefox能显示出来请教各位,怎么能让IE最好是IE7也能显示出来?谢谢了

解决方法：

1、`<link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>`

2、IE要7以上版本才支持，低于7的，除非用Maxhon之类的壳才能出现该图标。

3、这种问题应该是安装了别的浏览器引起的，比如：我就安装了Firefox.打开注册表找到如下内容：[HKEY_LOCAL_MACHINE\SOFTWARE\Classes\.htm\]下的默认值改为htmlfile(比如：我是由FirefoxHTML改为htmlfile.)，问题解决.^_^。最好事先把这个键值导出备份一下。


# 检查错误链接

直接查看代码或者使用浏览器debug

# JSP 里外部引用CSS样式的路径问题   .

我的工程目录

/WebRoot/manage/css
/WebRoot/manage/js
/WebRoot/manage/images
/WebRoot/manage/mian.jsp

我之前在 mian.jsp 里引用方式是这样的，但发布的时候找不到样式：
```jsp
    <link rel="stylesheet" href="css/mian.css" type="text/css" />
    <script language="javascript" src="js/main.js"> </script>
```
解决方案：
```jsp
    <link rel="stylesheet" href="<%=request.getContextPath()%>/manage/css/mian.css" type="text/css" />
    <script language="javascript" src="<%=request.getContextPath()%>/manage/js/main.js"> </script>
```
`<%=request.getConetxtPath%>`这句话的意思就是引入你当前的项目的名字 输出出来是“/当前项目的名字”


# The markup declarations contained or pointed to by the document type declaration must be well-form

各位大哥小弟用dtd文件限制XML总报这个错误，是什么意思啊，我的XML肯定没错，因为不用DTD可以运行
```xml
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
```

你这个事内部的dtd文件，要放在XML文件中，如果要做成外部dtd，那么要把你的<!DOCTYPE pets[ ]> 去掉。

# 关于重启tomcat问题

修改servlet需要重启tomcat，修改jsp不需要

# Servlet3中使用`@WebFilter`注解怎么指定Filter的顺序？

在Servlet3.0当中关于`@WebFilter`并没有提供顺序的参数。



## 在多线程中创建单例模式的双重锁定(Double-Check Locking )

http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html

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
```
    .classpath文件是用来描述程序模块编译的类路径的。
    .myhibernatedata文件里写了一些资源文件的信息。
    .myhibernatedata中是hibernate依赖目录描述。
    .mystrutsdata描述struts的数据信息。
    .project存储项目的一些基本配置信息的。
    .springBeans是存储Spring工具的配置信息的，路径不对，工具有可能不能用的。
```
新建WebRoot文件夹，然后在项目工程目录下找到.mymetadata文件，里面的
```xml
    <attributes>
        <attribute name="<SPAN class=hilite1>webrootdir</SPAN>" value="WebRoot" />
    </attributes>
```
这句话应该是来设置项目的根目录的


## 异常：created a ThreadLocal with key of type

异常信息:
```
    created a ThreadLocal with key of type [com.opensymphony.xwork2.inject.ContainerImpl$10] (value [com.opensymphony.xwork2.inject.ContainerImpl$10@12c74b9]) and a value of type [java.lang.Object[]] (value [[Ljava.lang.Object;@1a34544]) but failed to remove it.
```
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