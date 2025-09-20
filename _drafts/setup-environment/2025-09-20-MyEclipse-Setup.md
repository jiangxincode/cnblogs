## MyEclipse 2014安装说明

下载过程就不详述了。

说明一下，可以只安装MyEclipse 2014，而不用提前安装JDK、Eclipse、Tomcat等软件，MyEclipse 2014内嵌了这些东西，网上说的MyEclipse只是Eclipse的插件，所以要安装MyEclipse就要先安装Eclipse，而要安装Eclipse又必须提前安装JDK。这对于旧版本的MyEclipse来说确实是这样，但是对于比较新的几个版本来说，不需要了，MyEclipse包含了开发所需要的大多数工具。

当然，如果你不想使用其自带的JDK或者服务器软件，你可以在安装了其它的JDK版本和服务器软件之后自行设置。（在Window->Preferences中进行配置）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image204.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image205.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image206.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image207.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image208.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image209.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image210.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image211.png)

安装好之后，先不要打开MyEclipse 2014的程序。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image212.png)

接下来对MyEclipse进行破解，由于破解包是jar包，所以需要JRE，不过一般的机子上都有，可以打开CMD输入java命令测试一下，如果显示以下命令则证明本机已有JRE，无需安装，如果没有下载JRE，进行安装。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image213.png)

打开破解文件夹，运行`cracker.jar`。在破解界面中，usercode随便输入，然后点击右边的SystemId按钮，将在SystemId中自动生成一串机器码。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image214.png)

然后选择`Tools->RebuildKey`。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image215.png)

点击激活按钮。将会看到有日志生成。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image216.png)

选择`Tools->ReplaceJarFiles`。选择MyEclipse安装目录中的Plugin文件夹。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image217.png)

操作`Tools->SaveProperities`

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image218.png)

重新打开MyEclipse 2014

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image219.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image220.png)

`MyEclipse->Subscription Informatioon`，显示激活。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image221.png)