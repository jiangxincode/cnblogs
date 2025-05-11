
## MANIFEST.MF文件

在Eclipse的.classpath和runableX.jar中的MANIFEST.MF文件中都指定了可依赖jar包的顺序，所以只要保证需要的jar包排在前面，被classloader首先加载即可。对一普通的jar包，由于MANIFEST.MF没有指定加载顺序，所以必须`java -cp A.jar;C-2.jar;C-1.jar com.jiangxin.classloader.A`


## Eclipse 一直提示 loading descriptor for 解决

Eclipse左侧的Project Explorer 最右上角有一个小钮,鼠标移上去时提示"View Menu".点一下,在弹出的上下文菜单中选择"Customize View..." 弹出一个对话框.选择: Content 选项卡,在里面把没用的去掉就行了 J2EE WEB loading descriptor .

## 关于Eclipse配置文件导出问题

Eclipse的默认配置一般不能满足我们的要求，我们一般会修改一些配置，如字体、背景颜色、快捷键及一些template等等，这样方便我们的开发。可是当我们新建一个工作空间的时候，Eclipse又会使用默认配置，怎样将我们习惯的配置导出然后导入新工作空间呢？

方法一：使用eclipse的导出功能。工作目录中右键选择Export->General->Preference，这样可以导出epf文件，新的工作空间中可以用Import导入该配置文件，这个方法的确可以导入绝大多数的配置，但是并不全，导入后会丢失很多配置。

方法二：将workspace/.metadata/.plugins/org.eclipse.core.runtime中的.settings文件夹拷贝出来，里面就是所有的配置文件，新建工作空间的时候将该.settings文件夹替换掉新工作空间中的.settings文件夹即可。（有网友是将.plugings文件夹替换，但是.plugings文件夹太大了，实际上就是替换.settings文件夹，.settings只有几百k。）另外导出界面上的工具栏对话框布局等：.metadata\.plugins\org.eclipse.e4.workbench 将该文件夹保存起来即可。

## 如何升级Eclipse才能保留之前安装的插件

`File->Import->Install->From Exist Installation`，选择旧的Eclipse安装文件夹，这样以前装的插件就都出现了。直接全选安装，瞬间就从本地的安装中把原来的插件都迁移过来了。
如果中途报错，直接重启，然后一部分一部分导入即可。揪出哪个插件导致的崩溃。


## Eclipse列编辑

其实Eclipse也有列编辑功能，不过要3.5以后的版本。要使用Eclipse的列编辑功能，只需要通过快捷键Alt+Shift+a来打开，关闭也一样。有了列编辑功能，就可以对一块代码进行编辑了，比如一块代码的缩进，只需要选中代码块按Tab就可以了，又比如想在每行第二个字符前加入一个“test”，那么只需要向下拖动光标，使定位在每行的第二个字符，然后就可以插入啦。当然，还有更多好玩的功能可以使用，摸索一下就知道了。

## Eclipse中修改注释中@author

`Window-->Preferences-->Java-->Code Style-->Code Templates`，点击Comments，找到Types 然后双击填入以下几个东西，然后在新建类的时候选择`Generate comments`即可

    /**
     * @author 作者的名字  E-mail: 写自己的Email
     * @version 创建时间：${date}  ${time}
     */

## Eclipse中 sysout 按alt+/为什么不出System.out.println();

需要重新设置快捷键。按快捷键ctrl+shirt+L，然后在按一下L。设置快捷键的对话框就出来了，然你将Word Completion移除，在将Content Assist 这个设置为alt+/。就可以了。

1、myeclpse–>Preferences–>General–>Keys。删掉word completion的快捷键设置alt+/ 【这个跟Content Assist起冲突了】

2、把Content Assist的快捷键由ctrl+space改成alt+/ 

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

```java
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
```

执行Format操作后，注释格式却变为：

```java
/**
 * 根据文件开头的BOM（如果存在的话），判断文件的编码格式。 文本文件有各种不同的编码格式，如果判断有误，则会导致显示或保存错误。
* 为了标识文件的编码格式，便于编辑和保存，则在文件开头加入了BOM，用以标识编码格式。 UTF-8格式：0xef 0xbb 0xbf， Unicode
  * Little Endian格式：0xff 0xfe， Unicode Big Endian格式：0xfe
  * 0xff。而ANSI格式是没有BOM的。另有一种不含BOM的UTF-8格式的文件，则不易与ANSI相区分，因此未能识别此类格式。
*
  * @param file
  *          待判断的文件
*/
```

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

## Eclipse插件开发相关问题

在Eclipse插件开发过程中，运行或调试时总会在控制台中输出一些对于当前开发无用的日志，比如各种插件的快捷键冲突，某些插件的自身报错，某些插件的license交互等等，这些日志会妨碍我们查看真正想看的日志。解决办法是在run/debug设置中去掉对应的启动插件。

![](http://images2015.cnblogs.com/blog/611264/201604/611264-20160424232948226-816722543.jpg)