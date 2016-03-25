# Linux自身相关内容

## 快捷键

添加快捷键：系统——首选项——键盘快捷键

### Shell 快捷键
```
    <Ctrl k>：删除从光标到行尾的部分 
    <Ctrl u>：删除从光标到行首的部分
    <Alt d>：删除从光标到当前单词结尾的部分 
    <Ctrl w>：删除从光标到当前单词开头的部分 
    <Ctrl a>：将光标移到行首 
    <Ctrl e>：将光标移到行尾 
    <Alt a>：将光标移到当前单词头部 
    <Alt e>：将光标移到当前单词尾部 
    <Ctrl y>：插入最近删除的单词         
    <Ctrl a>：跳到行首
    <Ctrl b>：左移一个字符
    <Ctrl c>：终止终端进程
    <Ctrl d>：从光标处向右删除
    <Ctrl e>：跳到行尾
    <Ctrl f>：右移一个字符
    <Ctrl k>：从光标处删除到行尾
    <Ctrl l>：清屏，类似 clear 命令
    <Ctrl r>：查找历史命令
    <Ctrl z>：Suspend/ Stop the command  、 暂停命令的执行
    <Ctrl h>：删除当前字符
    <Ctrl w>：删除最后输入的单词
    <!$>：重复前一个命令最后的参数。
    <SHIFT PageUp/PageDown>：终端上下翻页
```

### 常用快捷键
```
    <Alt+Tab>：切换窗口(win)
    <Win+Tab>：若开3D效果了切换
    <Ctrl+Alt+Backspace>：相当于强制注销
    <Ctrl+Alt+Del>：调出关机菜单
    <Ctrl+Alt+l>：锁定桌面
    <Ctrl+Alt+d>：最小化gnome所有窗口
    <Ctrl+Alt+f2>：linux终端用户（Alt + f7返回xwindows，Alt+ <- 或-> 进行终端切换）
    <Ctrl+Alt+ <- 或-> >：切换桌面
    <Alt + F1>：打开主菜单
    <Alt + F2运行>：（重启x窗口：r 重启：reboot 关机：hAlt）
    <Ctrl + Alt + d>：显示桌面
    <Alt + F9>：最小化当前窗口
    <Alt + F10>：最大化当前窗口
    <Alt + F4>：关闭当前窗口
    Print Screen截取全屏
    Alt + Print Screen截取窗口
    <Ctrl+Alt+上下箭头>：切换工作区(Fedora)
    <Alt+F10>：调整窗口的默认大小(Fedora)
```

## linux修改默认打开文件的程序

linux 下全局的文件与程序的关联是通过`/usr/share/applications/defaults.list`文件来设置，该文件保存了个人文件与程序的关联的打开方式。安装了nero之后文件iso的文件默认使用archive manager打开，在`~/.local/share/applications/mimeapps.list`添加一行：

    `application/x-cd-image=nerolinux.desktop;`

在`/usr/share/applications/defaults.list`中添加一行：

    `application/x-cd-image=nerolinux.desktop;`

图形界面下双击iso文件就使用nero打开了。



##联网问题

12.10以及之前的版本很好使，但是13.04之后，不仅校园网老是掉线，解决方法是在panel的网络菜单里面把“启用wifi”关掉。

* 星级译王词典安装目录: /usr/share/stardict/dic 
* 字体目录: home/user/.font/

##关闭盖子时的命令：

在系统设置/电源中

##切换到Ubuntu gnome 经典桌面

注销unity桌面环境，然后选择登录环境为“经典桌面”即可进入。

# Linux重装系统指南(Ubuntu)

* 连上网络(ubuntu暂时关闭wifi)
* 安装chrome，同步书签
* 安装vim，移入配置文件
* 修改主文件夹文件名
* 安装金山wps，解决字体问题
``` 
     fedora:/opt/kingsoft/wps-office/office6/wps: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory
     yum install libstdc++-devel.i686
``` 
* 安装Synaptic软件包管理器
* 卸载libreoffice/firefox/thunderbird/youker-assistant/amazon
* 重新启动计算机
* 安装GLX-Dock并进行配置
* 配置输入法（快捷键等）并重新登录
* 安装clementine/osd-lyrics并进行配置，解决乱码问题，安装解码插件
* 按装bluefish和geany
* 安装快盘，进行配快盘和ubuntu one
* 安装filezilla/okular/meld
* 卸载Rhythmbox/empathy/account-plugin-*
* 安装font-manager

# Linux重装系统指南(Fedora)

* 安装gnome-tweak-tool设置工具
* sudo yum install gnome-tweak-tool
* 安装后在左上角【活动】里可以找到【优化工具】图标打开进行设置
* 安装最快软件源插件：sudo yum install yum-plugin-fastestmirror
* 安装下载加速插件：sudo yum install yum-presto -y
* 安装鼠标右键【在终端中打开】：sudo yum install nautilus-open-terminal
* 配置RPM Fusion
* 卸载相关软件: firefox
* 安装相关软件:gcc/Yumex/Compiz(ccsm)/Cariodock
* 设置自动挂载文件系统fstab
* 升级系统yum update
* 安装vim
* 删除旧内核

    1. 查看当前系统中已安装的内核相关包：# rpm -qa | grep kernel
    2. 查看当前使用的内核：# uname -r
    3. 确定要删除的内核：
    4. 删除内核：# yum remove kernel-...（内核版本名称）使用 yum remove 进行删除，会自动移除：/boot/grub/menu.lst 中的相关启动项


# 软件源设置问题

## ubuntu更新问题

更新管理器在检查软件包的时候总是有如下问题

无法下载 cdrom://Ubuntu 8.10 _Intrepid Ibex_ - Release i386 (20081029.5)/dists/intrepid/main/binary-i386/Packages  请使用 apt-cdrom，通过它就可以让 APT 能识别该光盘。apt-get upgdate 不能被用来加入新的光盘。

无法下载 cdrom://Ubuntu 8.10 _Intrepid Ibex_ - Release i386 (20081029.5)/dists/intrepid/restricted/binary-i386/Packages  请使用 apt-cdrom，通过它就可以让 APT 能识别该光盘。apt-get upgdate 不能被用来加入新的光盘。

无法下载 http://cn.archive.ubuntu.com/ubuntu/dists/intrepid-backports/main/binary-i386/Packages.bz2  Hash 校验和不符

有一些索引文件不能下载，它们可能被忽略了，也可能转而使用了旧的索引文件。

解决方法

把 /etc/apt/sources.list里面有cdrom的几行删掉，或者利用软件中心或新立德包管理器把软件源终中的cdrom去掉。

## Ubuntu更新安装源  

1.sudo cp /etc/apt/sources.list /etc/apt/sources.list.bk

sudo gedit /etc/apt/sources.list

编辑你的源列表，将原来的内容全部删除，添加下面列表中最适合你的源（注意不要全部添加），选择一个最合适你的即可，复制到你的列表中，然后保存列表。

2.sudo apt-get update 更新源列表信息

可以在运行“sudo apt-get update ”时查看一下错误信息，把不能连接的源删除再重新运行“sudo apt-get update ”。

3.sudo apt-get upgrade 升级或者用ubuntu自带的更新管理器升级也可。

网易 Ubuntu 10.10 源（速度很快）

代码:

deb http://mirrors.163.com/ubuntu/ maverick main restricted universe multiverse

deb http://mirrors.163.com/ubuntu/ maverick-security main restricted universe multiverse

deb http://mirrors.163.com/ubuntu/ maverick-updates main restricted universe multiverse

deb http://mirrors.163.com/ubuntu/ maverick-proposed main restricted universe multiverse

deb http://mirrors.163.com/ubuntu/ maverick-backports main restricted universe multiverse

deb-src http://mirrors.163.com/ubuntu/ maverick main restricted universe multiverse

deb-src http://mirrors.163.com/ubuntu/ maverick-security main restricted universe multiverse

deb-src http://mirrors.163.com/ubuntu/ maverick-updates main restricted universe multiverse

deb-src http://mirrors.163.com/ubuntu/ maverick-proposed main restricted universe multiverse

deb-src http://mirrors.163.com/ubuntu/ maverick-backports main restricted universe multiverse

这里强烈推荐用163的速度极快，等我们更改完毕以后千万别忘了apt-get update一下吆！

deb http://tw.archive.ubuntu.com/ubuntu/ karmic main universe restricted multiverse

deb http://tw.archive.ubuntu.com/ubuntu/ karmic-security universe main multiverse restricted

deb http://tw.archive.ubuntu.com/ubuntu/ karmic-updates universe main multiverse restricted

deb http://tw.archive.ubuntu.com/ubuntu/ karmic-proposed universe main multiverse restricted

deb http://tw.archive.ubuntu.com/ubuntu/ karmic-backports universe main multiverse restricted

## RPM Fusion源

Fedora安装Package软件包目前已经由原先的单纯RPM包方式慢慢进化为yum方式了, 其相比原方式而言,不是简单的安装某个RPM包, 而是比较智能化地找到相对应包的联系,如果需要装入某个包,其所依赖的其他各个包也可以被安装,相比原先的方式有了相当大的进步. 但Fedora自带的软件库不是很丰富,因此RPM fusion就产生了,其主要目的是为Fedora/RedHat等Linux发行包提供软件包支持,其合并了 Dribble/ Freshrpms和rpm.livna.org三大软件包仓库,很多原先不支持的软件包,我们都可以通过RPM Fusion很容易的找到,例如Fedora 10下的mplayer等等.     RPM Fusion的官方站点: http://rpmfusion.org/ 

RPM Fusion的安装方法: 

1. 首先从RPM Fusion网站下载相应的RPM Fusion包,或者从本地下载.
2. 
原网站:    

http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm        http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm         本地链接:

rpmfusion-free-release-stable.noarch.rpm

rpmfusion-nonfree-release-stable.noarch.rpm

2. 切换为root用户

3. 安装rpm fusion

rpm -ivh rpmfusion-free-release-stable.noarch.rpm

rpm -ivh rpmfusion-nonfree-release-stable.noarch.rpm

4. 此时运行yum时,就已经可以利用到rpm fusion所对应的软件库了.  
5. 


## ATrpms源

因为rpmfusion并不包含ATrpms软件库,因此建议执行下面的步骤增加ATrpms源.

ATrpms官方网站:http://atrpms.net/

安装方法见官方网站。

# FTP资源

Linux相关                                                

ftp://ftp.tsinghua.edu.cn   各种镜像、Linux软件                
ftp://mirror.pku.edu.cn/pub/linux/                                    
ftp://219.238.157.219/pub/                                            
ftp://eelinux.3322.org                                                
ftp://166.111.72.5/Linux                                        
ftp://166.111.121.3/Linux/                               
ftp://166.111.68.183/pub/Linux/                                 

Debian升级镜像

ftp://debian.ustc.edu.cn/          这个比较全            
ftp://ftp.tsinghua.edu.cn/mirror/debian 
ftp://ftp.sjtu.edu.cn/mirror/sites/ftp.debian.org/
ftp://mirror.dlut.edu.cn/ 
ftp://debian.nctu.edu.tw/ 

http://debian.cn99.com/   

http://debian.okey.net/   

ftp://deb.distro.cn       

Gentoo升级镜像                      

ftp://ftp.sjtu.edu.cn/mirror/sites/gentoo 

ftp://ftp.tsinghua.edu.cn/mirror/gentoo   

ftp://166.111.172.55/pub/mirror/gentoo   

rsync://gentoo.net9.org/gentoo-portage  

Fedora:apt-rpm

ftp://ftp.tsinghua.edu.cn/mirror/ayo.freshrpms.net/pub/freshrpms/ayo/fedora/linux/2/i386/ 

rpm ftp://ftp.sjtu.edu.cn apt/fedora/2/i386 os updates freshrpms 

ftp://ftp.ctex.org/?

ftp://ftp.kernel.org/pub/

ftp://ftp.gnu.org

# 乱码及编码问题

##总论

基本码：

ascii

中国制定的编码：（gb代表国家标准，其中gbk不是国家标准，但其兼容gb2312.并扩充了许多字符）

gb2312

gbk

gb18030

世界统一编码：

utf

linux系统中文件名内容为urf8编码

windows系统中文件名默认为gbk编码

多数文档使用gbk编码，系统采用utf8编码

##无中文输入法导致的乱码

1、ibus输入法

Ubuntu 系统安装后已经自带了ibus输入法，在英语环境下默认不启动。

配置ibus自动启动可以在ubuntu系统菜单上选择System --- Preferences --- Startup Applications，在该窗口中增加一个程序：

Name: ibus-daemon

Command: ibus-daemon -d -x -r

ibus默认提供的中文输入法比较弱智，需要额外安装ibus-pinyin，命令如下：

sudo apt-get install ibus-pinyin

这 时，还需要将ibus-pinyin输入法启动。在ubuntu系统菜单上选择System --- Preferences --- IBus Preferences，在Input Method页中的“Select an input method”下拉框中选择增加Chinese – Pinyin，就是图标中有个一个大大的“拼”字的那一个，然后点击Add按钮，最后通过Up按钮将该输入法移动到最上面。

系统重启后，通过Ctrl + 空格即可调出ibus输入法。

ibus输入法总体来说不错，但是在我的环境下发现无法在部分Java程序中调出来，例如Netbeans、OpenProj。

2、fcitx输入法

由于ibus的缺陷，所以我尝试了fcitx，使用下来也非常不错，而且可以在Java程序中正常使用，只是在这种情况下光标跟随有些问题，输入界面会停 留在屏幕最下端，但是可以接受，比起ibus不能使用要好多了。

安装fcitx：

sudo apt-get install fcitx

启动fcitx：

im-switch -s fcitx

注销后重新登录，fcitx就会生效。

如果需要切换回ibus，可以运行im-switch -s ibus，然后注销，重新登录。

fcitx同样可以通过Ctrl + 空格调出，这时会发现fcitx显示的中文是方框，因此需要修改fcitx的配置。Fcitx的配置文件在~/.fcitx/config，该文件为 GBK编码，在Ubuntu下显示不正常，可以通过如下方式操作：

cd ~/.fcitx

iconv -f gbk -t utf8 config > config.tmp

编辑config.tmp文件：

显示字体(中)=WenQuanYi Micro Hei

显示字体大小=10

使用粗体=0

保存退出，然后运行命令：

iconv -f utf8 -t gbk config.tmp > config

注销后重新登录，fcitx显示正常。

对于搜狗输入候选字乱码问题，先运行

sudo apt-get install fcitx-module-kimpanel

然后注销或者重启，一般就可以了



## utf8 和 UTF-8 有什么区别

“UTF-8”是标准写法，在windows下边英文不区分大小写，所以也可以写成“utf-8”。“UTF-8”也可以把中间的“-”省略，写成“UTF8”。一般程序都能识别，但也有例外（如下文），为了严格一点，最好用标准的大写“UTF-8”。

在MySQL数据库中只能使用“utf8”

　　在MySQL的命令模式中只能使用“utf8”，不能使用“utf-8”，也就是说在PHP程序中只能使用“set names utf8(不加小横杠)”，如果你加了“-”此行命令将不会生效，但是在PHP中header时却要加上“-”，因为IE不认识没杠的“utf8”，原因 见下文。

在IE浏览器中只能使用“utf-8”

　　IE中如果使用了“utf8”，页面可能会 空白 或 显示为乱码。

　　但是在其它浏览器却是正常的，原因是因为：其它浏览器默认使用的是UTF-8的编码，如果无法识别页面的编码就会用默认的UTF-8来解码，但 是IE的默认编码是GB2312，所以默认的话就。。。。。（其它浏览器指“FireFox”、“Chrome”、“Opera”）

总结　　

　　【只有在MySQL中可以使用“utf-8”的别名“utf8”，但是在其他地方一律使用大写“UTF-8”。】

　　具体为：

　　　　在命令“mysql_query(set names utf8)”外一律用大写“UTF-8”。



##网页上Flash中的中文显示为方框的解决办法

编辑/etc/fonts/conf.d/49-sansserif.conf文件，作如下修改：

<edit name="family" mode="append_last">

<string>WenQuanYi Micro Hei</string>

</edit>

## Java程序部分中文显示为方框的解决办法

在$JAVA_HOME/jre /lib/fonts目录下建立fallback目录，将中文字体文件复制（或link）到fallback目录。

sudo mkdir $JAVA_HOME/jre/lib/fonts/fallback

sudo ln /usr/share/fonts/truetype/wqy/wqy-microhei.ttc $JAVA_HOME/jre/lib/fonts/fallback/

## “GBK乱码”，参考

乱码的样子类似：  

à??ü òá??à3?￡???1,°2à??ü òá??à3?￡???1 

解决方法： 

使用convmv 

把乱码文件名文件复制在一个空目录里运行（这样错了也不怕）： 

代码: 

convmv -r -f utf8 -t iso88591 --notest --nosmart * && convmv -r -f gbk -t utf8 --notest --nosmart *       

## “ascii乱码”参考 

乱码的样子类似： 

%E5%8C%BB%E4%BF%9D 

解决方法： 

1.使用uni2ascii 代码: 

echo 乱码原文 | ascii2uni -a J 

2.安装nautilus-filename-repairer0.06（官方有源码，但是依赖问题，我还没安装成功，而0.05版与现在的nautilus有点小小的合作障碍，只能看不能改名) 

3.用chromeplus-1.3.3.1下载（因为这类乱码主要在用ff（默认utf8）下载qq群里的文件之后产生，用chromeplus(默认GBK)下就没问题了）      

另外，至于文件里面内容的乱码问题可以搜索enca.

##解决Rhythmox乱码问题： 

安装Rhythmox：sudo apt-get install rhythmbox 

安装mid3iconv：sudo apt-get install python-mutagen 

mid3iconv -h 



## Clementine乱码问题

安装mid3iconv：sudo apt-get install python-mutagen 

mid3iconv -h

Clementine不支持utf8，需要吧所有的mp3歌曲转换为gbk格式，wma好像不用转就可以

mid3iconv -e gbk *.mp3(由于不能带-r参数，所以要依次进入每个文件夹)

另外clementine采用gstreamer作为后端，需要安装gstreamer插件：

1 如果想支持mp3，需要安装gstreamer-0.10-plugins-bad和gstreamer-0.10-plugins-ugly

2 如果想支持wma，需要安装gstreamer-0.10-ffmpeg

3 如果想支持mms流媒体，需要安装gstreamer plugins for mms

另外Clementine基于Amarok，所以支持Amarok的插件一般都支持Clementine，比如osdlyrics。

##转换文件内容编码: 

    file -i <file name> 检测文件编码
    iconv --help 

##转换文件名编码

    sudo apt-get install convmv 
    convmv --help 
    convmv -f gbk -t utf8 -r --notest files 
    convmv -r -f utf8 -t iso88591 * --notest --nosmart && convmv -r -f gbk -t utf8 * --notest --nosmart 

##解决gedit乱码问题： 

    gsettings set org.gnome.gedit.preferences.encodings auto-detected "['GB18030', 'GB2312', 'GBK', 'UTF-8', 'BIG5', 'CURRENT', 'UTF-16']" 
    gsettings set org.gnome.gedit.preferences.encodings shown-in-menu "['GB18030', 'GB2312', 'GBK', 'UTF-8', 'BIG5', 'CURRENT', 'UTF-16']" 

##解决PDF中文乱码： 

安装poppler-data来解决： sudo apt-get install poppler-data 

##解决rar文件乱码

使用rar 

##解压zip文件乱码

最近碰到这个问题，网上搜了一圈，都是什么unzip -O，一点用都没有，这些哥们估计是直接复制，用都没用过。后来找了个终极方法，用python的脚本来解压，试了下，还真管用！！！以下为python脚本的代码，新建文件jieya.py，写入以下代码：

```python
    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import os
    import sys
    import zipfile

    print "Processing File " + sys.argv[1]
    file=zipfile.ZipFile(sys.argv[1],"r");
    for name in file.namelist():
        utf8name=name.decode('gbk')
        print "Extracting " + utf8name
        pathname = os.path.dirname(utf8name)
        if not os.path.exists(pathname) and pathname!= "":
            os.makedirs(pathname)
        data = file.read(name)
        if not os.path.exists(utf8name):
            fo = open(utf8name, "w")
            fo.write(data)
            fo.close
    file.close()
```

然后zip文件跟jieya.py放在同一级目录，运行命令python  jieya.py file.zip，哦了！

## smplayer 中文字幕乱码解决方法 

1。打开选项－》首选现：选择字幕选项卡。 

2。找到“默认字符编码”选项，在下拉框中选择“简体中文（cp936）” 

3。再打开“字体”页卡（上边），选择“系统字体”在下拉选框中选择一种简体中文字体，如 Weu Quanyi Zen Hei 等。 

经过以上设置，smplayer已经可以正常显示中文字幕了，你还可以在刚才的位置作一下扩展设置，如“文本颜色”“显示位置”的，这个读者按自己喜好去作罢。

## VLC播放器显示文件名乱码

初选项中修改一种支持中文的字体



# 常用软件及相关配置问题

pdf阅读器:okular evince

文本编辑器：vim，emacs，gedit

音乐播放软件：clementine

rhythmbox歌词显示工具：osd-lyrics

桌面美化工具：compiz

视频播放器：KMPlayer

eD2k下载:aMule

编程工具:bluefish

pdf合并工具——pdftk

输入法：ibus+fcitx  重新启动Xwindow完成，按 Ctrl + 空格键激活输入法。当不能切换输入法时，把键盘-拼音输入法调到顶部。

微软字体包：sudo apt-get install msttcorefonts 

字体管理器:font manager 

笔记软件:为知笔记：直接用tar.gz包

网盘:云诺网盘(菜单会有部分变成英文,不宜使用,可以替换为坚果云) /Dropbox

软件包工具:新立得(Synaptic) 

磁盘管理器：LVM/GParted 

浏览器：Chrome 

词典：goldendict 

3D建模工具：blender 

图片处理工具：GIMP 

Dock:GLX-Dock 

视频编辑–Openshot

BT下载：Transimssion

ftp客户端Filezilla

邮件客户端：thunderbird 

虚拟光驱软件：Furius ISO Mount

文件对比软件：meld

脑图软件：xmind

远程控制：vncview

数据处理软件：octave（部分兼容matlab）

记录、保存和播放终端会话软件: ttyrec 和 ttyplay

垃圾清理软件：BleachBit

Audio CD Extractor（音频CD提取器）

又名“音乐榨汁机”、“Sound Juicer”。

能把CD转成flac、ogg、mp3等格式。

官方主页：http://www.burtonini.com/blog/computers/sound-juicer 

Sound Converter（声音转换程序）

支持flac、ogg、mp3、wav、m4a等格式间批量互转。

官方主页：http://soundconverter.berlios.de 

curl是利用URL语法在命令行方式下工作的文件传输工具。

流程图、UML、脑图工具

IHMC CmapTools:http://cmap.ihmc.us/

yED Grahp Editor:http://www.yworks.com/en/index.html

##搜狗输入法安装指南

由于 Ubuntu 12.04 LTS 自带的 Fcitx 版本较旧，需要先通过 PPA 升级，才能安装下载的 deb 软件包。

1. 点击左上角的图标打开Dash，输入update-manager，点击更新管理器。
2. 在更新管理器中，选择菜单：编辑->软件源，点击添加...按钮，在弹出的窗口中输入ppa:fcitx-team/nightly， 点击添加源。
3. 然后点击重新载入。
4. 打开Ubuntu软件中心，在搜索栏输入fcitx，将会搜出fcitx，然后按照一般软件安装步骤安装即可完成升级。
5. 双击下载的 deb 软件包安装搜狗输入法。

##解决金山wps字体问题

将字体解压到~/.fonts目录，然后重启wps即可。

说明：这些文件为微软版权所有，使用这些字体请自行确定拥有这些字体的使用授权（比如说有某版本windows授权即可）

另外据一部分用户反映，如果系统安装了xfonts-mathml可能导致符号无法显示。

经过查证，发现是因为xfonts-mathml中也存在一个字体叫Symbol导致的。

如果安装上述字体后仍存在乱码现象，请尝试移除xfonts-mathml包。

## libreoffice中PPT字体便粗问题

Tools → Options... → LibreOffice → View → Graphics output (取消钩选Use hardware acceleration)  

##小企鹅输入法突然无法使用

查看一下是否安装了ibus，可在系统设置中的语言支持中重新把输入法改为ibus



# 主文件夹里的中文文件夹改成英文文件夹

打开终端，在终端下输入命令：

 

export LANG=en_US

xdg-user-dirs-gtk-update

 

这个时候会弹出一个配置界面，提示是否将中文目录切换为英文目录。选中不再提示，确定。系统会删除没有内容的中文目录，而有内容的目录会保持。并创建8个相应的英文目录如下：“Desktop”、“Download”、“Templates”、“Public”、“Documents”、“Music”、“Pictures”、“Videos”。此时，您在“位置”里看到的常用中文目录已经变成英文目录；

再执行：

export LANG=zh_CN.UTF-8     

以显示中文

#软件安装使用问题

## Rdseed的安装

1、下载: 

http://www.iris.edu/pub/programs/rdseedv5.2.tar.gz

2、解压: tar -xzvf rdseedv5.2.tar.gz

3、编译：

1）在makefile中找到这几句

CC = cc 

# for cygwin add the -D_CYGwin flag, for users of windows pcs

CFLAGS     = -O -m32 -g -D_CYGwin



# to compile rdseed as a 32-bit application

#CFLAGS     = -O -m32 -g 



2）将CYGwin行注释掉，取消最下面一行的注释：

CC = cc 

# for cygwin add the -D_CYGwin flag, for users of windows pcs

#CFLAGS     = -O -m32 -g -D_CYGwin



# to compile rdseed as a 32-bit application

CFLAGS     = -O -m32 -g 



3）输入make clean



4）输入make



4、将编译好的rdseed文件拷贝靠bin目录下：sudo cp rdseed /usr/bin/



5、输入rdseed即可进入。



注：64位系统下可以直接使用已编译好的文件:cp -p rdseed.rh6.linux_64 /usr/local/bin/rdseed 

## SAC安装

1、软件包可以在下面给出的网站上申请，认真填写，在平台选择处选择Linux 32 位或64位（如果有兴趣也可以选择一个source code）。注意不要图省事一次把所有包都申请了，那样管理员会专门给你发邮件要你解释的。最好使用学校邮箱或者较正规的邮箱，否则有被拒的可能。若验证通过，三个工作日内即可收到邮件。

申请网址：http://www.iris.edu/forms/sac_request.htm

2、对sac 文件压缩包直接解压，会出现sac文件夹，里面包含了多个文件夹：

tar xvfz netcdf-3.6.3.tar.gz

for i in *.bz2;do tar jxvf $i;done



3、将整个sac 文件夹拷到某目录下（SAC 推荐安装目录为/usr/local）：

sudo cp -r sac /usr/local

4、编辑.bashrc 设置环境变量

gedit ~/.bashrc

在.bashrc 的最后添加如下语句



export SACHOME=/usr/local/sac

export SACAUX=$SACHOME/aux

export PATH=$SACHOME/bin:$PATH



5、终端输入source ~/.bashrc 6、终端输入sac（注意要小写），看到版本号等信息即安装成功。
6、
## SEISMIC UNIX 安装实例（Fedora Core /Ubuntu 系统 ）

前提 ：1 由于 fedora core 系统在安装过程中 是依据个人的选择而指定安装软件包的，在SU的安装 过程中如果遇到某项安装无法进行，则很可能是某个包没有被安装到系统是，特别是在安装时 ，一定要选上 MESA－LibGLU，和 MESA－LibGL这 两个包 ，这两个 包 在 “x系统开发 "中 可以找到 。

2 此外，SU 的安装过程中还需要 GLUT包 ，这需要在网上下载。下载方法 ： 在GOOGLE上 输入 FREEGLUT ，即可看到相关链接 。 

安装具体过程 ：

1 SU 安装环境的建立之一

主要有两点。1，在终端 中输入＃export CWPROOT＝／home/yourname/su 说明，路径 ／home/yourname/su 为自己任意指定的路径 ，以后SU将在这个路径下进行安装，例如 ，我的路径是 ／home/wh/su.

2 在终端 中 输入 ＃export PATH=$PATH：/home/yourname/su/bin 说明，如上，本部分路径为自己任意指定的路径（前一部分要和上面一致），而本句的意思是将/home/yourname/su/bin中的命令加入的LINUX系统的搜索路径。

2 SU在本系统中安装环境的建立及安装

这里的内容根据系统的不同而不同，但大体是一致的。这里将分部分进行说明。

（1）将CWP－SU拷贝到／home/yourname/su，然后 解压 ＃tar zxvf cwp-su.xx,解压后将会看到出现了一个新 目录 src,进入此目录。

（2）阅读文件readme-to-install,可以看到安装SU的大体步骤。

（3)阅读文件makefile.config,这是成功安装SU的关键。里面对如何安装SU说明的很清楚 。本文将介绍里面的关键几点。

2－1 执行make install的准备工作

主要是需要修改makefile.config中的两项。

1，将 ENDIANFLAG = -DCWP_LITTLE_ENDIAN 句激活。

2，将 include $(CWPROOT)/src/Rules/gnumake.rules 句激活，并屏蔽掉 #include $(CWPROOT)/src/Rules/oldmake.rules 句,修改后 保存，然后运行 make install就可以成功安装。

2－2 执行make xtinstall, 不需要修改，直接运行make xtinstall

2－3 执行make finstall 的准备工作

这里需要指定fortran编译器，在fedora core 6系统中，GCC的版本是4。1。1，因此可以直接利用GCC中的编译器gfortran,即在makefile.config中的相关句改为FC = gfortran,其他的系统改为相应的fortran编译器即可。

2－4 执行make mglinstall 的准备工作

这里就需要最先提到的LIBGLU，和 GLUT这两个相关库了 。LIBGLU在安装FC6时候就可以安装入系统。其默认安装路径为：usr/lib,和 usr/include. 而GLUT需要从网上下载。值得 注意的是，要下载较新的FREEGLUT。下载后解压安装。FREEGLUT的安装为常规安装 ，装好后可以发现其安装路径为：usr/local/lib,和 usr/local/include, 因此，就不需要对makefile.config中相关部分作任何改动。

至此，SU的主体部分安装完毕，其余两点为可选项。其道理是类似，即对 makefile.config                                中的相关句作适当的改动。

补充说明：1 在以后每次运行SU的时候，都需要输入export那两个语句。如果不想每次都输入，可以修改.bashrc文件(在我的系统中这个文件在/home/wh/.bashrc)将export那两句添加进入即可。

2 如果按照本文所说的过程进行安装，但发现其中某一步出现错误，那很可能是系统在 安装的过程中没有安装相应的库，这时，仔细分析错误描述，就可以发现到底是那些库没有安装，然后在GOOGLE中找到相应的库下载安装即可（或用 YUM命令）。

最后，上传一张SU在DEMO的例子结果展示图片。



$(CWPROOT)/src/Rules/oldmake.rules 句,修改后 保存，然后运行 make install就可以成功安装。补充说明：1 在以后每次运行SU的时候，都需要输入export那两个语句。如果不想每次都输入，可以修改.bashrc文件(在我的系统中这个文件在/home/wh/.bashrc)将export那两句添加进入即可。





××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××××

1 刚装上ubuntu后，首先需要将网络设置好，并选择合适的软件源。对于教育网用户，推荐中国科大的软件源，请参考下面blog中的设置方法：http://hi.baidu.com/from/blog/item/30db2e734f516e1f8701b0a4.html



2 预装7个软件包，即在终端中输入如下命令：

sudo apt-get install build-essential

sudo apt-get install libx11-dev

sudo apt-get install libxt-dev

sudo apt-get install libglut3-dev

sudo apt-get install libxmu-dev

sudo apt-get install libxi-dev

sudo apt-get install gfortran



3 su安装的准备工作，一共有3步：



1）输入： export CWPROOT=/home/yourname/su   注：这里的/home/yourname/su为你下载并解压su所在的目录

2）输入：export PATH=$PATH:/home/yourname/su/bin 注：/home/yourname/su 的意义同上，bin为解压su后所生成的目录。

3）进入/home/yourname/su/src 这个目录，可以看到makefile.config 这个文件，要修改里面的三项,输入命令：gedit makefile.config , 然后修改所打开的文件：



1，将 ENDIANFLAG = -DCWP_LITTLE_ENDIAN 句激活（即去掉#）。

2，将 include $(CWPROOT)/src/Rules/gnumake.rules 句激活，并屏蔽掉 include$(CWPROOT)/src/Rules/oldmake.rules 句,修改后 保存。

3, 将FC=g77, FC=f77,FC=ifort 屏蔽掉，激活FC=gfortran

4，将OPTF = -O -static -mcpu=i686 -fno-globals -fno-automatic -fno-second-underscore 屏蔽，激活OPTF = -O -static -march=i686 -fno-automatic -fno-second-underscore



4 正式安装,分别输入：

1）make install

2) make xtinstall

3）make finstall

4) make mglinstall

至此su主体已经成功，参见下图：



补充说明：1 在以后每次运行SU的时候，都需要输入export那两个语句。如果不想每次都输入，可以修改.bashrc文件(在我的系统中这个文件在/home/wh/.bashrc)将export那两句添加进入即可。



2   （2011.11）libglut3-dev已经被freeglut3-dev替换。即:  sudo apt-get install freeglut3-dev



3  在最新版本su下 ，需添加 OPTF = -O -static -march=i686 -fno-automatic -fno-second-underscore 至makefile.config文件中。

## wine

winetricks 用wineTricks令你的wine更完整

分类： Linux系统学习记录 2011-04-26 22:11 4493人阅读 评论(0) 收藏 举报

微软windowsscriptingmfcvbbasic



Linux下最有名的windows环境模拟器就是WINE了。它提供了一个可以模拟WINDOWS环境的基本平台，在这上面你几乎可以运行任何你想运行的windows程序。



什么？你不相信？不要告诉我你的程序运行时总是提示缺少mfc42.dll。。。



默认的wine环境缺少很多win平台的库，而且最可恨的是，system32目录下竟然没有regedit程序。



 



下面我来介绍一下，如何让你的winE环境更为完整。



我示范的linux发行版是ubuntu 9.04， wine的版本号是1.1.26



 



1.准备正确的注册表编辑器



首先将/home/你的用户名/.wine/dosdevices/c:/windows下的regedit.exe程序复制到system32目录下。



命令：



sudo cp /home/你的用户名/.wine/dosdevices/c:/windows/regedit.exe /home/你的用户名/.wine/dosdevices/c:/windows/system32/



2.下载并安装winetricks



wget http://www.kegel.com/wine/winetricks



chmod +x winetricks



sudo mv winetricks /usr/local/bin



3。用winetricks安装必须的win支持库。这一步很关键。



命令行中输入winetricks



然后勾选colorprofile、corefonts、d3dx9、fontfix、fontsmooth-gray、fontsmooth-rgb、fontsmooth-bgr、gdiplus、mfc40、mfc42、



msxml3、msxml4、msxml6、riched20、riched30、tahoma、urlmon、vb6run、vcrun6、vcrun2003、vcrun2005、vcrun2008、ie6、allfonts



然后选择安装。



4。下面输入winetricks后，勾选dotnet11、dotnet20、vjrun20并安装。



都安装完毕以后，有兴趣的朋友可以尝试安装一下powerdesigner看看能不能用。哈哈。



更多信息请参见http://wiki.winehq.org/winetricks



 



 



wine的其中一个开发者DanKegel写的一个安装windows有关库和软件的小程序，非常有用！



介绍一下使用方法：



1、打开终端，输入

wget



http://www.kegel.com/wine/winetricks



2、再输入

sudo apt-get install cabextract



3、再输入

chmod +x winetricks



4、最后

./winetricks



在打开的窗口中，可以看到程序所支持的一个软件列表

代码:

art2kmin 微软 Access 2000 运行时.

colorprofile 标准 RGB 颜色配置文件

comctl32 微软 common controls 5.80

comctl32.ocx 微软的comctl32.ocx 和comctl.ocx,VB6的comctl32外壳

corefonts 微软 Arial, Courier, Times 字体

dcom98 微软 DCOM, 替换wine所自带的

dirac0.8 the obsolete Dirac 0.8 directshow filter

directx9 微软 DirectX 9

divx divx 视频编码

dotnet11 微软 .NET 1.1

dotnet20 微软 .NET 2.0

ffdshow ffdshow 视频编码

flash Adobe Flash Player ActiveX 与 firefox 插件

fontfix Fix bad fonts which cause crash in some apps (e.g. .net).

gdiplus 微软 gdiplus.dll (须安装powerpoint)

gecko HTML 渲染引擎(Mozilla)

icodecs Intel 媒体编码 (Indeo)

jet40 微软 Jet 4.0 Service Pack 8

liberation Red Hat Liberation 字体 (Sans, Serif, Mono)

mdac25 微软 MDAC 2.5: 微软 ODBC 驱动, etc.

mdac27 微软 MDAC 2.7

mdac28 微软 MDAC 2.8

mfc40 微软 mfc40 (Microsoft Foundation Classes from Visual C++ 4)

mfc42 微软 mfc42 (包含于下面的vcrun6)

mono19 mono-1.9.1-gtksharp-2.10.4-win32-2

msi2 微软 Installer 2.0

msls31 微软 Line Services 3.1 (needed by native riched?)

msxml3 微软 XML version 3

msxml4 微软 XML version 4

msxml6 微软 XML version 6

ogg ogg 过滤器和编码器: flac, theora, speex, vorbis,



pdh 微软 pdh.dll (Performance Data Helper)

quicktime72 苹果 Quicktime 7.2

riched20 微软 riched20 and riched32

riched30 微软 riched30

tahoma 微软 Tahoma 字体 (not part of corefonts)

vb3run 微软 Visual Basic 3 运行时

vb4run 微软 Visual Basic 4 运行时

vb5run 微软 Visual Basic 5 运行时

vb6run 微软 Visual Basic 6 运行时

vcrun6 微软 Visual C++ 6 sp4 运行库 (包括mfc42.dll, msvcp60.dll, msvcrt.dll)

vcrun2003 微软 Visual C++ 2003 运行库 (包括mfc71.dll,msvcp71.dll,msvcr71.dll)

vcrun2005 微软 Visual C++ 2005 运行库 (包括mfc80.dll,msvcp80.dll,msvcr80.dll)

vcrun2005sp1 微软 Visual C++ 2005 sp1 运行库

vcrun2008 微软 Visual C++ 2008 运行库 (包括mfc90.dll,msvcp90.dll,msvcr90.dll)

vjrun20 微软 Visual J# 2.0 运行库 (需要安装 dotnet20)

wmp9 微软 windows Media Player 9

wmp10 微软 windows Media Player 10

wsh51 微软 windows Scripting Host 5.1

wsh56 微软 windows Scripting Host 5.6

wsh56js 微软 windows scripting 5.6, 只有jscript,没有cscript

wsh56vb 微软 windows scripting 5.6, 只有vbscript,没有cscript

xvid xvid 视频编码



autohotkey Autohotkey (open source gui scripting language)

firefox3 Firefox 3

kde KDE for windows installer

mpc Media Player Classic

vlc VLC media player



allfonts 以上所有字体 (corefonts, tahoma, liberation)

allcodecs 以上所有媒体编码 (xvid, ffdshow, icodecs)

fakeie6 在注册表中写入IE6已安装信息

native_mdac Override odbc32 and odbccp32

nt40 Set windows version to nt40

win98 Set windows version to windows 98

win2k Set windows version to windows 2000

winxp Set windows version to windows XP

vista Set windows version to windows Vista

winver= Set windows version to default (winxp)

volnum Rename drive_c to harddiskvolume0 (needed by some installers)



其中，要安装QQ2008的话，只需安装flash gecko msls31 riched20 vcrun6即可。



## GTK

我利用此方法成功在Ubuntu?12.04下安装GTK 2.24.10  记录一下

1、安装gcc/g++/gdb/make 等基本编程工具

sudo apt-get install build-essential

2、安装 libgtk2.0-dev libglib2.0-dev 等开发相关的库文件

sudo apt-get install gnome-core-devel

3、用于在编译GTK程序时自动找出头文件及库文件位置

sudo apt-get install pkg-config

4、安装 devhelp GTK文档查看程序

sudo apt-get install devhelp

5、安装 gtk/glib 的API参考手册及其它帮助文档

sudo apt-get install libglib2.0-doc libgtk2.0-doc

6、安装基于GTK的界面GTK是开发Gnome窗口的c/c++语言图形库

sudo apt-get install glade libglade2-dev

7、安装gtk2.0 或者 将gtk+2.0所需的所有文件统通下载安装完毕

sudo apt-get install libgtk2.0-dev

查看GTK库版本

1.查看 2.x 版本

pkg-config --modversion gtk+-2.0

2.查看pkg-config的版本

pkg-config --version

3.查看是否安装了gtk

pkg-config --list-all grep gtk

测试程序

代码如下：

//Helloworld.c

#include <gtk/gtk.h>

int main(int argc,char *argv[])

{

    GtkWidget    *window;

    GtkWidget    *label;

    

    gtk_init(&argc,&argv);

    

    /* create the main, top level, window */

    window = gtk_window_new(GTK_winDOW_TOPLEVEL);

    

    /* give it the title */

    gtk_window_set_title(GTK_winDOW(window),"Hello World");

    

    /* connect the destroy signal of the window to gtk_main_quit

    * when the window is about to be destroyed we get a notification and

    * stop the main GTK+ loop

    */

    g_signal_connect(window,"destroy",G_CALLBACK(gtk_main_quit),NULL);

    

    /* create the "Hello, World" label */

    label = gtk_label_new("Hello, World");

    

    /* and insert it into the main window */

    gtk_container_add(GTK_CONTAINER(window),label);

    

    /* make sure that everything, window and label, are visible */

    gtk_widget_show_all(window);

    

    /* start the main loop, and let it rest until the application is closed */

    gtk_main();

    

    return 0;

}

编译运行

1、编译

gcc -o Helloworld Helloworld.c `pkg-config --cflags --libs gtk+-2.0`

2、运行

./Helloworld

## wubi

首先，空出一个盘符（如F盘），将下载的ubuntu-12.04-desktop-i386.iso单独放在另一个盘如（D盘），从D盘里的镜像中解压出 wubi.exe，并将ubuntu-12.04-desktop-i386.iso和 wubi.exe放在同一个文件夹下用英文命名（如ubuntu-12.04），然后双击 wubi.exe会安装而不会再去下载镜像，安装过程中让你选择盘符时选择想要安装盘如F盘。祝你好运！



你直接解压镜像文件，然后把解压出来的wubi.exe跟原先下载好的ubuntu-12.04-desktop-i386.iso放在同一个文件夹中，双击运行wubi，然后按照提示一步步安装即可。需要注意的是，最好断开网络再安装，不然的话安装出来有可能会变成64位的，我曾经发生过这样的悲剧。

## pdftk处理PDF文件



Pdftk是由Sid Steward写的一个PDF增强软件，它可以合并/分割PDF文档、解开必要的输入密码、输出加密、给PDF文档加水印、从PDF文档中解出附件、将PDF文档变成一页等等，能够做到操作PDF文档的所有事情。 



合并

pdftk 1.pdf 2.pdf 3.pdf cat output 123.pdf

或

pdftk A=1.pdf B=2.pdf cat A B output 12.pdf

或

pdftk *.pdf cat output combined.pdf





多个pdf中抽出部分页合成新pdf

pdftk A=one.pdf B=two.pdf cat A1-7 B1-5 A8 output combined.pdf





128位加密，限制一切权限

pdftk mydoc.pdf output mydoc.128.pdf owner_pw foopass





同上，但打开不需密码

pdftk mydoc.pdf output mydoc.128.pdf owner_pw foo user_pw baz





同上，可打印

pdftk mydoc.pdf output mydoc.128.pdf owner_pw foo user_pw baz allow printing





解密

pdftk secured.pdf input_pw foopass output unsecured.pdf





合并，其中一个加密，合并后文件不加密

pdftk A=secured.pdf mydoc.pdf input_pw A=foopass cat output combined.pdf





Uncompress PDF Page Streams for Editing the PDF Code in a Text Editor

pdftk mydoc.pdf output mydoc.clear.pdf uncompress





修复 Repair a PDF's Corrupted XREF Table and Stream Lengths (If Possible)

pdftk broken.pdf output fixed.pdf





Burst a Single PDF Document into Single Pages and Report its Data to doc_data.txt

pdftk mydoc.pdf burst





Report on PDF Document Metadata, Bookmarks and Page Labels

pdftk mydoc.pdf dump_data output report.txt

## Wireshark

Wireshark是一款非常流行的协议分析软件。自然可以网络抓包的需求。

 sudo apt-get install wireshark 

出于安全方面的考虑，普通用户不能够打开网卡设备进行抓包，wireshark不建议用户通过sudo在root权限下运行，

wireshark为ubuntu（Debian）用户提供了一种在非root下的解决方法。

详细解释可以参考：

/usr/share/doc/wireshark-common/README.Debian  http://nariver.com/usr/share/doc/wireshark-common/README.Debian）

具体步骤：

sudo dpkg-reconfigure wireshark-common

press the right arrow and enter for yes

sudo chmod +x /usr/bin/dumpcap

## Vimium、Vimperator 浏览器插件

今天的主角是 Vimium 和 Vimperator，相信很多人一看到上面的两个名字就已经联想到了经典的 Vim 编辑器 —— 这是一款被无数人誉为编辑器中的神器。它完全只使用键盘操作，虽然 Vim 的入门学习曲线比较陡峭，但一旦熟悉之后，你将会被其极之高效且无比强大的键盘流操作深深折服，而且一点都不会比使用鼠标的编辑器慢，相反，用得好的高手往往效率比使用一般win下的编辑器效率要高得多。

Vimium 和 Vimperator 就是两款参考了 Vim 按键操作方式和理念而来的浏览器插件，可以让你几乎全程使用键盘快捷键来上网，大大提高浏览效率。如果你本身是一位 Vim 用户的话，你几乎没有学习的门槛，很快就能找到使用 Vim 编辑器那种流畅操作的“熟悉感”！不过，如果你之前完全没有接触过 Vim，那么就得稍微了解学习一下了。当然，你也可以将其看作是网页浏览器的快捷键工具，记住一些常用操作就能体验一番高手们行云流水地用键盘工作时的畅快感了。Vimium 是一款 Chrome 浏览器中的插件，而 Vimperator 则是 FireFox 火狐浏览器的插件，虽然名字不同，但是他们的操作基本上没有什么区别，所以下面我就以介绍 Vimium 为主吧。Vimperator 的同学可以作为参考一下.按 shift+/ （chrome）或者是进入设置页面（firefox+chrome），可以找到更详细的的帮助。甚至，你还可以在设置中按照你自己的习惯替换掉一些键。如果有些网站你不想它占用你的按键的话，可以在设置中加入例外，比方说豆瓣电台（小问题：你知道豆瓣电台的快捷键吗？）

## glxgears

glxgears是一个测试你的Linux是否可以顺利运行2D、3D的测试软件。这个程序弹出一个窗口，里面有三个转动的齿轮，屏幕将显示出每五秒钟转动多少栅，所以这是一个合理的性能测试。

窗户是可以缩放的，栅数多少极大程度上依赖于窗口的大小。如果你的显示卡够好，而且你的驱动程序也配合得很好，那齿轮就跑得越快。这里请记录下FPS数字（每秒的帧速度）以鉴别3D加速效果。

查询OpenGL是否打开：

#glxinfo | grep rendering

提示：direct rendering: Yes 表明启动正常

#文件系统与磁盘分区相关问题

##重装Ubuntu如何保留/home分区中的数据

windows系统可以在重装时只格式化C盘，从而保留其他分区的数据。 Ubuntu系统也可以，只要在安装系统时分出一个/home分区。你可以把Ubuntu的“/”分区看为windows的C盘，重装Ubuntu时只格式化“/”分区，不格式化“/home”，这样就可以保留“/home”中的数据

## FAT与NTFS差别

FAT采用32位的文件分配表，能有效地管理2GB以上的硬盘，最多可以支持2TB的磁盘容量。 

在NTFS文件系统中，对于不同配置的硬件，实际的文件大小从4GB到64GB。由于NTFS文件系统的开销较大，使用的最小分区应为50MB。 

NTFS文件系统与FAT文件系统相比最大的特点是安全性，NTFS提供了服务器或工作站所需的安全保障。在NTFS分区上，支持随机访问控制和拥有权，对共享文件夹无论采用FAT还是NTFS文件系统都可以指定权限，以免受到本地访问或远程访问的影响 

就知道这些了，不过文件在网络上不保密性跟NTFS格式也是有关系的！ 



比较大的不同就是簇不一样,簇影响到硬盘的空间分配和操作系统所支持的硬盘分区大小. 

FAT16的簇为16K或32K,不支持大于2GB(win9X下)或4GB(win2K下)的硬盘分区. 

FAT32的簇为4KB至16K,不支持大于32GB的硬盘分区. 

NTFS的簇为0.5K至4K,可以支持到2TB(2048GB)的分区. 

另外,NTFS的分区可以制定安全访问权限和对用户使用空间的配额. 



顺便再介绍一下簇这个概念吧,好像是计算硬盘使用空间的最小单位.簇越小硬盘在储存文件时浪费的空间就越小. 

比如某个文件的大小是20K,如果簇是16K,则储存这个文件就要用2个簇(32K),多出的部分32-20=12K,别的文件也没办法再用了(浪费掉了).而如果簇是4K,则储存这个文件要5个簇(20K),刚刚好,就没有浪费的空间了~ 

其实小文件(例如用windows记事本写几个字存起来),也就有几bytes,一下子就要浪费一个簇的空间,这种问题多了,硬盘当然就严重浪费啦~  



NTFS文件系统 



NTFS是“新技术文件系统”的缩写,是微软为windows NT开发的一种文件系统，它在以前FAT文件系统的基础上作了一定的改进，提高了性能。它是建立在保护文件和目录数据基础上，同时节省存储资源、减少磁盘占用量的一种先进的文件系统。windows XP采用的NTFS文件系统，可以使用户不但可以像win 9X那样方便快捷地操作和管理计算机，同时也可享受到NTFS所带来的系统安全性。 NTFS支持基于NT操作系统的安全性管理，当然天下没有免费的午餐，需要进行这种管理的时候就需要付出额外的空间。一般在运行NT操作系统的时候，最好将硬盘空间的10-15%空出，以保证NT操作系统的正常运行。 



NTFS文件系统有以下几个特点： 



1.NTFS可以支持的分区大小可以达到2TB（2048GB）,而FAT32支持分区的大小最大为32GB。  



2.NTFS采用了更小的簇组，可以更有效率地管理磁盘空间。NTFS文件系统，当分区的大小在2GB以下时，簇的大小都比相应的FAT32簇小，当分区的大小在2GB以上时，簇的大小都为4KB。在FAT32文件系统的情况下，分区大小在2GB～8GB时簇的大小为4KB，分区大小在8GB～16GB时簇的大小为8KB，分区大小在16GB～32GB时簇的大小为16KB。相比较而言，NTFS可以更有效地管理磁盘空间，最大限度地避免了磁盘空间的浪费。  



3.NTFS可以自动地修复磁盘错误而不会显示出错信息。windows XP向NTFS分区中写文件时，会保留文件的一份拷贝，然后检查向磁盘中所写的文件是否与内存中的一致。如果两者不一致，windows就把相应的扇区标为坏扇区而不再使用它（簇重映射），然后用内存中保留的文件拷贝重新向磁盘上写文件。如果在读文件时出现错误，NTFS则返回一个读错误信息，并告知相应的应用程序数据已经丢失。 



4.NTFS有许多安全性能方面的选项，可以在本机上和通过远程的方法保护文件、目录。NTFS还支持加密文件系统（EFS），可以阻止没有授权的用户访问文件。 



5.NTFS文件系统带来的另一个好处是支持文件压缩功能，用户可以选择压缩单个文件或整个文件夹。任何基于windows的应用程序对NTFS分区上的压缩文件进行读写时不需要事先由其他程序进行解压缩，当对文件进行读取时,文件将自动进行解压缩；文件关闭或保存时会自动对文件进行压缩。  



6.磁盘限额功能允许系统管理员管理分配给各个用户的磁盘空间，合法用户只能访问属于自己的文件，windows 2000中的磁盘限额功能是基于用户和卷的。 



FAT32文件系统  



在FAT32文件系统之前，PC机通常使用的文件系统是FAT16。像MS-DOS，winows95等系统采都用了FAT16文件系统。在win 9X系统下，FAT16最大支持的分区大小为2GB。在FAT16情况下簇比较大，存储效率越低，造成了存储空间的浪费。在这种情况下，推出了增强的文件系统FAT32。FAT32使用了32位的空间来表示每个扇区(Sector)配置文件的情形。利用FAT32所能使用的单个分区，最大可达到2TB(2048GB)，而且各种大小的分区所能用到的簇的大小，也是恰如其分，上述两大优点，造就了硬盘使用上更有效率。 



同FAT16相比，FAT32主要具有以下特点： 



1. FAT32可以支持的磁盘大小达到2TB，windows XP下可以支持分区最大为32GB。而FAT16最大只支持4GB的分区。 



2. 由于采用的簇更小，因此FAT32文件系统可以更有效率地进行信息的保存，通常情况下可以提高15%。  



三、结尾 



我们就两个文件系统的区别加以说明：NTFS相对于FAT文件系统的区别在于NTFS不但是一个可恢复的，安全高效的文件系统，NTFS在设计时还考虑到了支持多数据流，西欧字符集名称和坏簇重定向功能。多数据流使得可以在对文件添加新属性或信息时不用重新建立文件系统。西欧字符集可以支持世界上任何一种语言，而我们知道ASCII码只有7位，支持的语言种类也就是英语。最后，坏簇的重定向功能可以使NTFS识别坏簇，这样可以使写入的数据不写入这些族中，保证了数据的安全性。 



如果在windows XP中使用大于32GB的分区，唯一可以选择的是NTFS格式。如果计算机不考虑安全性问题，更注重与win 9X的兼容性，那么FAT32格式是最好的选择。如果注重计算机系统的安全性的话，建议用户采用NTFS格式。如果要使用多个操作系统，需要安装win 9X或其它操作系统，建议用户做成多启动系统，一个分区采用FAT32格式，另外的分区采用NTFS格式，并且将windowds XP安装在NTFS格式分区下，其它操作系统安装在FAT32格式下。   如果你使用下面的命令却没有成功，可以尝试用root权限执行，因为设计文件系统与磁盘分区等命令都有一定等风险，所以可能需要较高等执行权限。

##一些小工具

cfdisk -Ps

cfdisk 也是一款不错的分区工具；在有些发行版中，此工具已经从util-linux包中剔除；cfdisk 简单易用是他的特点。查看磁盘分区的用法   cfdisk   -Ps 磁盘设备名 只有一个硬盘也可以用 cfdisk -Ps



[root@localhost ~]# cfdisk -Ps

Partition Table for /dev/sda



                First         Last

# Type        Sector      Sector       Offset     Length      Filesystem Type         (ID) Flag

-- -------   ----------- -----------    ------   ----------- --------------------      －－－----

1 Primary           0     10233404     63      10233405         Linux (83)             Boot

2 Primary    10233405    14313914      0       4080510       Linux swap / So (82)    None

3 Primary    14313915    24547319      0      10233405         Linux (83)             None

4 Primary    24547320    44082359      0      19535040       Extended (05)           None

5 Logical    24547320     34314839     63       9767520        Linux (83)             None

6 Logical    34314840    44082359     63       9767520         Linux (83)             None

   Logical    44082360    78124094      0      34041735         Free Space            None



[root@localhost ~]# cfdisk -Ps /dev/sda

Partition Table for /dev/sda



               First       Last

# Type       Sector      Sector   Offset    Length   Filesystem Type (ID) Flag

-- ------- ----------- ----------- ------ ----------- -------------------- ----

1 Primary           0    10233404     63    10233405 Linux (83)           Boot

2 Primary    10233405    14313914      0     4080510 Linux swap / So (82) None

3 Primary    14313915    24547319      0    10233405 Linux (83)           None

4 Primary    24547320    44082359      0    19535040 Extended (05)        None

5 Logical    24547320    34314839     63     9767520 Linux (83)           None

6 Logical    34314840    44082359     63     9767520 Linux (83)           None

   Logical    44082360    78124094      0    34041735 Free Space           None

sfdisk -l

[root@localhost ~]# sfdisk -l



Disk /dev/sda: 4863 cylinders, 255 heads, 63 sectors/track

Units = cylinders of 8225280 bytes, blocks of 1024 bytes, counting from 0



   Device Boot Start     End   #cyls    #blocks   Id System

/dev/sda1   *      0+    636     637-   5116671   83 Linux

/dev/sda2        637     890     254    2040255   82 Linux swap / Solaris

/dev/sda3        891    1527     637    5116702+ 83 Linux

/dev/sda4       1528    2743    1216    9767520    5 Extended

/dev/sda5       1528+   2135     608-   4883728+ 83 Linux

/dev/sda6       2136+   2743     608-   4883728+ 83 Linux

Testdisk

教程参考《TestDisk使用教程》

##修改分区的卷标

Fat16/Fat32格式:

#安装 

$ sudo apt-get install mtools 

#新建配置文件 

$ cp /etc/mtools.conf ~/.mtoolsrc

#编辑刚复制的”~/.mtoolsrc”文件,在最後一行加入如下命令行： 

drive i: file="/dev/sda2"    //里面的”/devsda2”应根据实际情况更改为你要改的盘 

#更改命令提示符路径到”i:”盘： 

$ mcd i: 

#查看”i:”当前的卷标 

$ sudo mlabel -s i:

#更改”i:”盘原始卷标为你喜欢的新卷标名： 

$ sudo mlabel i: newLabelName

NTFS格式 

#安装 

$ sudo apt-get install ntfsprogs

注：安装包已下 

#修改 

$ sudo ntfslabel /dev/sda1 newLabelName //里面的"/dev/sda1"应根据实际情况修改



ext2/ext3格式

使用内置命令 

$ sudo e2label /dev/sda1 newLabelName

#权限账户设置问题

##如何启用 Ubuntu 中的 root 帐号

和其它发行版本的Linux不同，Ubuntu Linux有一个与众不同的特点，那就是初次使用时，你无法作为root来登录系统，为什么会这样？这就要从系统的安装说起。对于其他Linux系统来说，一般在安装过程就设定root密码，这样用户就能用它登录root帐户或使用su命令转换到超级用户身份。与之相反，Ubuntu默认安装时，并没有给root用户设置口令，也没有启用root帐户。问题是要想作为root用户来运行命令该怎么办呢？没关系，我们可以使用sudo命令达此目的。sudo是linux下常用的允许普通用户使用超级用户权限的工具，该命令为管理员提供了一种细颗粒度的访问控制方法，通过它人们既可以作为超级用户又可以作为其它类型的用户来访问系统。这样做的好处是，管理员能够在不告诉用户root密码的前提下，授予他们某些特定类型的超级用户权限，这正是许多系统管理员所梦寐以求的。

这里有必要说先简单一下sudo和su命令的区别：

su命令是在不退出当前用户的情况下切换用户的工具，通过su可以在用户之间切换，如果超级权限用户root向普通或虚拟用户切换不需要密码，而普通用户切换到其它任何用户都需要密码验证。

sudo是Unix/Linux平台上的一个非常有用的工具，它允许系统管理员分配给普通用户一些合理的“权利”，让他们执行一些只有超级用户或其他特许用户才能完成的任务这样一来，就不仅减少了root用户的登陆次数和管理时间，也提高了系统安全性。sudo设计者的宗旨是：给用户尽可能少的权限但仍允许完成他们的工作。我们可以简单的理解成：su获得稳定的超级用户（或其他用户权限），sudo获得暂时性的限制了的超级用户权限，一段时间之后会失效。

好，下面讲一下具体的设置方法：方法一：

1.为root设置一个root密码：$ sudo passwd root

之后会提示要输入root用户的密码，连续输入root密码

2.使用：$ su,并按照提示输入root密码，就可以在终端中切换成超级管理员用户身份了！

## Linux用户添加sudoer

使用sudo可以在以非root用户登录时临时获得root权限，并执行需要的命令。可以使用sudo的用户可以叫做sudoer。

添加sudoer的方法（假设您已经安装sudo）：执行

# visudo

或

# sudoedit

提示：

有些发行版的sudo提供了sudoedit，有的则提供了visudo，功能上基本是一样的。你也可以使用其他编辑器如vi进行编辑/etc/sudoers，但由于文件是只读的，请强制保存（如w!）或去除只读属性再保存。查找

root ALL=(ALL) ALL

在下面加入

%adm ALL=(ALL) ALL

如果sudo时不想输入密码，可以把上句改成：

%adm ALL=(ALL) NOPASSWD: ALL

保存文件，然后执行

#gpasswd -a 用户名 adm

然后这个用户就可以用sudo了。 

## linux无root权限安装软件

在有些公司是不会给开发人员root权限的，但是开发人员有时候也需要装一些软件。没有root权限是否可以成功安装软件呢？答案是yes。本文以安装nginx为例说明下如何操作。

没有root权限时往往也就没有权限操作一些系统目录，例如bin，usr等。所以在安装时需要配置将安装文件装在当前用户有权限操作的目录。

安装nginx首先要下载安装文件，具体的安装步骤如下：

1. 下载文件之后需要解压缩文件：

tar-zvxf nginx-1.2.3.tar.gz

2. 创建安装文件目录，例如：

cd ~

mkdir nginx

3. 转到解压后安装文件的存放目录，然后配置

cd xxx

./configure—prefix=/xxx/yy/nginx

4. 编译

make

5. 安装

make install

正常情况下这样就成功安装了。

和有root权限安装的区别在于./configure 需要指定安装文件的目录。



#卸载LNMP

killall nginx *//终止nginx进程

/etc/init.d/mysql stop *//关闭mysql

killall mysqld *//终止mysql进程

/usr/local/php/sbin/php-fpm stop *//关闭php

killall php-cgi *//终止php-cgi进程

rm -rf /usr/local/php *//删除php文件

rm -rf /usr/local/nginx *//删除nginx文件

rm -rf /usr/local/mysql *//删除mysql文件

rm -rf /usr/local/zend *//删除zend文件

rm /etc/my.cnf *//删除配置文件

rm /etc/init.d/mysql *//删除mysql文件

rm /root/vhost.sh *//删除配置虚拟主机脚本

rm /root/lnmp *//删除lnmp文件夹

或者安装文件中执行.unistall.sh

# Could not get lock /var/lib/apt/lists/lock - open

Could not get lock /var/lib/apt/lists/lock - open(11:Resource temporarily unavailable)

ubuntukilllist终端工作

出现这个问题的原因可能是有另外一个程序正在运行，导致资源被锁不可用。而导致资源被锁的原因，可能是上次安装时没正常完成，而导致出现此状况。

解决方法：输入以下命令

sudo rm /var/cache/apt/archives/lock

sudo rm /var/lib/dpkg/lock

之后再安装想装的包，即可解决

 

 

今天玩ubuntu的时候，在弄更新源的时候，突然出现以下错误：

[1]+ Stopped                 sudo apt-get update

haiquan@haiquan-desktop:~$ sudo apt-get update

E: Could not get lock /var/lib/apt/lists/lock - open (11: Resource temporarily unavailable)

E: Unable to lock the list directory

开始以为是权限不够，就是用 sudo apt-get update,发现还是报错，问题没有解决。于是上网搜索了一下，答案如下：

问题应该是之前那个更新被强制取消的问题，进程仍然还在。用这个命令查看一下：

ps -e | grep apt

显示结果如下：

6362 ? 00:00:00 apt

6934 ? 00:00:00 apt-get

7368 ? 00:00:00 synaptic

然后就执行

sudo killall apt

sudo killall apt-get

sudo killall synaptic

再次在终端里查看ps -e | grep apt 没有任何结果了

继续执行sudo apt-get update

 

原因：刚装好的Ubantu系统，内部缺少很多软件源，这时，系统会自动启动软件源更新进程“apt-get”，并且它会一直存活。由于它在运行时，会占用软件源更新时的系统锁（以下称“系统更新锁”，此锁文件在“/var/lib/apt/lists/”目录下），而当有新的apt-get进程生成时，就会因为得不到系统更新锁而出现"E: 无法获得锁 /var/lib/apt/lists/lock - open (11: Resource temporarily unavailable)"错误提示！因此，我们只要将原先的apt-get进程杀死，从新激活新的apt-get进程，就可以让新立德软件管理器正常工作了！



这时，你可以按一下步骤来解决：

1、输入以下命令：“ps -aux  > temp.txt”.敲回车确定。这时会有“warning”出现，但不予理会。

2、输入以下命令：“grep -n apt-get temp.txt”键入回车确定。而后从命令输出中找到 apt-get 进程的PID。

3、输入以下命令：“sudo kill <PID>”。

4、完成。



or



如果提示错误:E: Could not get lock /var/lib/dpkg/lock - open (11 Resource temporarily unavailable) 

输入

sudo rm /var/lib/apt/lists/lock

即可





# Ubuntu Linux下如何用源码文件安装软件

　　在附带了丰富的软件，这些软件一般使用图形化的自动方式（“添加／删除”或“新立得”）即可轻松安装，但是对于那些刚刚问世的新软件，Ubuntu的源中还未收录其中，这时我们就需要用到一种更通用的安装方式：通过手工方式从源文件来安装这些软件。下面就介绍这种手工安装方式的详细步骤。　　

　　一、 安装编译程序

　　因为要编译源代码，所以第一步就是安装编译和构建之类的程序。如果你已经安装过了，可以跳过此步。在Ubuntu系统中非常简单，只要执行下面命令就行了：

　　$ sudo apt-get install build-essential

　　该命令执行后，从源文件安装软件所需的工具，如gcc、make、g++及其他所需软件就安装好了。

　　二、下载并编译软件的源代码

　　当我们下载源文件时，一定要弄清该软件所依赖的库文件和其他程序，并且首先将它们装好。这些信息，通常都能在该开源项目的主页上查找到。做好这些准备工作后，我们就可以进行下面的工作了。因为，软件的源代码通常以压缩文件形式发布，所以需要将其解压到指定目录。命令如下所示：

　　OwnLinux@ubuntu:~$ tar xvzf

　　program.tar.gz

　　OwnLinux@ubuntu:~$ cd

　　program/

　　在Linux下从源文件安装程序时，有一个通用模式，即配置（./configure）–＞ 编译（make） –＞ 安装（sudo make install）。但是，此前你最好还是阅读源文件中附带的安装说明，因为对于每个程序，其开发者的指示才是最具权威性的。程序开发者通常将安装说明存放在名为INSTALL或README。到哪里找这些文件呢？它们在项目主页或源代码主目录中都能找到。

　　1.配置

　　构建应用的第一步就是执行configure脚本,该脚本位于程序源文件的主目录下：

　　OwnLinux@ubuntu:~/program$ ./configure

　　该脚本将扫描系统，以确保程序所需的所有库文件业已存在，并做好文件路径及其他所需的设置工作。如果程序所需的库文件不完全，该配置脚本就会退出，并告诉您还需要哪些库文件或者是哪些版本太旧需要更新。如果遇到这种情况，仅弄到含有该库文件的软件包还是不够的，同时还要找到具有该库文件所有头文件的开发包，在，这样的包一般以-dev作为文件名的结尾。安装好所有需要的库文件后，重新运行配置脚本，直到没有错误提示为止，这说明需要的库文件已经全部安装妥当了即满足了依赖关系。

　　2.编译

　　当配置脚本成功退出后，接下来要做的就是编译代码了。具体操作为在源文件的主目录中运行make命令：

　　OwnLinux@ubuntu:~/program$ make

　　这时，您会看到一串编译输出数据迅速从屏幕上滚过，如果正常的话，系统会返回的提示符状态。然而，如果编译过程中出现错误的话，排错的过程可就不像配置步骤那么简单了。因为，这通常要涉及到源代码的调试，可能源代码有语法错误，或其他错误等等。怎么办？如果您是编程高手，那就自己调试吧！否则，检查该软件的邮件列表等支持渠道，看看是不是已知的bug，如果是就看看别人是怎么解决的，不是就提交一份bug报告吧，也许不久就会有解决办法。

　　3.安装

　　当软件成功编译后，最后一步就是将它们安装到系统上。大部分程序的makefile文件中都会有一个用于安装的函数。需要注意的是，大多时候我们必须作为root用户来安装程序，这样程序就把文件安装到/usr或其他只有超级用户才有写权限的目录中。依旧是在源文件的主目录下，执行如下命令：

　　OwnLinux@ubuntu:~/program$ sudo make install

　　好了，这样程序就会安装到您的计算机上了。另外，当您不再使用该程序时，可以使用软件所带的卸载功能，一般程序都会具备此功能。切换至源文件的主目录下，执行以下命令即可：

　　OwnLinux@ubuntu:~/program$ sudo make uninstall

　　多数情况下，利用上面介绍的方法安装的程序，都位于/usr/local下面。若想让安装的程序文件与Ubuntu巡视的文件系统隔离开的话，可以为命令添加项，如下所示：

　　OwnLinux@ubuntu:~/program$ ./configure –prefix=/opt

　　尽管这样做一般都是有效的，但是也有例外，有些程序根本不理会项；有些程序如含有内核模块的程序，会把它们自己全部放进您的文件系统。

　　上面介绍的手工安装软件的方法虽然是针对Ubuntu环境来介绍的，但是各种Linux系统下的从源文件安装应用的方法基本上都大同小异。

#解压缩 压缩命令

tar

-c: 建立压缩档案

-x：解压

-t：查看内容

-r：向压缩归档文件末尾追加文件

-u：更新原压缩包中的文件



这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。



-z：有gzip属性的

-j：有bz2属性的

-Z：有compress属性的

-v：显示所有过程

-O：将文件解开到标准输出



下面的参数-f是必须的



-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。



# tar -cf all.tar *.jpg 

这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。 



# tar -rf all.tar *.gif 

这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。 



# tar -uf all.tar logo.gif 

这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。 



# tar -tf all.tar 

这条命令是列出all.tar包中所有文件，-t是列出文件的意思 



# tar -xf all.tar 

这条命令是解出all.tar包中所有文件，-x是解开的意思 



压缩

tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg

tar –czf jpg.tar.gz *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz

tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

tar –cZf jpg.tar.Z *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux

zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux



解压

tar –xvf file.tar //解压 tar包

tar -xzvf file.tar.gz //解压tar.gz

tar -xjvf file.tar.bz2   //解压 tar.bz2

tar –xZvf file.tar.Z   //解压tar.Z

unrar e file.rar //解压rar

unzip file.zip //解压zip



总结

1、*.tar 用 tar –xvf 解压

2、*.gz 用 gzip -d或者gunzip 解压

3、*.tar.gz和*.tgz 用 tar –xzf 解压

4、*.bz2 用 bzip2 -d或者用bunzip2 解压

5、*.tar.bz2用tar –xjf 解压

6、*.Z 用 uncompress 解压

7、*.tar.Z 用tar –xZf 解压

8、*.rar 用 unrar e解压

9、*.zip 用 unzip 解压

# Virtual Box相关

注：增强包已下载存在Documents

通过设备——分配光驱即可分配

##访问USB子系统失败

解决ubuntu下virtualbox访问usb子系统失败

http://blog.coltcn.com/2012/03/13/virtualbox-error-failed-to-access-usb-subsystem/

## ubuntu用户不在sudoers文件中问题

http://blog.csdn.net/killzero/article/details/10298845

##安装CentOS后安装增强功能

1.启动CentOS，以root身份登录，进入桌面环境。

2.执行如下命令：

#yum upadate

#yum install kernel-devel 　

#yum install gcc

3.重启系统

4.安装增强功能

5.重新启动

## Cannot register the hard disk错误解决办法

virtualbox中加载已有的虚拟硬盘时出现Cannot register the hard disk错误，描述类似下面的。



ERROR: Cannot register the hard disk '/mnt/ee/winxp/xp.vdi' with UUID {395ae4ae-8bf9-42e5-b82a-61af9f95fbf0} because a hard disk '/mnt/ee/winxp/xp.vdi' with UUID {395ae4ae-8bf9-42e5-b82a-61af9f95fbf0} already exists in the media registry ('/home/pzye/.VirtualBox/VirtualBox.xml')

Details: code NS_ERROR_INVALID_ARG (0x80070057), component VirtualBox, interface IVirtualBox, callee nsISupports

Context: "OpenHardDisk(Bstr(szFilenameAbs), AccessMode_ReadWrite, srcDisk.asOutParam())" at line 603 of file VBoxManageDisk.cpp



解决方法如下：

关闭virtualbox，重新启动它，它会检测虚拟硬盘，可能会检测出来一些虚拟硬盘，请将其删除，然后就不会出现这个问题了。

## VirtualBox虚拟机网络连接设置

VirtualBox的提供了四种网络接入模式，它们分别是：

1、NAT    网络地址转换模式(NAT,Network Address Translation)

2、Bridged Adapter    桥接模式

3、Internal    内部网络模式

4、Host-only Adapter  主机模式

下面我们分别对这四种网络模式进行分析解释：



第一种 NAT模式

解释：

NAT模式是最简单的实现虚拟机上网的方式，你可以这样理解：Vhost访问网络的所有数据都是由主机提供的，vhost并不真实存在于网络中，主机与网络中的任何机器都不能查看和访问到Vhost的存在。

虚拟机与主机关系：

只能单向访问，虚拟机可以通过网络访问到主机，主机无法通过网络访问到虚拟机。

虚拟机与网络中其他主机的关系：

只能单向访问，虚拟机可以访问到网络中其他主机，其他主机不能通过网络访问到虚拟机。

虚拟机与虚拟机之间的关系：

相互不能访问，虚拟机与虚拟机各自完全独立，相互间无法通过网络访问彼此。

IP:10.0.2.15

网关：10.0.2.2

DNS：10.0.2.3

一台虚拟机的多个网卡可以被设定使用 NAT， 第一个网卡连接了到专用网 10.0.2.0，第二个网卡连接到专用网络 10.0.3.0，等等。默认得到的客户端ip（IP Address）是10.0.2.15，网关（Gateway）是10.0.2.2，域名服务器（DNS）是10.0.2.3，可以手动参考这个进行修改。

NAT方案优缺点：

笔记本已插网线时： 虚拟机可以访问主机，虚拟机可以访问互联网，在做了端口映射后（最后有说明），主机可以访问虚拟机上的服务（如数据库）。

笔记本没插网线时： 主机的“本地连接”有红叉的，虚拟机可以访问主机，虚拟机不可以访问互联网，在做了端口映射后，主机可以访问虚拟机上的服务（如数据库）。



第二种 Bridged Adapter模式

解释：

网桥模式是我最喜欢的用的一种模式，同时，模拟度也是相当完美。你可以这样理解，它是通过主机网卡，架设了一条桥，直接连入到网络中了。因此，它使得虚拟机能被分配到一个网络中独立的IP，所有网络功能完全和在网络中的真实机器一样。

虚拟机与主机关系：

可以相互访问，因为虚拟机在真实网络段中有独立IP，主机与虚拟机处于同一网络段中，彼此可以通过各自IP相互访问。

虚拟机于网络中其他主机关系：

可以相互访问，同样因为虚拟机在真实网络段中有独立IP，虚拟机与所有网络其他主机处于同一网络段中，彼此可以通过各自IP相互访问。

虚拟机于虚拟机关系：

可以相互访问，原因同上。

IP：一般是DHCP分配的，与主机的“本地连接”的IP 是同一网段的。虚拟机就能与主机互相通信。

笔记本已插网线时：（若网络中有DHCP服务器）主机与虚拟机会通过DHCP分别得到一个IP，这两个IP在同一网段。 主机与虚拟机可以ping通，虚拟机可以上互联网。

笔记本没插网线时：主机与虚拟机不能通信。主机的“本地连接”有红叉，就不能手工指定IP。虚拟机也不能通过DHCP得到IP地址，手工指定IP后，也无法与主机通信，因为主机无IP。

这时主机的VirtualBox Host-Only Network 网卡是有ip的，192.168.56.1。虚拟机就算手工指定了IP 192.168.56.*，也ping不能主机。



第三种 Internal模式

解释：

内网模式，顾名思义就是内部网络模式，虚拟机与外网完全断开，只实现虚拟机与虚拟机之间的内部网络模式。

虚拟机与主机关系：

不能相互访问，彼此不属于同一个网络，无法相互访问。

虚拟机与网络中其他主机关系：

不能相互访问，理由同上。

虚拟机与虚拟机关系：

可以相互访问，前提是在设置网络时，两台虚拟机设置同一网络名称。如上配置图中，名称为intnet。

IP: VirtualBox的DHCP服务器会为它分配IP ，一般得到的是192.168.56.101，因为是从101起分的，也可手工指定192.168.56.*。

笔记本已插网线时：虚拟机可以与主机的VirtualBox Host-Only Network 网卡通信

这种方案不受主机本地连接（网卡）是否有红叉的影响。



第四种 Host-only Adapter模式

解释：

主机模式，这是一种比较复杂的模式，需要有比较扎实的网络基础知识才能玩转。可以说前面几种模式所实现的功能，在这种模式下，通过虚拟机及网卡的设置都可以被实现。

我们可以理解为Vbox在主机中模拟出一张专供虚拟机使用的网卡，所有虚拟机都是连接到该网卡上的，我们可以通过设置这张网卡来实现上网及其他很多功能，比如（网卡共享、网卡桥接等）。

虚拟机与主机关系

默认不能相互访问，双方不属于同一IP段，host-only网卡默认IP段为192.168.56.X 子网掩码为255.255.255.0，后面的虚拟机被分配到的也都是这个网段。通过网卡共享、网卡桥接等，可以实现虚拟机于主机相互访问。

虚拟机与网络主机关系

默认不能相互访问，原因同上，通过设置，可以实现相互访问。

虚拟机与虚拟机关系

默认可以相互访问，都是同处于一个网段。

虚拟机访问主机 用的是主机的VirtualBox Host-Only Network网卡的IP：192.168.56.1  ，不管主机“本地连接”有无红叉，永远通。

主机访问虚拟机，用是的虚拟机的网卡3的IP： 192.168.56.101  ，不管主机“本地连接”有无红叉，永远通。

虚拟机访问互联网，用的是自己的网卡2， 这时主机要能通过“本地连接”有线上网，（无线网卡不行）



通过对以上几种网络模式的了解，我们就可以灵活运用，模拟组建出我们所想要的任何一种网络环境了。

比如我想模拟出来一个一台主机，监控一个局域网上网情况的网络环境。

首先我开启了两台虚拟机vhost1与vhost2，当然如果硬件允许，我同样可以再增加vhost3、vhost4…

所有的vhost我都设置成internat内网模式，网络名称为intnal，网关为192.168.56.100，意思就是通过 192.168.56.100网卡上网。其中有一台vhost1我设置为双网卡，一张为内网模式（192.168.56.100），一张为网桥模式（192.168.1.101）。两张网卡设置双网卡共享上网

虚拟机之间为局域网，其中有一台虚拟机vhost1通过与外网相连，所有局域网中的虚拟机又通过vhost1来实现上外网。这样vhost1就可以监控整个虚拟机局域网上网情况了。



NAT 设置端口映射

http://huzhangsheng.blog.163.com/blog/static/34787784200802801435931/

你可以设置一个虚拟机的服务（比如 WEB  服务），通过使用命令行工具 VboxManage 代理。你需要知道虚拟机的服务使用哪个端口，然后决定在主机上使用哪个端口（通常但不总是想要使虚拟机和主机使用同一个端口）。在主机上提供一个服务需要使用一个端口，你能使用在主机上没有准备用来提供服务的任何端口。一个怎样设置新的 NAT 例子，在虚拟机上连接到一个 ssh 服务器，需要下面的三个命令：

VBoxManage setextradata 'Linux Guest' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/guestssh/Protocol' TCP

VBoxManage setextradata 'Linux Guest' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/guestssh/GuestPort' 22

VBoxManage setextradata 'Linux Guest' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/guestssh/HostPort' 2222

说明：VboxManage 是一个命令行程序，请查询你的 VirtualBox 安装目录，'Linux Guest' 是虚拟主机名。guestssh 是一个自定义的名称，你可以任意设置，通过上面的三个命令，把虚拟机的 22 端口 转发到主机的 2222 端口。

又比如，我在虚拟机 debian 上安装了 apache2 服务器，使用 80 端口，映射到主机的 80 端口。使用下面的命令。

'C:\Program Files\innotek VirtualBox\VBoxManage.exe' setextradata 'debian' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/huzhangsheng/Protocol' TCP

'C:\Program Files\innotek VirtualBox\VBoxManage.exe' setextradata 'debian' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/huzhangsheng/GuestPort' 80

'C:\Program Files\innotek VirtualBox\VBoxManage.exe' setextradata 'debian' 'VBoxInternal/Devices/pcnet/0/LUN#0/Config/huzhangsheng/HostPort' 80

注意：要使设置生效，请关掉 VirtualBox 再运行虚拟机，我把 VirtualBox 安装在 winxp 上，在虚拟机中安装 debian 4.02r ，虚拟机名是 debian ，并安装了 apache2 php5 mysql-server ，在主机上用IE浏览 http://localhost，成功转发到虚拟机 debian 的 apache2 web 服务器上

## virtualbox命令行共享CentOS目录

1. 安装virtualbox增强工具

2. 设置共享文件夹

完成后点击"设备(Devices)" -> 共享文件夹(Shared Folders)菜单，添加一个共享文件夹，选项固定和临时是指该文件夹是否是持久的。共享名可以随意取，如"yongfu"，尽量使用英文名称，不要有空格。

3. 挂载共享文件夹

在命令行终端下输入：

mkdir /mnt/yongfu

mount -t vboxsf yongfu /mnt/yongfu

其中"yongfu"是之前创建的共享文件夹的名字。现在虚拟机和主机可以互传文件了。

如不想每次都手动挂载，可以在/etc/fstab中添加一项

yongfu /mnt/yongfu vboxsf rw,gid=100,uid=1000,auto 0 0

这样就能够自动挂载了。

4. 卸载的话使用下面的命令：

umount -f /mnt/yongfu

linux连接投影机



# update-Alternatives学习笔记

Linux 发展到今天，可用的软件已经非常多了。这样自然会有一些软件的功能大致上相同。例如，同样是编辑器，就有 nvi、vim、emacs、nano，而且我说的这些还只是一部分。大多数情况下，这样的功能相似的软件都是同时安装在系统里的，可以用它们的名称来执行。例如，要执行 vim，只要在终端下输入 vim 并按回车就可以了。不过，有些情况下我们需要用一个相对固定的命令调用这些程序中的一个。例如，当我们写一个脚本程序时，只要写下 editor，而不希望要为“编辑器是哪个”而操心。Debian 提供了一种机制来解决这个问题，而 update-Alternatives 就是用来实现这种机制的。



1)首先要介绍的参数是 --display。它使我们可以看到一个命令的所有可选命令。执行：

update-Alternatives --display editor

可以看到我的机器上的所有可以用来被 editor 链接的命令。



2)--config。这个选项使我们可以选择其中一个命令程序来作为editor,执行：

update-Alternatives --config editor



首先，update-Alternatives 在一般情况下是由postinst 和 prerm 这样的安装脚本自动调用的，所以一个 Alternative 的状态有两种：自动和手动。每个 Alternative 的初始状态都是自动。如果系统发现管理员手动修改了一个 Alternative，它的状态就从自动变成了手动，这样安装脚本就不会更新它了。如果你希望将一个 Alternative 变回自动，只要执行代码:

update-Alternatives --auto editor



general name -- 这是指一系列功能相似的程序的“公用”名字（包括绝对路径），比如 /usr/bin/editor。

link -- 这是指一个 Alternative 在 /etc/Alternative 中的名字，比如 editor。

Alternative -- 顾名思义，这是指一个可选的程序所在的路径（包括绝对路径），比如 /usr/bin/vim。



-auto，--display 和 --config 跟的都是 link。我们要说的第三个概念是优先级。这个比较简单，当然优先级越高的程序越好啦。最后一个概念是主和从的 Alternative。想想看，你将 /usr/bin/editor 链接到了 vim，可是当你执行 man editor 时看到的却是 emacs 的 manpage，你会做何感想呢？这就引出了主和从 Alternative 的概念了：当更新主的 Alternative 时，从的 Alternative 也会被更新。



另外两个选项：第一个是 --install。它的格式是：

update-Alternatives --install gen link Alt pri [--slave sgen slink sAlt] ...



gen，link，Alt，pri 分别是我们上面说过的。如果需要从的 Alternative，你可以用--slave 加在后面。如果你在向一个已经存在的 Alternative 组中添加新的 Alternatives，该命令会把这些 Alternatives 加入到这个已经存在的 Alternative 组的列表中，并用新的可选命令作为新的命令；否则，将会建立一个新的自动的 Alternative组。

呜呼！我加入了一个错误的 Alternative。我不想要这个 Alternative 了。在这种情况

下，可以执行下面的命令：

update-Alternatives --remove name path

# linux系统下无法访问电脑硬盘

```
    Error mounting /dev/sda6 at /media/qiaokaiming/20F47472F4744BD2: Command-line 'mount -t "ntfs" -o "uhelper=udisks2,nodev,nosuid,uid=1000,gid=1000,dmask=0077,fmask=0177" "/dev/sda6" "/media/qiaokaiming/20F47472F4744BD2"' exited with non-zero exit status 14: The disk contains an unclean file system (0, 0).
    Metadata kept in windows cache, refused to mount.
    Failed to mount '/dev/sda6': Operation not permitted
    The NTFS partition is in an unsafe state. Please resume and shutdown
    windows fully (no hibernation or fast restarting), or mount the volume
    read-only with the 'ro' mount option.
```

那个提示里有：Please resume and shutdown windows fully (no hibernation or fast restarting)。进win8把”快速启动“关掉就好了。控制面板》所有控制面板选项》电源选项》系统设置》关闭“启用快速启动”

# /etc/profile和/etc/environment(Ubuntu)

先将export LANG=zh_CN加入/etc/profile ,退出系统重新登录，登录提示显示英文。将/etc/profile 中的export LANG=zh_CN删除，将LNAG=zh_CN加入/etc/environment，退出系统重新登录，登录提示显示中文。

原因是系统是先执行/etc/environment，后执行/etc/profile。/etc/environment是设置整个系统的环境，而/etc/profile是设置所有用户的环境，前者与登录用户无关，后者与登录用户有关。系统应用程序的执行与用户环境可以是无关的，但与系统环境是相关的，所以当你登录时，你看到的提示信息，象日期、时间信息的显示格式与系统环境的LANG是相关的，缺省LANG=en_US，如果系统环境LANG=zh_CN，则提示信息是中文的，否则是英文的。登陆系统时shell读取的顺序应该是 ：

/etc/enviroment->/etc/profile-->$HOME/.profile-->$HOME/.env(如果存在)

如果同一个变量在用户环境(/etc/profile)和系统环境(/etc/environment)有不同的值那应该是以用户环境为准了。修改environment 之后，执行 source /etc/environment 可以立即生效。

# Configure参数解释说明

Linux环境下的软件安装，并不是一件容易的事情；如果通过源代码编译后在安装，当然事情就更为复杂一些；现在安装各种软件的教程都非常普遍；但万变不离其中，对基础知识的扎实掌握，安装各种软件的问题就迎刃而解了。Configure脚本配置工具就是基础之一，它是autoconf的工具的基本应用。与一些技巧相比，Configure显得基础一些，当然使用和学习起来就显得枯燥乏味一些，当然要成为高手，对基础的熟悉不能忽略哦。为此我转载了一篇关于Configure选项配置的详细介绍。供大家参考

'configure'脚本有大量的命令行选项。对不同的软件包来说，这些选项可能会有变化，但是许多基本的选项是不会改变的。带上'--help'选项执行'configure'脚本可以看到可用的所有选项。尽管许多选项是很少用到的，但是当你为了特殊的需求而configure一个包时，知道他们的存在是很有益处的。下面对每一个选项进行简略的介绍：

--cache-file=FILE 'configure'会在你的系统上测试存在的特性(或者bug!)。为了加速随后进行的配置，测试的结果会存储在一个cache file里。当configure一个每个子树里都有'configure'脚本的复杂的源码树时，一个很好的cache file的存在会有很大帮助。
--help 输出帮助信息。即使是有经验的用户也偶尔需要使用使用'--help'选项，因为一个复杂的项目会包含附加的选项。例如，GCC包里的'configure'脚本就包含了允许你控制是否生成和在GCC中使用GNU汇编器的选项。
--no-create 'configure'中的一个主要函数会制作输出文件。此选项阻止'configure'生成这个文件。你可以认为这是一种演习(dry run)，尽管缓存(cache)仍然被改写了。
--quiet

--silent

当'configure'进行他的测试时，会输出简要的信息来告诉用户正在作什么。这样作是因为'configure'可能会比较慢，没有这种输出的话用户将会被扔在一旁疑惑正在发生什么，使用这两个选项中的任何一个都会把你扔到一旁。(译注：这两句话比较有意思，原文是这样的：If there was no such output, the user would be left wondering what is happening. By using this option, you too can be left wondering!)



--version

打印用来产生'configure'脚本的Autoconf的版本号。



--prefix=PEWFIX

'--prefix'是最常用的选项。制作出的'Makefile'会查看随此选项传递的参数，当一个包在安装时可以彻底的重新安置他的结构独立部分。举一个例子，当安装一个包，例如说Emacs，下面的命令将会使Emacs Lisp file被安装到"/opt/gnu/share"：

$ ./configure --prefix=/opt/gnu



--exec-prefix=EPREFIX

与'--prefix'选项类似，但是他是用来设置结构倚赖的文件的安装位置，编译好的'emacs'二进制文件就是这样一个问件。如果没有设置这个选项的话，默认使用的选项值将被设为和'--prefix'选项值一样。



--bindir=DIR

指定二进制文件的安装位置，这里的二进制文件定义为可以被用户直接执行的程序。



--sbindir=DIR

指定超级二进制文件的安装位置。这是一些通常只能由超级用户执行的程序。



--libexecdir=DIR

指定可执行支持文件的安装位置。与二进制文件相反，这些文件从来不直接由用户执行，但是可以被上面提到的二进制文件所执行。



--datadir=DIR

指定通用数据文件的安装位置。



--sysconfdir=DIR

指定在单个机器上使用的只读数据的安装位置。





--sharedstatedir=DIR



指定可以在多个机器上共享的可写数据的安装位置。





--localstatedir=DIR



指定只能单机使用的可写数据的安装位置。



--libdir=DIR



指定库文件的安装位置。





--includedir=DIR



指定C头文件的安装位置。其他语言如C++的头文件也可以使用此选项。





--oldincludedir=DIR



指定为除GCC外编译器安装的C头文件的安装位置。





--infodir=DIR



指定Info格式文档的安装位置.Info是被GNU工程所使用的文档格式。





--mandir=DIR



指定手册页的安装位置。





--srcdir=DIR



这个选项对安装没有作用，他会告诉'configure'源码的位置。一般来说不用指定此选项，因为'configure'脚本一般和源码文件在同一个目录下。





--program-prefix=PREFIX



指定将被加到所安装程序的名字上的前缀。例如，使用'--program-prefix=g'来configure一个名为'tar'的程序将会使安装的程序被命名为'gtar'。当和其他的安装选项一起使用时，这个选项只有当他被`Makefile.in'文件使用时才会工作。





--program-suffix=SUFFIX



指定将被加到所安装程序的名字上的后缀。





--program-transform-name=PROGRAM



这里的PROGRAM是一个sed脚本。当一个程序被安装时，他的名字将经过`sed -e PROGRAM'来产生安装的名字。





--build=BUILD



指定软件包安装的系统平台。如果没有指定，默认值将是'--host'选项的值。





--host=HOST



指定软件运行的系统平台。如果没有指定。将会运行`config.guess'来检测。





--target=GARGET



指定软件面向(target to)的系统平台。这主要在程序语言工具如编译器和汇编器上下文中起作用。如果没有指定，默认将使用'--host'选项的值。





--disable-FEATURE



一些软件包可以选择这个选项来提供为大型选项的编译时配置，例如使用Kerberos认证系统或者一个实验性的编译器最优配置。如果默认是提供这些特性，可以使用'--disable-FEATURE'来禁用它，这里'FEATURE'是特性的名字，例如：



$ ./configure --disable-gui





-enable-FEATURE[=ARG]



相反的，一些软件包可能提供了一些默认被禁止的特性,可以使用'--enable-FEATURE'来起用它。这里'FEATURE'是特性的名字。一个特性可能会接受一个可选的参数。例如：



$ ./configure --enable-buffers=128



`--enable-FEATURE=no'与上面提到的'--disable-FEATURE'是同义的。





--with-PACKAGE[=ARG]



在自由软件社区里，有使用已有软件包和库的优秀传统。当用'configure'来配置一个源码树时，可以提供其他已经安装的软件包的信息。例如，倚赖于Tcl和Tk的BLT器件工具包。要配置BLT，可能需要给'configure'提供一些关于我们把Tcl和Tk装的何处的信息：



$ ./configure --with-tcl=/usr/local --with-tk=/usr/local



'--with-PACKAGE=no'与下面将提到的'--without-PACKAGE'是同义的。





--without-PACKAGE



有时候你可能不想让你的软件包与系统已有的软件包交互。例如，你可能不想让你的新编译器使用GNU ld。通过使用这个选项可以做到这一点：



$ ./configure --without-gnu-ld





--x-includes=DIR



这个选项是'--with-PACKAGE'选项的一个特例。在Autoconf最初被开发出来时，流行使用'configure'来作为Imake的一个变通方法来制作运行于X的软件。'--x-includes'选项提供了向'configure'脚本指明包含X11头文件的目录的方法。





--x-libraries=DIR



类似的，'--x-libraries'选项提供了向'configure'脚本指明包含X11库的目录的方法。





在源码树中运行'configure'是不必要的同时也是不好的。一个由'configure'产生的良好的'Makefile'可以构筑源码属于另一棵树的软件包。在一个独立于源码的树中构筑派生的文件的好处是很明显的：派生的文件，如目标文件，会凌乱的散布于源码树。这也使在另一个不同的系统或用不同的配置选项构筑同样的目标文件非常困难。建议使用三棵树：一棵源码树(source tree)，一棵构筑树(build tree)，一棵安装树(install tree)。这里有一个很接近的例子，是使用这种方法来构筑GNU malloc包：



$ gtar zxf mmalloc-1.0.tar.gz



$ mkdir build && cd build



$ ../mmalloc-1.0/configure



creating cache ./config.cache



checking for gcc... gcc



checking whether the C compiler (gcc ) works... yes



checking whether the C compiler (gcc ) is a cross-compiler... no



checking whether we are using GNU C... yes



checking whether gcc accepts -g... yes



checking for a BSD compatible install... /usr/bin/install -c



checking host system type... i586-pc-linux-gnu



checking build system type... i586-pc-linux-gnu



checking for ar... ar



checking for ranlib... ranlib



checking how to run the C preprocessor... gcc -E



checking for unistd.h... yes



checking for getpagesize... yes



checking for working mmap... yes



checking for limits.h... yes



checking for stddef.h... yes



updating cache ../config.cache



creating ./config.status



这样这棵构筑树就被配置了，下面可以继续构筑和安装这个包到默认的位置'/usr/local'：



$ make all && make install

# fedora如何用yum清除无用的软件包

yum history [undo|redo|info|...]: yum的子命令，显示你yum的历史记录，并且可以撤销指定的记录(undo)，重做指定记录(redo)等等，更多的功能看man yum

yum-plugin-remove-with-leaves：卸载软件包时把因此产生的叶子一起卸载掉，用的时候别加-y选项，看清楚了再确认，有些非常大的依赖树会把主要的系统组件卸载掉，具体用法安装完该插件以后看帮助:yum --help，这个yum插件应该就是最贴近你需求的，不过记住，慎用，如果能从yum history里查到记录的话，还是用yum history undo来操作比较安全。

yum-plugin-show-leaves： 执行安装/卸载以后，显示此次操作所产生的叶子，自动运行，无需要操作。

rpmreaper: 基于ncurses库的程序，通过基于文本的gui界面显示系统中的rpm依赖树，提供各种操作，具体的看man。



#如何在Ubuntu中屏蔽一个网站

打开/etc/hosts文件，添加下面这行

127.0.0.1 domain.com

更换domain.com为你要屏蔽的网站，你完成了编辑处理后，保存该文件并退出。

#将脚本中的信息输出到文件中

Linux中，脚本语言环境中，即你用make xxx及其他一些普通linux命令，比如ls，find等，不同的数字，代表不同的含义： 

0代表标准输入

1代表标准输出

2代表错误输出

而系统默认的stdin是键盘，stdout，stderr都是屏幕，所以当你执行命令，比如make后，所输出的信息，都是可以在屏幕上看到的。所以想要将对应信息输出到某个文件中，就用对应的数字加上重定向符号'>'，实现将这些信息重新定向到对应的文件中即可。下面以make命令为例来说明，如何把对应的信息，输出到对应的文件中：

1.想要把make输出的全部信息，输出到某个文件中，最常见的办法就是：
2.
3.make xxx > build_output.txt
4.
5.此时默认情况是没有改变2=stderr的输出方式，还是屏幕，所以，如果有错误信息，还是可以在屏幕上看到的。
6.
7.2.只需要把make输出中的错误（及警告）信息输出到文件中ing，可以用：
8.
9.make xxx 2> build_output.txt
10.
11.相应地，由于1=stdout没有变，还是屏幕，所以，那些命令执行时候输出的正常信息，还是会输出到屏幕上，你还是可以在屏幕上看到的。
12.
13.3.只需要把make输出中的正常（非错误，非警告）的信息输出到文件中，可以用：
14.
15.make xxx 1> build_output.txt
16.
17.相应地，由于2=stderr没有变，还是屏幕，所以，那些命令执行时候输出的错误信息，还是会输出到屏幕上，你还是可以在屏幕上看到的。
18.
19.4.想要把正常输出信息和错误信息输出到分别的文件中，可以用：
20.
21.make xxx 1> build_output_normal.txt 2>build_output_error.txt
22.
23.即联合使用了1和2，正常信息和错误信息，都输出到对应文件中了。
24.
25.5. 所有的信息都输出到同一个文件中：
26.
27.make xxx > build_output_all.txt 2>&1
28.
29.其中的2>&1表示错误信息输出到&1中，而&1，指的是前面的那个文件：build_output_all.txt 。
30.
31.注意：上面所有的1,2等数字，后面紧跟着大于号'>' ，中间不能有空格。
32.
6.make xxx > build_output_all.txt 2>&1
7.
也可以写成：

make xxx 2>&1 | tee build_output_all.txt

唯一的区别就是，stdout和stderr被导入文件的同时，还可以看到屏幕输出。

#常用命令

## ps –fu $USER | grep java

## find . –name “*.log” | xargs grep …

显示当前用户的所有线程

## ack

http://beyondgrep.com/

## Glances

top 命令是 Linux 下的一个实时任务管理器， 同时也是用于在 GNU/Linux 发行版中寻找系统性能方面的瓶颈，并帮助我们作出正确操作的常用系统监视工具。 她有着一个极为简洁的界面，并自带少量的可以帮助我们快速了解系统性能的实用选项。但是，有些时候想要通过她寻找一个占用系统资源比较大的应用或进程可能会比较困难。 因为 top 命令本身并不会帮助我们高亮那些吃太多 CPU，内存，或者其他资源的程序。为了达到这个目标，这里我们将介绍一款超牛逼的系统监视程序 —— Glances。 她可以自动高亮利用最高系统资源的程序，并为 Linux/Unix 服务器提供尽可能多的信息。

https://github.com/nicolargo/glances/



##获取某程序的完整路径名

当我们在Linux下用ps aux 看到有如下一个进程时：

root     19463  0.0  0.0   1508   272 pts/0    S    16:43   0:00 ./server-a

作为系统管理员的你，如何获得程序server-a所在的完整路径呢？在此告诉大家一个简单的解决办法：从上面ps 的输出中可以看出19463是server-a的PID号，那么运行如下命令：cat /proc/19463/environ ,输出如下：

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/gamesGNOME_KEYRING_PID=2269USER=jiangxinLANGUAGE=zh_CN:XDG_SEAT=seat0TEXTDOMAIN=im-configCOMPIZ_CONFIG_PROFILE=ubuntuHOME=/home/jiangxinQT4_IM_MODULE=fcitxDESKTOP_SESSION=ubuntuXDG_SEAT_PATH=/org/freedesktop/DisplayManager/Seat0GTK_MODULES=overlay-scrollbar:unity-gtk-moduleGNOME_KEYRING_CONTROL=/run/user/1000/keyring-wrFl7VQT_QPA_PLATFORMTHEME=appmenu-qt5MANDATORY_PATH=/usr/share/gconf/ubuntu.mandatory.pathIM_CONFIG_PHASE=1SESSIONTYPE=gnome-sessionLOGNAME=jiangxinGTK_IM_MODULE=fcitxDEFAULTS_PATH=/usr/share/gconf/ubuntu.default.pathXDG_SESSION_ID=c3GDM_LANG=zh_CNXDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session0XDG_RUNTIME_DIR=/run/user/1000DISPLAY=:0XDG_CURRENT_DESKTOP=UnityLANG=zh_CN.UTF-8XAUTHORITY=/home/jiangxin/.XauthorityXMODIFIERS=@im=fcitxXDG_GREETER_DATA_DIR=/var/lib/lightdm-data/jiangxinSHELL=/bin/bashGDMSESSION=ubuntuTEXTDOMAINDIR=/usr/share/locale/XDG_VTNR=7QT_IM_MODULE=ximPWD=/home/jiangxinXDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/usr/share/upstart/xdg:/etc/xdgXDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/CLUTTER_IM_MODULE=ximSELINUX_INIT=YESUBUNTU_MENUPROXY=1DBUS_SESSION_BUS_ADDRESS=unix:abstract=/tmp/dbus-BqwNaGt8wESSH_AUTH_SOCK=/run/user/1000/keyring-wrFl7V/sshSSH_AGENT_PID=2383SSH_AGENT_LAUNCHER=upstartGNOME_DESKTOP_SESSION_ID=this-is-deprecatedJOB=gnome-sessionINSTANCE=UnityUPSTART_EVENTS=started startingUPSTART_JOB=unity-settings-daemonUPSTART_INSTANCE=UPSTART_SESSION=unix:abstract=/com/ubuntu/upstart-session/1000/2299GPG_AGENT_INFO=/run/user/1000/keyring-wrFl7V/gpg:0:1

注意输出中的：PWD=/data1/1230

由此可以判断出程序server-a所在完成路径为： /data1/1230/server-a

来，验证一下吧：

bash-3.2# ls -l /data1/1230/server-a

-rwxr-xr-x 1 root root 5842 Feb 25 16:42 /data1/1230/server-a

果然如此！

##时钟校准:rdate

rdate(receive date)

功能说明：显示其他主机的日期与时间。

语法：rdate [-ps][主机名称或IP地址...]

补充说明：执行rdate指令，向其他主机询问系统时间并显示出来。

参数：

  -p 　显示远端主机的日期与时间。 

  -s 　把从远端主机收到的日期和时间，回存到本地主机的系统时间。

##打印某一文件夹下的所有文件名及其行数

这里分别要考虑到该文件夹有或没有子文件夹的情况，用shell实现打印某一文件夹下的所有文件（如果是子文件夹下的文件，需要打印相对目录）及该文件的行数清单。列表类似这样：

filename1 100行

file/filename2 200行

.......



find -name "*" | xargs wc -l



加 -type f 参数，过滤掉对目录的wc

find -name "*" -type f | xargs wc -l



想要得到指定的格式，用万能的awk：

find -name "*" -type f| xargs wc -l | awk '{print $2" "$1"行"}'



find 后面可加指定目录，如"/etc/"

find "/etc/" -name "*" -type f| xargs wc -l | awk '{print $2" "$1"行"}'

##查看cpu是否支持64位

查看cpuinfo中是否有lm，如果有lm表示支持64位，lm的意思是long mode，具体命令如下：

cat /proc/cpuinfo | grep flags 检查输出里面是否有 lm 字符 或 cat /proc/cpuinfo | grep flags | grep lm | wc -l 输出结果大于 0 表示支持64位

 

查看机器有几个cpu，是否支持64位

1. 查看物理CPU的个数

#cat /proc/cpuinfo |grep "physical id"|sort |uniq|wc -l

 

2. 查看逻辑CPU的个数

#cat /proc/cpuinfo |grep "processor"|wc -l

 

3. 查看CPU是几核

#cat /proc/cpuinfo |grep "cores"|uniq

 

4. 查看CPU的主频

#cat /proc/cpuinfo |grep MHz|uniq

 

# uname -a

Linux euis1 2.6.9-55.ELsmp #1 SMP Fri Apr 20 17:03:35 EDT 2007 i686 i686 i386 GNU/Linux

(查看当前操作系统内核信息)



# cat /etc/issue | grep Linux

Red Hat Enterprise Linux AS release 4 (Nahant Update 5)

(查看当前操作系统发行版信息)



# cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c

      8  Intel(R) Xeon(R) CPU            E5410   @ 2.33GHz

(看到有8个逻辑CPU, 也知道了CPU型号)



# cat /proc/cpuinfo | grep physical | uniq -c

      4 physical id      : 0

      4 physical id      : 1

(说明实际上是两颗4核的CPU)



# getconf LONG_BIT

32

(说明当前CPU运行在32bit模式下, 但不代表CPU不支持64bit)



# cat /proc/cpuinfo | grep flags | grep ' lm ' | wc -l

8

(结果大于0, 说明支持64bit计算. lm指long mode, 支持lm则是64bit)

## apt-cache

apt 0.9.7.7ubuntu4，用于 i386 构架，编译于 Apr 12 2013 23:49:20

Usage: apt-cache [options] command

       apt-cache [options] showpkg pkg1 [pkg2 ...]

       apt-cache [options] showsrc pkg1 [pkg2 ...]



apt-cache is a low-level tool used to query information

from APT's binary cache files



Commands:

   gencaches - Build both the package and source cache

   showpkg - Show some general information for a single package

   showsrc - Show source records

   stats - Show some basic statistics

   dump - Show the entire file in a terse form

   dumpavail - Print an available file to stdout

   unmet - Show unmet dependencies

   search - Search the package list for a regex pattern	查找包含部分关键字的软件包

   show - Show a readable record for the package	获取包的相关信息，如说明、大小、版本等

   depends - Show raw dependency information for a package	了解使用依赖

   rdepends - Show reverse dependency information for a package	了解某个具体的依赖

   pkgnames - List the names of all packages in the system

   dotty - Generate package graphs for GraphViz

   xvcg - Generate package graphs for xvcg

   policy - Show policy settings



Options:

  -h   This help text.

  -p=? The package cache.

  -s=? The source cache.

  -q   Disable progress indicator.

  -i   Show only important deps for the unmet command.

  -c=? Read this configuration file

  -o=? Set an arbitrary configuration option, eg -o dir::cache=/tmp

See the apt-cache(8) and apt.conf(5) manual pages for more information.



## apt-file

是一个软件包查找工具，可以查到软件包所含的文件和安装的位置。

apt-file [options] action [pattern]

apt-file [options] -f action <file>

apt-file [options] -D action <debfile>



Configuration options:

    --architecture		-a  <arch>       Use specific architecture

    --cache			-c  <dir>        Cache directory

    --cdrom-mount		-d  <cdrom>      Use specific cdrom mountpoint

    --dummy			-y               run in dummy mode (no action)

    --fixed-string		-F               Do not expand pattern

    --from-deb		-D               Use file list of .deb package(s) as

                                        patterns; implies -F

    --from-file			-f               Read patterns from file(s), one per line

                                        (use '-' for stdin)

    --ignore-case		-i               Ignore case distinctions

    --non-interactive	-N               Skip schemes requiring user input

                                        (useful in cron jobs)

    --package-only     -l               Only display packages name

    --regexp          -x               pattern is a regular expression

    --sources-list     	-s  <file>       sources.list location

    --verbose         -v               run in verbose mode

    --help            -h               Show this help.

                     --               End of options (neccessary if pattern

                                        starts with a '-')



Action:

update                              Fetch Contents files from apt-sources.

更新软件包的文件库，第一次使用或apt-get update后都需运行一次。

search|find        <pattern>        Search files in packages

查找该文件存在于哪些软件包中。



list|show          <pattern>        List files in packages

显示该软件包的文件

    purge                               Remove cache files

## apt-get

apt 0.9.7.7ubuntu4，用于 i386 构架，编译于 Apr 12 2013 23:49:24

Usage: apt-get [options] command

       apt-get [options] install|remove pkg1 [pkg2 ...]

       apt-get [options] source pkg1 [pkg2 ...]



apt-get is a simple command line interface for downloading and

installing packages. The most frequently used commands are update

and install.



Commands:

   update - Retrieve new lists of packages	更新源。最好定期更新一下使你自己机器上面的数据和服务器(/etc/apt/sources.list列出)上面的信息保持一致,在安装软件之前可以运行一下这个命令保证成功性。

   upgrade - Perform an upgrade	更新已安装的包。这里加上-u选项列出将要升级的软件，可能会提示有些软件不会升级，因为可能会破坏依赖关系，更好的方法是利用apt-get dist-upgrade

你 可以通过cd或者添加源地址来更新，如果你想从cd来升级，首先运行apt-cdrom把cd中的软件添加到/etc/apt/sources源中，然后 运行apt-get dist-upgrade来升级，但是因为apt-get总是使用最新版本，如果cd中的不是最新的版本，那么也不会用到cd。

   install - Install new packages (pkg is libc6 not libc6.deb)	

   remove - Remove packages		删除包

   autoremove - Remove automatically all unused packages	删除所有无用包

   purge - Remove packages and config files	删除包及其依赖的软件包配置文件等

   source - Download source archives	下载该包的源代码

   build-dep - Configure build-dependencies for source packages	安装相关的编译环境

   dist-upgrade - Distribution upgrade, see apt-get(8)	升级系统。这样安装的软件前面apt-get -u upgrade安不了的也会安装了，但个别的仍然不能安装，例如：升级会导致需要卸载一些包，卸载这些包会导致另外的软件不能用，所以就不升级了。

   dselect-upgrade - Follow dselect selections	使用 dselect 升级

   clean - Erase downloaded archive files	清理下载文件的存档

   autoclean - Erase old downloaded archive files	只清理过时的包

   check - Verify that there are no broken dependencies	检查是否有损坏的依赖

   changelog - Download and display the changelog for the given package

   download - Download the binary package into the current directory



Options:

  -h  This help text.

  -q  Loggable output - no progress indicator

  -qq No output except for errors

  -d  Download only - do NOT install or unpack archives

  -s  No-act. Perform ordering simulation

  -y  Assume Yes to all queries and do not prompt

  -f  Attempt to correct a system with broken dependencies in place

  -m  Attempt to continue if archives are unlocatable

  -u  Show a list of upgraded packages as well

  -b  Build the source package after fetching it

  -V  Show verbose version numbers

  -c=? Read this configuration file

  -o=? Set an arbitrary configuration option, eg -o dir::cache=/tmp

See the apt-get(8), sources.list(5) and apt.conf(5) manual

pages for more information and options.

                       This APT has win Cow Powers.

## apt-cdrom

apt-cdrom is a tool to add CDROM's to APT's source list. The

CDROM mount point and device information is taken from apt.conf

and /etc/fstab.



Commands:

   add - Add a CDROM

   ident - Report the identity of a CDROM



Options:

  -h   This help text

  -d   CD-ROM mount point

  -r   Rename a recognized CD-ROM

  -m   No mounting

  -f   Fast mode, don't check package files

  -a   Thorough scan mode

  --auto-detect Auto detect drive and mount point

  -c=? Read this configuration file

  -o=? Set an arbitrary configuration option, eg -o dir::cache=/tmp

See fstab(5)



## apititude

aptitude update 更新可用的包列表

aptitude upgrade 升级可用的包

aptitude dist-upgrade 将系统升级到新的发行版

aptitude install pkgname 安装包

aptitude remove pkgname 删除包

aptitude purge pkgname 删除包及其配置文件

aptitude search string 搜索包

aptitude show pkgname 显示包的详细信息

aptitude clean 删除下载的包文件

aptitude autoclean 仅删除过期的包文件

## dpkg

dpkg -L  软件名  查看软件安装的位置



##打开.sh文件

sudo sh *.sh

##打开其它可执行文件：

./***(如果没有可执行权限，需要chmod)

## nautilus命令

file explore



## 命令行快速打开各类型文件

xdg-open (opens a file or URL in the user's preferred application)

或者： mplayer xxx.mp3

## ED编辑器的使用

ed 编辑器是 Linux 操作系统下最简单的文本编辑器。它是以行为单位对文件进行编辑的编辑器，而不像 MS-DOS 系统下的 edit 那样是以整个屏幕框架为单位对文件进行编辑的。因此，如果你已经习惯了使用 edit 这种风格的编辑器，那么你可能需要一段时间才能习惯 ed 的风格。但是这并不重要，因为 ed 的简便性可以使你很快上手的。 

ed 编辑器的调用很简单，如果你想新建一个文件，那么只需要在命令行窗口中敲入 ed 然后按下回车键即可： 

[titan@localhost titan]$ ed <- 

如果你想编辑一个已经存在的文件，那么你只要在 ed 的后面空一个，然后敲入文件名即可： 

[titan@localhost titan]$ ed filename <- 

激活 ed 命令后进入的是 ed 编辑器的命令行状态，这可能使一些初学者有些不习惯，如果你这时候随便敲入一些内容，系统会返回一个 ?，表示不知道你要执行什么任务： 

[titan@localhost titan]$ ed <- 

abcde <- 

? 



这时候你要明确几个编辑器命令，它们是： 

a - 在文件的末尾添加新内容 

i - 在文件的最后一行之前插入新内容 

o - 把文件输入的最后一行（不论是原来存在的或者插入的）替换成新内容 

. - 退出编辑文件模式进入命令行模式（注意：此时并没有退出 ed 编辑器） 

w - 保存文件 

q - 真正退出 ed 编辑器 



下面我将就着几个命令举例说明一下。 

[titan@localhost titan]$ ed <- 激活 ed 命令 

a <- 告诉 ed 我要编辑新文件 

My name is Titan. <- 输入第一行内容 

And I love Perl very much. <- 输入第二行内容 

. <- 返回 ed 的命令行状态 

i <- 告诉 ed 我要在最后一行之前插入内容 

I am 24. <- 将“I am 24.”插入“My name is Titan.”和“And I love Perl very much.”之间 

. <- 返回 ed 的命令行状态 

c <- 告诉 ed 我要替换最后一行输入内容 

I am 24 years old. <- 将“I am 24.”替换成“I am 24 years old.”（注意：这里替换的是最后输的内容） 

. <- 返回 ed 的命令行状态 

w readme.text <- 将文件命名为“readme.text”并保存（注意：如果是编辑已经存在的文件，只需要敲入 w 即可）

q <- 完全退出 ed 编辑器 

[titan@localhost titan]$ 返回到 Linux 系统的命令行状态 

这是文件的内容是： 

[titan@localhost titan]$ cat readme.text <- 

My name is Titan. 

I am 24 years old. 

And I love Perl vrey much. 

[titan@localhost titan]$ 



因为使用 ed 编辑文件时时看不到文件内容的，而且它不像 MS-DOS 下的 edit 那么灵活，请你在编辑文件是一定要仔细检查输入的内容以保证其正确性，避免反复往返于编辑状态和命令行状态之间，那样会浪费大量的时间。

##在shell中使用chrome命令

以linux的bash shell为例说明 google-chrome这个命令的使用方法

linux中打开chrome浏览器的命令为:"google-chrome"(打开chromium浏览器的命令为:"chromium-browser",chrome浏览器是基于开源的chromium浏览器开发的)

在basn中输入“google-chrome” 执行命令后即可弹出chrome浏览器的窗口,网址为设置的默认的网址

在ban中输入"google-chrome --help"或者"google-chrome -h"即可弹出关于google-chrome这个命令的一些用法信息

在bash中输入"google-chrome  网址"即可打开指定的网址

在bash中输入"google-chrome --app="http://www.baidu.com"" 就可以以应用程序的方式打开网址

其他命令的使用方式同上



##查看字体

fc-list :lang=zh-cn

## mkisofs用法详解



功能说明：建立ISO 9660映像文件。

语法：mkisofs [-adDfhJlLNrRTvz][-print-size][-quiet][-A <应用程序ID>][-abstract <摘要文件>][-b <开机映像文件>][-biblio <ISBN文件>][-c <开机文件名称>][-C <盘区编号，磁区编号>][-copyright <版权信息文件>][-hide <目录或文件名>][-hide-joliet <文件或目录名>][-log-file <记录文件>][-m <目录或文件名>][-M <开机映像文件>][-o <映像文件>][-p <数据处理人>][-P <光盘发行人>][-sysid <系统ID >][-V <光盘ID >][-volset <卷册集ID>][-volset-size <光盘总数>][-volset-seqno <卷册序号>][-x <目录>][目录或文件]

补充说明：mkisofs可将指定的目录与文件做成ISO 9660格式的映像文件，以供刻录光盘。

参数：

-a或--all   mkisofs通常不处理备份文件。使用此参数可以把备份文件加到映像文件中。 

-A<应用程序ID>或-appid<应用程序ID>   指定光盘的应用程序ID。 

-abstract<摘要文件>   指定摘要文件的文件名。

-b<开机映像文件>或-eltorito-boot<开机映像文件>   指定在制作可开机光盘时所需的开机映像文件。

-biblio<ISBN文件>   指定ISBN文件的文件名，ISBN文件位于光盘根目录下，记录光盘的ISBN。

-c<开机文件名称>   制作可开机光盘时，mkisofs会将开机映像文件中的全-eltorito-catalog<开机文件名称>全部内容作成一个文件。

-C<盘区编号，盘区编号>   将许多节区合成一个映像文件时，必须使用此参数。

-copyright<版权信息文件>   指定版权信息文件的文件名。

-d或-omit-period   省略文件后的句号。

-D或-disable-deep-relocation   ISO 9660最多只能处理8层的目录，超过8层的部分，RRIP会自动将它们设置成ISO 9660兼容的格式。使用-D参数可关闭此功能。

-f或-follow-links   忽略符号连接。

-h   显示帮助。

-hide<目录或文件名>   使指定的目录或文件在ISO 9660或Rock RidgeExtensions的系统中隐藏。

-hide-joliet<目录或文件名>   使指定的目录或文件在Joliet系统中隐藏。

-J或-joliet   使用Joliet格式的目录与文件名称。

-l或-full-iso9660-filenames   使用ISO 9660 32字符长度的文件名。

-L或-allow-leading-dots   允许文件名的第一个字符为句号。

-log-file<记录文件>   在执行过程中若有错误信息，预设会显示在屏幕上。

-m<目录或文件名>或-exclude<目录或文件名>   指定的目录或文件名将不会房入映像文件中。

-M<映像文件>或-prev-session<映像文件>   与指定的映像文件合并。

-N或-omit-version-number   省略ISO 9660文件中的版本信息。

-o<映像文件>或-output<映像文件>   指定映像文件的名称。

-p<数据处理人>或-preparer<数据处理人>   记录光盘的数据处理人。

-print-size   显示预估的文件系统大小。

-quiet   执行时不显示任何信息。

-r或-rational-rock   使用Rock Ridge Extensions，并开放全部文件的读取权限。

-R或-rock   使用Rock Ridge Extensions。

-sysid<系统ID>   指定光盘的系统ID。

-T或-translation-table   建立文件名的转换表，适用于不支持Rock Ridge Extensions的系统上。

-v或-verbose   执行时显示详细的信息。

-V<光盘ID>或-volid<光盘ID>   指定光盘的卷册集ID。

-volset-size<光盘总数>   指定卷册集所包含的光盘张数。

-volset-seqno<卷册序号>   指定光盘片在卷册集中的编号。

-x<目录>   指定的目录将不会放入映像文件中。

-z   建立通透性压缩文件的SUSP记录，此记录目前只在Alpha机器上的Linux有效。

## linux命令制作iso镜像

例如：把/dev/cdrom目录制作为镜像，名字为/root/rh1.iso

方法1：dd if=/dev/cdrom of=/root/rh1.iso

方法2：#cat /dev/cdrom >;/root/1.iso

方法3：mkisofs -r -o myiso.iso /dev/cdrom

方法4：cp -r /home/user name.iso

## lspci的使用  

PCI和PCI Express，是计算机常使用的一种高速总线。操作系统中的PCI/PCI-E设备驱动以及操作系统内核，都需要访问PCI及PCI-E配置空间。PCI/PCI-E设备的正常运行，离不开PCI/PCI-E配置空间。通过读写PCI/PCI-E配置空间，可以更改设备运行参数，优化设备运行。本文介绍用户空间可以读取、修改、扫描PCI/PCIE设备的用户命令及使用。在Linux内核中，为PCI和PCI-E只适用了一种总线PCI（内核提供的总线系统），故访问PCI-E配置空间，也包括了PCI设备配置空间。读取PCI-E设备配置空间的命令是lspci。详细命令参数，可以使用man lspci来查看，这里我们只介绍常用参数。命令默认输出结果是，当前系统的所有PCI/PCI-E设备。

常用参数：

-v 显示设备的详细信息。

-vv 显示设备更详细的信息。

-vvv 显示设备所有可解析的信息。

-x 以16进制显示配置空间的前64字节，或者CardBus桥的前128字节。

-xxx 以16进制显示整个PCI配置空间（256字节）。

-xxxx 以16进制显示整个PCI-E配置空间（4096字节）。

-s [[[[<domain>]:]<bus>]:][<slot>][.[<func>]]：

## mplayer使用ascii文本播放电影

首先，你要确认mplayer已经装好，你只需执行下面这条命令：

sudo apt-get install mplayer

接下来，为了播放电影，你需要执行下面的命令，记得把MovieName.avi改成你电脑里面电影文件的名字：

mplayer -vo caca MovieName.avi

“caca”命令代表着彩色文本播放引擎，你也可以使用“-vo aa”命令来替代它，这样你就可以把彩色的文本变成黑白两色。

##信息命令查看大全

```
    # uname -a               # 查看内核/操作系统/CPU信息
    # head -n 1 /etc/issue   # 查看操作系统版本
    # cat /proc/cpuinfo      # 查看CPU信息
    # hostname               # 查看计算机名
    # lspci -tv              # 列出所有PCI设备
    # lsusb -tv              # 列出所有USB设备
    # lsmod                  # 列出加载的内核模块
    # env                    # 查看环境变量资源
    # free -m                # 查看内存使用量和交换区使用量
    # df -h                  # 查看各分区使用情况
    # du -sh <目录名>        # 查看指定目录的大小
    # grep MemTotal /proc/meminfo   # 查看内存总量
    # grep MemFree /proc/meminfo    # 查看空闲内存量
    # uptime                 # 查看系统运行时间、用户数、负载
    # cat /proc/loadavg      # 查看系统负载磁盘和分区
    # mount | column -t      # 查看挂接的分区状态
    # fdisk -l               # 查看所有分区
    # swapon -s              # 查看所有交换分区
    # hdparm -i /dev/hda     # 查看磁盘参数(仅适用于IDE设备)
    # dmesg | grep IDE       # 查看启动时IDE设备检测状况网络
    # ifconfig               # 查看所有网络接口的属性
    # iptables -L            # 查看防火墙设置
    # route -n               # 查看路由表
    # netstat -lntp          # 查看所有监听端口
    # netstat -antp          # 查看所有已经建立的连接
    # netstat -s             # 查看网络统计信息进程
    # ps -ef                 # 查看所有进程
    # top                    # 实时显示进程状态用户
    # w                      # 查看活动用户
    # id <用户名>            # 查看指定用户信息
    # last                   # 查看用户登录日志
    # cut -d: -f1 /etc/passwd   # 查看系统所有用户
    # cut -d: -f1 /etc/group    # 查看系统所有组
    # crontab -l             # 查看当前用户的计划任务服务
    # chkconfig --list       # 列出所有系统服务
    # chkconfig --list | grep on    # 列出所有启动的系统服务程序
    # rpm -qa                # 查看所有安装的软件包 
```

## Linux下查看某个端口下运行的是什么程序

netstat -anp | grep xxxx   #xxxx为端口号

或者

lsof -i :xxxx    #xxxx为端口号

## Windows/Linux文本文件格式转换

DOS/Windows和Linux/Unix的文本文件换行格式不同，基于 DOS/Windows 的文本文件在每一行末尾有一个 CR（回车）和 LF（换行），而 UNIX 文本只有一个LF（换行）。

DOS/Windows文本文件格式转换成Linux/Unix文本文件格式

sed -e 's/.$//' mydos.txt > myunix.txt

说明：替代正则表达式与一行的最末字符匹配，而该字符恰好就是回车。我们用空字符替换它，从而将其从输出中彻底删除。

把Linux/Unix 文本文件格式转换成 DOS/Windows文本文件格式

sed -e 's/$/\r/' myunix.txt > mydos.txt

说明：'$' 正则表达式将与行的末尾匹配，而 '\r' 告诉 sed 在其之前插入一个回车。在换行之前插入回车，每一行就以 CR/LF 结束。

另外还有个方法，使用命令 ：

unix2dos filename

dos2unix filename

## Linux的rename命令

不同于Dos下的rename命令，linux下的rename命令功能非常强大。 rename命令的格式：

rename [ -v ] [ -n ] [ -f ] perlexpr [ files ]

第一个参数：被替换掉的字符串

第二个参数：替换成的字符串

第三个参数：匹配要替换的文件模式

例：rename  main1.c main.c main1.c  将main1.c重命名为main.c

rename支持通配符

?    可替代单个字符

*    可替代多个字符

[charset]  可替代charset集中的任意单个字符

 

eg：文件夹中有这些文件foo1, ..., foo9, foo10, ..., foo278，如果使用

rename foo foo0 foo?

会把foo1到foo9的文件重命名为foo01到foo09，重命名的文件只是有4个字符长度名称的文件，文件名中的foo被替换为foo0。如果使用

rename foo foo0 foo??

foo01到foo99的所有文件都被重命名为foo001到foo099，只重命名5个字符长度名称的文件，文件名中的foo被替换为foo0。如果使用

rename foo foo0 foo*

foo001到foo278的所有文件都被重命名为foo0001到foo0278，所有以foo开头的文件都被重命名。如果使用

ename foo0 foo foo0[2]*

从foo0200到foo0278的所有文件都被重命名为foo200到foo278，文件名中的foo0被替换为foo。

rename支持正则表达式

字母的替换rename "s/AA/aa/" *             //把文件名中的AA替换成aa

修改文件的后缀rename "s/.html/.php/" *     //把.html 后缀的改成 .php后缀

批量添加文件后缀rename "s/$//.txt/" *             //把所有的文件名都以txt结尾

批量删除文件名rename "s//.txt//" *               //把所有以.txt结尾的文件名的.txt删掉

##使用script记录Linux终端会话

许多系统管理员都知道保留一个包含各种任务、配置改变等活动日志的重要性。对一些组织而言，保留“我做了这件事”或“约翰做了那件事”的简单日志就已足够；但另一些组织则需要记录所有改变。对终端输出进行复制粘贴可能非常乏味，我们使用一个叫做script的鲜为人知的程序来解决这个问题，它是大多数Linux产品util-linux软件包的一部分。script记录会话的一切内容：你输入的内容和你看到的内容。它甚至记录颜色；因此如果你的命令提示符或程序输出中包含颜色，script将记录它。要使用script，简单执行以下命令：

$ script

默认情况下，它向当前目录的typescript文件中写入内容。然后，你输入的一切内容都被记录到那个文件中。要往另一个文件中记录日志，只需使用命令：

script /path/to/file

(例如script screen.log)

完成记录后，输入exit退出。这个命令将关闭script会话并保存文件。现在你可以使用cat或其它任何程序来检查日志文件。异常退出也没有问题,仍然记录log,只不过需要加上参数：

script -f ido.log

如果在一个终端上使用：

mkfifo ido.log;script -f ido.log 

然后在另一个终端登录,找到这个ido.log文件,你tail -f 就会滚动输出你操作的内容。

2.使用script的缺点在于，它记录所有特殊的字符；因此你输入的文件中将充满控制字符和ANSI转义序列。你可以在script中使用一个非常简单的shell来解决这个问题：

SHELL=/bin/bash PS1=”$ ” script

使用script时，不要使用交互式程序或处理窗口的程序，如vior top。它们会破坏会话的输出结果。另外，日志文件会记录你使用的任何命令行程序和你完成一项任务所采取的步骤。如果你需要在脚本中编辑一个文件，考虑退出script会话，然后用script –a（它在旧会话后添加新会话）对文件进行编辑后再重新启动会话。

## tee命令

tee--  read from standard input and write to standard output and files

这个命令可以读取终端输入输出到终端或者文件中，有时候可以用来记录make等命令可能产生的输出到终端的大量内容输出到文件中去。这样可以方便记录这些命令的日志。

cmd | tee -a file.txt

> make 2>&1 | tee make.log当然，我们也可以直接重定向到一个文件中> make > make.log

PS: 2>&1是为了记录错误日志if you want to filter the control symbols, try to use the "col" command like this:

$ cat screenlog.0 | col -b > screenlog

or

$ cat typescript | col -b > scriptlog

 执行script -q tty.log后,就开始记录终端的输入输出信息,结束的时候按Ctrl+D即可得到终端的内容文件tty.log

## screen命令

Screen是一个可以在多个进程之间多路复用一个物理终端的窗口管理器,这意味着你能够使用一个单一的终端窗口运行多终端的应用。Screen中有会话的概念，用户可以在一个screen会话中创建多个screen窗口，在每一个screen窗口中就像操作一个真实的 telnet/SSH连接窗口那样。

安装：

CentOS/Red Hat：yum install screen

Debian/Ubuntu：apt-get install screen

源码编译安装:

[root@host1 src]# wget ftp://ftp.gnu.org/pub/gnu/screen/screen-4.0.3.tar.gz

[root@host1 src]# tar -zxvf screen-4.0.3.tar.gz

[root@host1 src]# cd screen-4.0.3

[root@host1 screen-4.0.2]# ./configure

[root@host1 screen-4.0.2]# make

[root@host1 screen-4.0.2]# make install

[root@host1 screen-4.0.2]# install -m 644 etc/etcscreenrc /etc/screenrc

[root@host1 screen-4.0.2]# cp ./screen /bin

注意和一般程序的安装过程有所不同，后面这两条指令一定要执行。 

screen的配置文件，一般在 /etc/screenrc 或者 ~/.screenrc，可以在文件里更改参数设定，也可以通过参数传递或者命令来动态指定。

语法：

screen [-AmRvx -ls -wipe][-d <作业名称>][-h <行数>][-r <作业名称>][-s ][-S <作业名称>]

补充说明：

screen为多重视窗管理程序。此处所谓的视窗，是指一个全屏幕的文字模式画面。通常只有在使用telnet登入主机或是使用老式的终端机时，才有可能用到screen程序。

参数：

-A 　将所有的视窗都调整为目前终端机的大小。

-d <作业名称> 　将指定的screen作业离线。

-h <行数> 　指定视窗的缓冲区行数。

-m 　即使目前已在作业中的screen作业，仍强制建立新的screen作业。

-r <作业名称> 　恢复离线的screen作业。

-R 　先试图恢复离线的作业。若找不到离线的作业，即建立新的screen作业。

-s 　指定建立新视窗时，所要执行的shell。

-S <作业名称> 　指定screen作业的名称。

-v 　显示版本信息。

-x 　恢复之前离线的screen作业。

-ls或--list 　显示目前所有的screen作业。

-wipe 　检查目前所有的screen作业，并删除已经无法使用的screen作业。

常用screen参数：

screen -S yourname -> 新建一个叫yourname的session

screen -ls -> 列出当前所有的session

screen -r yourname -> 回到yourname这个session

screen -d yourname -> 远程detach某个session

screen -d -r yourname -> 结束当前session并回到yourname这个session

在每个screen session 下，所有命令都以 Ctrl+a(C-a) 开始。退出screen使用 exit

例：Ctrl+a,d(按住Ctrl　然后按a　放开a　按d)

C-a ? -> Help，显示简单说明

C-a c -> Create，开启新的 window

C-a n -> Next，切换到下个 window 

C-a p -> Previous，前一个 window 

C-a 0..9 -> 切换到第 0..9 个window

Ctrl+a [Space] -> 由視窗0循序換到視窗9

C-a C-a -> 在两个最近使用的 window 间切换 

C-a x -> 锁住当前的 window，需用用户密码解锁

C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里    每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。 

C-a z -> 把当前session放到后台执行，用 shell 的 fg 命令則可回去。

C-a w -> windows，列出已开启的 windows 有那些 

C-a t -> Time，显示当前时间，和系统的 load 

C-a K -> kill window，强行关闭当前的 window

screen可以同步显示你的屏幕给另一个会话。这在给别人处理问题是尤为好用，可以让对方同步看到你的操作。双方同时登陆一台主机，演示方输入  screen -S example，观看方输入 screen -x example，即可同步显示演示方输入的内容

## tree命令

有时我们需要生成目录树结构:

这时需要用到TREE命令:

关于TREE命令的一些参数:

常见的用法:

tree -a 显示所有

tree -d 仅显示目录

tree -L n n代表数字..表示要显示几层...

tree -f 显示完整路径..

当然tree支持重定向至文件...

tree -L 4 >dirce.doc即可生成UTF8格式的文档..我们也可以在windows 下查看..

注意:生成的TXT或其他文件在win下面打开时也为乱码...这时我们要选择字符编码为UTF-8..当然..UTF-8是你linux下的默认字符集才可以......

## Linux下创建目录和文件 

创建文件夹：

语法：mkdir [-p][--help][--version][-m <目录属性>][目录名称]

说明：mkdir可建立目录并同时设置目录的权限。

参数：

  -m<目录属性>或--mode<目录属性>   建立目录时同时设置目录的权限。

  -p或--parents   若所要建立目录的上层目录目前尚未建立，则会一并建立上层目录

例：

mkdir aaa

mkdir -p aaa

mkdir -m 777 aaa   (创建一个名字为aaa的可写可读文件夹)

创建文件：

vi a.php

echo “abfdsfdsf” > b.txt

cat > c.txt

具体步骤:

1、键入cat > filename.txt 后回车 

2、录入文本内容； 

3、键入回车； 

4、在键盘上按下Ctrl+D (或者键入Control－D)。

## linux连接投影机

方案一：

一般来说，需要笔记本当前使用的分辨率和投影仪的分辨率相同，才能在投影仪上显示笔记本的X。那么，可以先运行这个命令： 

$xrandr

比如在我的电脑上，结果如下：

$xrandr

 SZ:    Pixels          Physical       Refresh

*0   1280 x 1024   ( 433mm x 346mm )  *50   54

 1   1024 x 768    ( 346mm x 260mm )   51   60   61

 2    800 x 600    ( 270mm x 203mm )   52   65   66   67   68

 3    640 x 480    ( 216mm x 162mm )   53   73   74   75

 4   1280 x 960    ( 433mm x 325mm )   55

 5   1280 x 800    ( 433mm x 270mm )   56

 6   1280 x 768    ( 433mm x 260mm )   57

 7   1152 x 864    ( 390mm x 292mm )   58

 8   1152 x 768    ( 390mm x 260mm )   59

 9    960 x 600    ( 325mm x 203mm )   62

 10   840 x 525    ( 284mm x 177mm )   63

 11   832 x 624    ( 281mm x 211mm )   64

 12   800 x 512    ( 270mm x 173mm )   69

 13   720 x 450    ( 243mm x 152mm )   70

 14   640 x 512    ( 216mm x 173mm )   71   72

 15   640 x 400    ( 216mm x 135mm )   76

 16   640 x 384    ( 216mm x 130mm )   77

 17   576 x 432    ( 195mm x 146mm )   78

 18   576 x 384    ( 195mm x 130mm )   79

 19   512 x 384    ( 173mm x 130mm )   80   81   82

 20   416 x 312    ( 140mm x 105mm )   83

 21   400 x 300    ( 135mm x 101mm )   84   85   86   87

 22   320 x 240    ( 108mm x  81mm )   88   89   90

Current rotation - normal

Current reflection - none

Rotations possible - normal

Reflections possible - none

 

第0条加了*号，说明这是笔记本电脑当前使用的分辨率。如果投影仪的分辨率是1024x768，那么就需要改变笔记本电脑的分辨率。因为在上面的结果中，1024x768对应第1条，所以运行这个命令来改变分辨率：

$xrandr -s 1

这样就切换了分辨率。等待投影仪的搜索吧。

首先接上VGA，执行命令(VGA代表显示器，LVDS代表笔记本液晶屏):

$ xrandr --output VGA --auto

当前桌面会复制到VGA上面，此时执行xrandr会看到有了VGA-0

断开VGA-0:

$ xrandr --output VGA-0 --auto

按照当前的配置扩展桌面:

$xrandr --output VGA-0 --auto --left-of LVDS

这是需修改xorg.conf，先用不带参数执行xrandr能够列出当前的显示设备和每个设备支持的模式。Screen代表了总显示区域，VGA代表显示器，LVDS代表笔记本液晶屏。

 

Screen 0: minimum 320 x 200, current 1280 x 768, maximum 1280 x 1280 

VGA connected (normal left inverted right x axis y axis)

   1280x1024      75.0 +   69.8     59.9  

   1024x768       75.1     70.1     60.0  

   800x600        72.2     75.0     60.3  

   640x480        75.0     72.8     65.4     60.0  

   720x400        70.1  

LVDS connected 1024x768+0+0 (normal left inverted right x axis y axis) 246mm x 184mm

   1024x768       50.0*+   60.0     40.0  

   800x600        60.3  

   640x480        60.0     59.9 

 

修改：

 

gksudo gedit /etc/X11/xorg.conf

 

修改后如下：

 

Section "Screen"

   Identifier "Default Screen"

   Monitor "Configured Monitor"

   Device "Configured Video Device"

   SubSection "Display" 

      Virtual 2304 1024 #左右扩展双屏,2304=1280+1024,1024=max(1024,768)

   EndSubSection 

EndSection

 

注意：Ubuntu 8.04中的xorg.conf已经非常精简，Subsection "Display" 可能要自己添加，别忘记 EndSubSection

 

 

xrandr 命令行可以很方便地切换双屏，常用方式如下，其他的可以自己探索：

 

xrandr --output VGA --same-as LVDS --auto

 

         打开外接显示器(最高分辨率)，与笔记本液晶屏幕显示同样内容（克隆）

 

xrandr --output VGA --same-as LVDS --mode 1024x768

 

         打开外接显示器(分辨率为1024x768)，与笔记本液晶屏幕显示同样内容（克隆）

 

xrandr --output VGA --right-of LVDS --auto

 

         打开外接显示器(最高分辨率)，设置为右侧扩展屏幕

 

xrandr --output VGA --off

 

          关闭外接显示器

 

xrandr --output VGA --auto --output LVDS --off

 

        打开外接显示器，同时关闭笔记本液晶屏幕（只用外接显示器工作）

 

xrandr --output VGA --off --output LVDS --auto

 

        关闭外接显示器，同时打开笔记本液晶屏幕 (只用笔记本液晶屏)

 

方案二：

 

打开xorg.conf

 

gksudo gedit /etc/X11/xorg.conf

 

修改Section “Device”如下：

 

Section "Device"

 

Identifier "Configured Video Device"

 

Option "TwinView" "True" #打开双显支持

 

Option "TwinViewOrientation" "Clone" #复制模式，Relative为扩展模式

 

Option "UseEdidFreqs" "True" #打开刷新频率设置

 

Option "Metamodes" "1024x768_60, 1024x768; 1024x768_60,800x600" #刷新频率模式，指明这两个设备的分辨率，逗号前的第一个是本机显示设备，逗号后的第二个是外部设备，分号分隔开多套模式，可以设两套方案或更多。

 

EndSection

 

保存。连接好投影仪，重新启动Xwindows(Ctrl+Alt+Backspace)就OK了。

#鸟哥的linux私房菜勘误表

鸟哥的Linux私房菜基础学习篇(第三版)简体中文勘误表(人民邮电出版社)



简体中文版书籍资料：



出版日期：2010年7月第3版



书籍ISBN：978-7-115-22626-6



出版社：人民邮电出版社







正文P10，0.2.2 内存，表0-2



“DDR DDRII800 64 400 800 6.4GB/s”



应改为：“DDR DDRII800 64 200 800 6.4GB/s”







P19，0.4.1 机器程序与编译程序，图0-17下面第一行



“从上面的图示我们......。鸟哥已将经程序代码(英文)写成中文，”



应改为：“从上面的图示我们......。鸟哥已经将程序代码(英文)写成中文，”







P30，1.1.2 Linux之前UNIX的历史，最后一行



“此外，Minux操作系统的开发者仅有谭宁邦教授”



应改为：“此外，Minix操作系统的开发者仅有谭宁邦教授”







P46，1.4 重点回顾



“1984年由Andrew Tannenbaum制作出Minix操作系统，”



应改为：“1984年由Andrew Tanenbaum制作出Minix操作系统，”







P46，1.4 重点回顾



“目前Linux内核的开发分为两种版本......；一种是开发中版本，如2.5.x版”



应改为：“目前Linux内核的开发分为两种版本......；一种是开发中版本的奇数版，如2.5.x版”







P55，2.2.3 X Window的学习



“Open Office(http://www.latex-project.org/)”



应改为：“Open Office(http://www.openoffice.org/)”







P160，6.5 本章练习，请问下面的目录主要放置什么数据？



“/etc/、/etc/initd、/boot、/usr/bin、/bin、/usr/sbin、/sbin、/dev、/var/log。”



应改为“/etc/、/etc/init.d、/boot、/usr/bin、/bin、/usr/sbin、/sbin、/dev、/var/log。”，并去掉前面的小方点







P200，8.1.3 Linux的Ext2文件系统(inode)，例题



“所有文件容量为：50 x 10000(bytes)= 488.3KB，但此时浪费的容量为： 4046 x 10000(bytes) = 38.6MB”



应改为“所有文件容量为：50 (bytes)x 10000 = 488.3KB，但此时浪费的容量为： 4046 (bytes) x 10000 = 38.6MB”







P203，8.1.3 Linux的Ext2文件系统(inode)，block bitmap



“同样......，此时在block bitmpap当中相对应到该block号码的标志就要修改”



应改为：“同样......，此时在block bitmap当中相对应到该block号码的标志就要修改”







P243，8.6.2 磁盘空间的浪费问题，第二个灰色框



“118  /etc   <==单位是KB”



应改为“118  /etc   <==单位是MB”







繁体中文“如果在文章內有對齊的區塊，可以使用 [ctrl]-v 進行複製/貼上/刪除的行為”



P291，10.5 重点回顾，倒数第五点



“可以使用[ctrl]-v进行复制/粘帖/删除的行为。”







P301，11.2.2 变量的显示与设置，第三行



“变量的显示就如同上面的范例，利用ehco就能够读出，”



应改为：“变量的显示就如同上面的范例，利用echo就能够读出，”







P316，11.2.8 变量内容的删除、替代与替换，第一个灰色框



“然后测试一下等号（-）的用法”



应改为：“然后测试一下减号（-）的用法”







P338，11.6.2 排序命令，本节最后一行



“就使用wc-c这个参数”



应改为：“就使用wc-m这个参数”







P354，12.2.3 基础正则表达式练习，例题四



“*(星号)：代表重复前一个0到无穷多次的意思，为组合形态”



应改为：“*(星号)：代表重复前一个字元，0到无穷多次的意思，为组合形态”







P356，12.2.4 基础正则表达式字符(characters)，表12-2，[n1-n2]



“grep -n '[0-9]' regular_express.txt”



应改为：grep -n '[A-Z]' regular_express.txt







P379，13.2.2 script的执行方式区别，图13-2 sh02.sh在父进程中运行



“sh sh02.sh在此执行”



应改为：“source sh02.sh在此执行”







P430，14.4.2 sudo，visudo与/etc/sudoers



“有趣吧……，所以这个文件就是/etc/sudoerds”



应改为“有趣吧……，所以这个文件就是/etc/sudoers”







P449，14.9 本章习题，第三个灰色框



“useradd -G youcan -s -m $username”



应改为：“useradd -G youcan -s /bin/bash -m $username”







P500，16.3.2 系统的配置文件：/etc/crontab，Tips



“/etc/init.d/crondrestart”



应改为：“/etc/init.d/crond restart”







P515，17.2.3 脱机管理问题，第二个灰色框



“[root@www ~]#exit”应在灰色框中



“如果你再次登录的话，再使用ps -l去查看你的进程，”



应改为：“如果你再次登录的话，再使用pstree去查看你的进程，”







P560，18.2.1 默认值配置文件，表18-1，per_source



“设置值：[一个数字或NULIMITED]”



应改为：“设置值：[一个数字或UNLIMITED]”







P572，18.4.3 CentOS 5.x 默认启动的服务简易说明，表18-2，xfs



“如果你不启动X窗口的话，那么这个服务可以启动。”



应改为：“如果你不启动X窗口的话，那么这个服务可以不启动。”







P572，18.5 重点回顾，倒数第三行



“而启动的方式则为/etc/init.d/xientd restart。”



应改为：“而启动的方式则为/etc/init.d/xinetd restart。”







P579，19.2.1 日志文件内容的一般格式，第四行



“某个demon执行过程老是不顺畅时；”



应改为：“设置值：某个daemon执行过程老是不顺畅时；”







P627，20.5 重点回顾，第六点



“init的配置文件为/etc/initab，”



应改为：“init的配置文件为/etc/inittab，”







P652，21.3.2 驱动USB设备，第二点



“至于USB2.0在Linux上都以Enahnced Host Controller Interface (EHCI)来驱动的。”



应改为：“至于USB2.0在Linux上都以Enhanced Host Controller Interface (EHCI)来驱动的。”







P740，25.1.3 选择备份设备，存储设备的考虑



“硬盘：/dev/hd[a-d][1-16] (IDE), /dev/sd[a-p][1-16] (SCSI/SATA)”



应改为：“硬盘：/dev/hd[a-d][1-63] (IDE), /dev/sd[a-p][1-16] (SCSI/SATA)”



 



                                                                                     2011年9月16日 
# ssh相关

## Agent admitted failure to sign using the key 
ssh-keygen 产生出 id_rsa, id_rsa.pub, 已经都放到正确位置(.ssh), 但是联机时却出现下述讯息:

Agent admitted failure to sign using the key

解法

于自己的机器上, 执行 ssh-add, 会出现下述讯息.

Identity added: /home/user/.ssh/id_rsa (/home/user/.ssh/id_rsa)

## connect to host localhost port 22: Connection refused

错误原因：

1.sshd 未安装

2.sshd 未启动 

3.防火墙

4需重新启动ssh 服务



解决方法：

1.确定安装sshd: 

$ sudo apt-get install openssh-server 

2.启动sshd: 

$ sudo net start sshd 

3.检查防火墙设置,关闭防火墙： 

$ sudo ufw disable

检验方法：

输入命令：

$ ssh localhost  

若成功，则表示安装成功，且连接通过；

但是有的时候虽然成功了但是还是会出现Connection refused 问题。

运行 ps -e | grep ssh，查看是否有sshd进程：

 

有时候虽然可以看到sshd 但是还是不能连接成功

这时候就要想到重新启动一下：sudo service ssh restart

然后在连接 
#查看linux进程的执行文件路径 
具体做法就是：

           1、以超级用户登陆

           2、进入/proc目录

           3、ps查看所有符合./cmd的进程，找出其对应的PID进程号

           4、用ll命令： ll 进程号 

              如下显示一个示例：

              [root@Cluster1 proc]# ll 22401 (proc文件夹中有对应PID码的文件名,进入即可)

       total 0

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 cmdline

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 cpu

       lrwxrwxrwx    1 zhouys    zhouys     0 Dec 11 11:10 cwd -> /home/zhouys/sbs/bin

       -r--------    1 zhouys    zhouys     0 Dec 11 11:10 environ

       lrwxrwxrwx    1 zhouys    zhouys     0 Dec 11 11:10 exe -> /home/zhouys/sbs/bin/cbs (deleted)

       dr-x------    2 zhouys    zhouys     0 Dec 11 11:10 fd

       -r--------    1 zhouys    zhouys     0 Dec 11 11:10 maps

       -rw-------    1 zhouys    zhouys     0 Dec 11 11:10 mem

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 mounts

       lrwxrwxrwx    1 zhouys    zhouys     0 Dec 11 11:10 root -> /

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 stat

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 statm

       -r--r--r--    1 zhouys    zhouys     0 Dec 11 11:10 status

              /proc文件系统下的 进程号目录 下面的文件镜像了进程的当前运行信息，

              从中可以看到：

              cwd符号链接的就是进程22401的运行目录；

              exe符号连接就是执行程序的绝对路径；

              cmdline就是程序运行时输入的命令行命令；本例为：./cbs

              cpu记录了进程可能运行在其上的cpu；显示虚拟的cpu信息

              environ记录了进程运行时的环境变量

              fd目录下是进程打开或使用的文件的符号连接

              ...

                  

        通过cwd直接进入进程运行目录，通过查看相关信息就可以定位此目录对应那个端口号，以及

    定位是那个应用才使用此服务程序。       



3. ps -aux 命令



　　ps也可打印其路径,但不是万能的,有些路径只能使用以上两种方法取得.

#一些网络文章

12款最佳Linux命令行终端工具

http://www.vaikan.com/best-terminal-alternatives-for-linux-systems/

Linux下好玩的命令

http://www.cnblogs.com/joeyupdo/articles/2768113.html

动画演示一些无用但有趣的Linux命令

http://www.vaikan.com/10-funny-liunx-command/

Linux中10个有用的命令行补齐命令

http://www.geekfan.net/8169/

Linux中的10个链接操作符

http://linux.cn/thread/12205/1/1/

7 个致命的 Linux 命令

http://linux.cn/thread/10246/1/1/

翻墙！（Chrome+代理工具GoAgent+SwitchySharp插件/火狐Firefox+AutoProxy）

http://blog.chinaunix.net/uid-24250828-id-3788304.html

通过命令行查找一个IP的地理位置信息

http://www.geekfan.net/7863/

多终端管理器tmux使用详解

http://blog.csdn.net/stelalala/article/details/9025691

Linux系统里如何彻底的清空屏幕？

http://www.vaikan.com/how-to-clear-the-terminal-screen-for-real-in-case-of-linux/

如何在Linux上将HTML页面转化成png图片

http://linux.cn/article-2708-1.html

SSH原理与运用（一）：远程登录

http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html

SSH原理与运用（二）：远程操作与端口转发

http://www.ruanyifeng.com/blog/2011/12/ssh_port_forwarding.html

LNMP安装快速导航（官网教程）

http://lnmp.org/install.html

ubuntu删除旧内核和多余启动项 

http://pppboy.blog.163.com/blog/static/3020379620113173147935/

各个Linux版本的本地root密码破解方法

http://os.51cto.com/art/200910/159523.htm

apt-get remove, apt-get autoremove和aptitude remove的区别

http://blog.csdn.net/jiangxinnju/article/details/38341283

# Linux编程学习之路

# GTK+相关

##在Windows下使用GTK+

由于GTK+的跨平台特性, 我们可以在Windows下使用DevCpp来开发使用GTK+图形库的GUI程序.

  步骤如下:



1. 下载DevCPP, 也叫Dev-C++, 我使用的版本是4.9.9.2, 并安装



2. 下载gtk+ for win32工具包集合, 这个里面含有编译运行GTK+程序所需的所有东西, 不需要一个一个包下载安装了. 地址 : http://ftp.gnome.org/pub/gnome/binaries/win32/gtk+/2.14/gtk+-bundle_2.14.4-20081108_win32.zip, 照提示安装, 我的安装目录为 D:/dev/GTK



3. 将D:/dev/GTK/bin加入环境变量PATH



4. 运行cmd, 输入 " pkg-config --cflags --libs gtk+-2.0 > d:/a.txt", 意思是把编译GTK+程序所需要的参数都重定向到D盘的a.txt文本文件中



5. 打开DevCpp, 新建一个工程, 注意工程类型为 Windows Application, C工程.

   DevCpp可能会给你生成一个源文件, 将这个源文件的所有内容替换为一个简单的GTK+代码, 以下是一个例子:

#include <gtk/gtk.h>

int  main( int  argc, char  *argv[])

{

    GtkWidget *window;

    gtk_init(&argc,&argv);

    window=gtk_window_new(GTK_WINDOW_TOPLEVEL);

    gtk_window_set_title(GTK_WINDOW(window),g_locale_to_utf8("中文" ,-1,NULL,NULL,NULL));

    g_signal_connect(window,  "destroy", G_CALLBACK(gtk_main_quit), &window);

    gtk_widget_show(window);

    gtk_main();

     return  0;

}

6.点击 工程 > 工程属性 > "参数"选项卡, 在"编译器"框中输入a.txt的前半部分内容,我机器上是这样的:

 -mms-bitfields -ID:/dev/GTK/include/gtk-2.0 -ID:/dev/GTK/lib/gtk-2.0/include -ID:/dev/GTK/include/atk-1.0 -ID:/dev/GTK/include/cairo -ID:/dev/GTK/include/pango-1.0 -ID:/dev/GTK/include/glib-2.0 -ID:/dev/GTK/lib/glib-2.0/include -ID:/dev/GTK/include/libpng13 

  在"连接器"框中输入a.txt的后半部分内容, 我机器上是这样的:

 -LD:/dev/GTK/lib -lgtk-win32-2.0 -lgdk-win32-2.0 -latk-1.0 -lgdk_pixbuf-2.0 -lpangowin32-1.0 -lgdi32 -lpangocairo-1.0 -lpango-1.0 -lcairo -lgobject-2.0 -lgmodule-2.0 -lglib-2.0 -lintl

  注意这些内容会根据GTK+安装目录的不同而有所差别, 再说一遍, 我机器上是D:/dev/GTK. 设置完后点"确定".



7. 编译运行.

如果出现一个简单的空白窗口, 恭喜你成功了. [完]

# GTK中的delete_event和destroy 
delete_event 事件一般由用户或者说用户通过窗口管理器产生，即点击窗口右上角的退出按钮。假如不做任何特殊处理，窗口管理器会自动产生destroy信号；如果我们自 定义了处理delete_event事件的回调函数，是否产生destroy信号就和函数的返回值有关，如果是FALSE就产生，反之则没有效果。

至 于destroy，除了可以由delete_event事件产生之外，还可以通过gtk_widget_destroy函数与其它信号发生交换。同样，如果不加指定，默认结果是关闭所指向的窗口但并不结束进程。如果我们希望主窗口和进程一起关闭，必须使用gtk_main_quit()。

# g_signal_connect 与 g_signal_connect_swapped

在 2.0 版，信号系统已从 GTK 移到 GLib，因此在函数和类型的说明中有前缀 "g_" 而不是 "gtk_"。我们不打算介绍 GLib 2.0 信号系统相对 GTK 1.2 信号系统扩展的细节。

在我们详细分析 helloworld 程序之前，我们会讨论信号和回调函数。GTK 是一个事件驱动的工具包，意味着它会等在 gtk_main() 那里，直到下一个事件发生，才把控制权传给适当的函数。

控制权的传递是使用“信号”的办法来完成的。(注意这里的信号并不等同于 Unix 系统里的信号，并且也不是用它们实现的，虽然使用的术语是一样的。) 当一个事件发生时，如按一下鼠标键，所按的构件会“发出”适当的信号。这就是 GTK 的工作机制。有所有构件都继承的信号，如 "destroy"，有构件专有的信号，如开关 (toggle) 按钮发出的 "toggled" 信号。

要使一个按钮执行一个动作，我们需设置信号和信号处理函数之间的连接。可以这样使用函数来设置连接：

gulong g_signal_connect( gpointer *object,const gchar *name,GCallback func,gpointer func_data );

第一个参数是要发出信号的构件，第二个参数是你想要连接的信号的名称，第三个参数是信号被捕获时所要调用的函数，第四个参数是你想传递给这个函数的数据。

第三个参数指定的函数叫做回调函数，一般为下面的形式：

void callback_func( GtkWidget *widget,gpointer callback_data );

第一个参数是一个指向发出信号的构件的指针，第二个参数是一个指向数据的指针，就是上面 g_signal_connect() 函数的最后一个参数传进来的数据。

注意上面回调函数的声明只是一般的形式，有些构件的特殊信号会用不同的调用参数。

另一个在 helloworld 示例中使用的调用，是：

gulong g_signal_connect_swapped( gpointer *object,const gchar *name,GCallback func,gpointer *slot_object );

g_signal_connect_swapped() 和 g_signal_connect() 相同，只是回调函数只用一个参数，一个指向 GTK 对象的指针。所以当使用这个函数连接信号时，回调函数应该是这样的形式

void callback_func( GtkObject *object );



这个对象通常是一个构件。然而我们一般不用函数 g_signal_connect_swapped() 设置回调。它们常用来调用一个只接受一个单独的构件或者对象作为参数的 GTK 函数，如同我们的 helloworld 示例中那样。



拥有两个函数来设置信号连接的目的只是为了允许回调函数有不同数目的参数。GTK 库中许多函数仅接受一个单独的构件指针作为其参数，所以对于这些函数你要用 g_signal_connect_swapped()，然而对你自己定义的函数，你可能需要附加的数据提供给你的回调函数。

# CodeBlocks 使用经验谈  

以最新的CodeBlocks 10.05为例。

一、自定义自动补全

1、依次打开 Project -> Properties -> C/C++ parser options 来到 Additional search paths;

2、点  Add 选择头文件的路径后点确定;

3、在源文件中添加相应的头文件后即可实现自动补全。

或者在第2步，改成“工作空间”中包含相应的头文件也行。

apt-get install codeblocks-contrib

# ubuntu 无法使用gnome库,该如何处理

gcc: 
gcc -o gnome1 gnome1.c `pkg-config –libs –cflags libgnome-2.0 libgnomeui-2.0`

codebocks:

`pkg-config libgnome-2.0 libgnomeui-2.0 --cflags`

`pkg-config  libgnome-2.0 libgnomeui-2.0 --libs`

`pkg-config gtk+-2.0 --cflags --libs`

#线程调用

-lpthread

#常用函数

herror(3)

# Linux 中C语言如何清空标准输入流

今天在Linux程序设计的时候需要清空标准输入缓冲区，于是使用了如下Windows程序设计中的方法：fflush(stdin)，这个fflush()函数根本不是标准C中的函数，只是标准C的扩展，所以在Linux中使用根本不行；在网上搜索了下，发现有网友建议使用rewind(stdin)；这个函数其实是将指针指向流的开始处。但是它是文件操作中的一个函数，操作的是FILE型流，在Windows程序设计中是可以清空标准输入缓冲区的，但是在Linux中不行。

注：上述内容有几处错误，详见《The Standart Library》

通过读完标准缓冲区中的剩余字符并丢弃掉来清空标准缓冲区，使用的函数是getchar()，此函数的作用是从标准输入缓冲区中读出一个字符，此方法中Linux中可行。如果需要清除stdin可以通过如下循环实现：

char ch;

while((ch=getchar())!='/n'&&ch!=EOF);

以上语句将清除stdin中的字符，知道遇到换行符或者是读完缓冲区。

# linux中无 conio.h的解决办法（原创）

conio.h不是C标准库中的头文件，在ISO和POSIX标准中均没有定义。conio是Console Input/Output（控制台输入输出）的简写，其中定义了通过控制台进行数据输入和数据输出的函数，主要是一些用户通过按键盘产生的对应操作，比如getch()函数等等。大部分DOS，Windows，Phar Lap，DOSX，OS/2 等平台上的C编译器提供此文件，UNIX 和Linux平台的C编译器本身通常不包含此头文件，但已经有其兼容包，可参考：

http://conio.sourceforge.net/

另外大家平时主要是利用conio.h这个头文件中的getch()函数，即读取键盘字符但是不显示出来（without echo)，但是含有conio.h的程序在linux无法直接编译通过，因为linux没有这个头文件，除了利用上述的兼容包外还可以在linux采用原生的方法达到同样的效果，那就是利用linux系统的命令stty –echo，它代表不显示输入内容，源代码如下。

//in windows

#include<stdio.h>

#include<conio.h>

int main(){

char c;

printf("input a char:");

c=getch();

printf("You have inputed:%c \n",c);

return 0;

}

//in linux

#include<stdio.h>

int main(){

char c;

printf("Input a char:");

system("stty -echo");

c=getchar();

system("stty echo");

printf("You have inputed:%c \n",c);

return 0;

}

#改变linux终端颜色

文本终端的颜色可以使用“ANSI非常规字符序列”来生成，“ANSI非常规字符序列”均以 Esc[ 作为控制码的开始标志，其中，Esc 的ansi码为 27-十进制，33-八进制，所以在c中，可以使用 \033 表示。



echo -e "\033[前景;背景;光标m ME \033[0m"

 

举例：echo -e "\033[44;37;5m ME \033[0m COOL"

 

以上命令设置背景成为蓝色，前景白色，闪烁光标，输出字符“ME”，然后重新设置屏幕到缺省设置，输出字符 “COOL”。“e”是命令 echo 的一个可选项，它用于激活特殊字符的解析器。“\033”引导非常规字符序列。“m”意味着设置属性然后结束非常规字符序列，这个例子里真正有效的字符是 “44;37;5” 和“0”。修改“44;37;5”可以生成不同颜色的组合，数值和编码的前后顺序没有关系。可以选择的编码如下所示：



前景      背景       颜色

---------------------------------------

30          40          黑色

31          41          红色

32          42          绿色

33          43          黄色

34          44          蓝色

35          45          紫红色

36          46          青蓝色

37          47          白色





\33[0m 关闭所有属性 

\33[1m 设置粗体 

\33[2m 设置一半亮度（模拟彩色显示器的颜色） 

\33[4m 下划线 

\33[5m 闪烁 

\33[7m 反显 

\33[8m 消隐 

\33[30m -- \33[37m 设置前景色 

\33[38m在缺省的前景颜色上设置下划线

\33[39m在缺省的前景颜色上关闭下划线 

\33[40m -- \33[47m 设置背景色 

\33[nA 光标上移n行 

\33[nB 光标下移n行 

\33[nC 光标右移n行 

\33[nD 光标左移n行 

\33[y;xH设置光标位置 

\33[2J 清屏 

\33[K 清除从光标到行尾的内容 

\33[s 保存光标位置 

\33[u 恢复光标位置 

\33[?25l 隐藏光标 

\33[?25h 显示光标

\033[0q         　	关闭所有的键盘指示灯 

\033[1q         　	设置“滚动锁定”指示灯 (Scroll Lock) 

\033[2q         　	设置“数值锁定”指示灯 (Num Lock) 

\033[3q         　	设置“大写锁定”指示灯 (Caps Lock) 

\033[15:40H     		把关闭移动到第15行，40列 

\007            　　	发蜂鸣生beep

# linux下如何用c语言调用shell命令

#include <stdlib.h>

int system(const char *string);

例：在~/myprogram/目录下有shell脚本test.sh，内容为

　　#!bin/bash

　　#test.sh

　　echo $HOME

　　在该目录下新建一个c文件systemtest.c，内容为：

　　#include<stdlib.h>

　　

　　main()

　　{

　　system("~/myprogram/test.sh");

　　}

　　执行结果如下：

　　xiakeyou@ubuntu:~/myprogram$ gcc systemtest.c -o systemtest

　　xiakeyou@ubuntu:~/myprogram$ ./systemtest

　　/home/d/e/xiakeyou

　　xiakeyou@ubuntu:~/myprogram$

　　2）popen(char *command,char *type)

　　执行过程：popen()会调用fork()产生子进程，然后从子进程中调用/bin/sh -c来执行参数command的指令。参数type可使用“r”代表读取，“w”代表写入。依照此type值，popen()会建立管道连到子进程的标准输出设备或标准输入设备，然后返回一个文件指针。随后进程便可利用此文件指针来读取子进程的输出设备或是写入到子进程的标准输入设备中。此外，所有使用文件指针(FILE*)操作的函数也都可以使用，除了fclose()以外。

　　返回值：若成功则返回文件指针，否则返回NULL，错误原因存于errno中。

　　注意：在编写具SUID/SGID权限的程序时请尽量避免使用popen()，popen()会继承环境变量，通过环境变量可能会造成系统安全的问题。

　　例：C程序popentest.c内容如下：

　　#include<stdio.h>

　　main()

　　{

　　FILE * fp;

　　charbuffer[80];

　　fp=popen(“~/myprogram/test.sh”,”r”);

　　fgets(buffer,sizeof(buffer),fp);

　　printf(“%s”,buffer);

　　pclose(fp);

　　}

　　执行结果如下：

　　xiakeyou@ubuntu:~/myprogram$ vim popentest.c

　　xiakeyou@ubuntu:~/myprogram$ gcc popentest.c -o popentest

　　xiakeyou@ubuntu:~/myprogram$ ./popentest

　　/home/d/e/xiakeyou

　　xiakeyou@ubuntu:~/myprogram$

　　只是偶能力可能有点有限，没有太看懂。直接用system()倒是脚本可是执行，只是返回值却是一塌糊涂，试了多次也没有找到什么规律。不免又看了一下上面的那篇博文，得到一些启发，可以这样来实现：

　　先将脚本的返回值利用 echo > XXXXX 输出到一个本地文件中

　　当需要这个返回值是，可是通过C语言的文件操作函数来直接从文件中读取

　　后来一想，这应该就是上文中POPEN的实现方法！

C程序调用shell脚本共有三种法子 ：system()、popen()、exec系列函数 system() 不用你自己去产生进程，它已经封装了，直接加入自己的命令exec 需要你自己 fork 进程，然后exec 自己的命令

popen() 也可以实现执行你的命令，比system 开销小

1）system(shell命令或shell脚本路径);

system()会调用fork()产生 子历程，由子历程来调用/bin/sh-c string来履行 参数string字符串所代表的命令，此命令履行 完后随即返回原调用的历程。在调用system()期间SIGCHLD 信号会被暂时搁置，SIGINT和SIGQUIT 信号则会被漠视 。

返回值：如果system()在调用/bin/sh时失败则返回127，其他失败原因返回-1。若参数string为空指针(NULL)，则返回非零值。 如果 system()调用成功 则最后会返回履行 shell命令后的返回值，但是此返回值也有可能为system()调用/bin/sh失败所返回的127，因 此最好能再反省 errno 来确认履行 成功 。

system命令以其简略 高效的作用得到很很广泛 的利用 ，下面是一个例子

例：在~/test/目录下有shell脚本test.sh，内容为

#!bin/bash

#test.sh

echo hello

在同层目录下新建一个c文件system_test.c，内容为：

#include<stdlib.h>

int main()

{

system("~/test/test.sh");

}

履行 效果 如下：

[root@localhost test]$gcc system_test.c -o system_test

[root@localhost test]$./system_test

hello

[root@localhost test]$

2）popen(char *command,char *type)

popen()会调用fork()产生 子历程，然后从子历程中调用/bin/sh -c来履行 参数command的指令。参数type可应用 “r”代表读取，“w”代表写入。遵循此type值，popen()会建立 管道连到子历程的标准 输出设备 或标准 输入设备 ，然后返回一个文件指针。随后历程便可利用 此文件指针来读取子历程的输出设备 或是写入到子历程的标准 输入设备 中。此外，所有应用 文 件指针(FILE*)操作的函数也都可以应用 ，除了fclose()以外。

返回值：若成功 则返回文件指针，否则返回NULL，差错 原因存于errno中。注意：在编写具SUID/SGID权限的程序时请尽量避免应用 popen()，popen()会继承环境变量，通过环境变量可能会造成系统安全的问题。

例：C程序popentest.c内容如下：

#include<stdio.h>

main

{

FILE * fp;

charbuffer[80];

fp=popen(“~/myprogram/test.sh”,”r”);

fgets(buffer,sizeof(buffer),fp);

printf(“%s”,buffer);

pclose(fp);

}

履行 效果 如下：

[root@localhost test]$ vim popentest.c

[root@localhost test]$ gcc popentest.c -o popentest

[root@localhost test]$ ./popentest

# ftok()函数(linux)

系统建立IPC通讯（如消息队列、共享内存时）必须指定一个ID值。通常情况下，该id值通过ftok函数得到。ftok原型如下：

key_t ftok( char * fname, int id )

fname就时你指定的文件名(该文件必须是存在而且可以访问的)，一般使用当前目录，如：key = ftok(".", 1); 这样就是将fname设为当前目录。id是子序号，虽然为int，但是只有8个比特被使用(0-255)。当成功执行的时候，一个key_t值将会被返回，否则 -1 被返回。在一般的UNIX实现中，是将文件的索引节点号取出，前面加上子序号得到key_t的返回值。如指定文件的索引节点号为65538，换算成16进制为 0x010002，而你指定的ID值为38，换算成16进制为0x26，则最后的key_t返回值为0x26010002。查询文件索引节点号的方法是：ls -i。在成功获取到key之后，就可以使用该key作为某种方法的进程间通信的key值，例如shmget共享内存的方式。shmget的函数原型为：int shmget( key_t, size_t, flag)。在创建成功后，就返回共享内存的描述符。在shmget中使用到的key_t就是通过ftok的方式生成的。

shmctl(shmid, IPC_RMID, 0)的作用是从系统中删除该共享存储段。因为每个共享存储段有一个连接计数(shmid_ds结构中的shm_nattch)，所以除非使用该段的最后一个进程终止与该段脱接，否则不会实际上删除该存储段

#共享内存与信号量

##共享内存

共享内存是两个或多个进程共享同一块内存区域，并通过该内存区域实现数据交换的进程间通信。虽然共享内存是进程间通信的最快速的机制，但是进程间的同步问题靠自身难以解决，于是就需要信号量机制，信号量能很好的解决互斥资源的同步问题。这些牵涉到操作系统里的知识，要好好研究一番同步互斥问题才能继续。

共享内存的工作模式一般是：

创建或取得一块共享内存

1）不指定 KEY

// IPC_PRIVATE指出需要创建内存; 

//SHM_SIZE 指出字节大小; 

//SHM_MODE 指出访问权限字如 0600表示，用户可以读写该内存

int shmget(key_t IPC_PRIVATE,size_t SHM_SIZE,int SHM_MODE);

2）指定KEY

//如果SHM_KEY指向的共享存储已经存在，则返回共享存储的ID; 

//否则，创建共享存储并返回其ID

int  shmget(key_t SHM_KEY,size_t SHM_SIZE,int SHM_MODE);

2.	void *shmat(int shmid, const void *shmaddr, int shmflg);

	将shmid所指共享内存和当前进程连接(attach)

3.	要做的事

4.	int shmdt(const void *shmaddr);

	将先前用shmat连接好的共享内存分离(detach)当前的进程

5.	int shmctl(int shmid ,int cmd, struct shmid_ds *buf)

	把cmd设成IPC_RMID删除共享内存及其数据结构

附加说明：

1.     在经过fork()后，子进程将继承已连接的共享内存地址

2.     在经过exec()后，已连接的共享内存地址会自动detach

3.     在结束进程后，已连接的共享内存地址会自动detach

##信号量

信号量对应于某一种资源，取一个非负的整型值

信号量值指的是当前可用的该资源的数量，若它等于0则意味着目前没有可用的资源

在该信号量下等待资源的进程等待队列

对信号量进行的两个原子操作：P操作和V操作。最简单的信号量是只能取0 和1 两种值，叫做二维信号量

编程步骤：

创建信号量或获得在系统已存在的信号量

调用semget()函数，不同进程使用同一个信号量键值来获得同一个信号量

int semget(key_t key, int nsems, int semflg);

控制信号量

使用semctl()函数的SETVAL操作，当使用二维信号量时，通常将信号量初始化为1，如cmd=SETVAL设置信号量的值； 或者cmd=IPC_STAT获得semid_ds结构

 int semctl(int semid, int semnum, int cmd, union semun arg);

进行信号量的PV操作

调用semop()函数，实现进程之间的同步和互斥的核心部分

如果不需要信号量，则从系统中删除它

使用semclt()函数的IPC_RMID操作，在程序中不应该出现对已被删除的信号量的操作

一个例子程序”sem_shm_1.c”，有小改动：简单的服务器和客户端程序，启动不带参数运行服务器，带参数则是客户端。服务器启动后创建信号量和共享内存，并将共享内存的引用ID显示出来，将信号量的引用ID放在共享内存中，利用服务器端提供的共享内存引用ID将共享内存附加到地址段,读取信号量以实现两个进程之间的同步,之后这两个进程就可利用共享内存进行进程间通信,客户端输入的信息将在服务器端显示出来。

# Linux下开发工具介绍

## indent

indent 实用程序是 Linux 里包含的另一个编程实用工具. 这个工具简单的说就为你的代码产生美观的缩进的格式. indent 也有很多选项来指定如何格式化你的源代码.这些选项的更多信息请看 indent 的指南页 .indent 并不改变代码的实质内容, 而只是改变代码的外观. 使它变得更可读, 这永远是一件好事.

indent是一个很有用的c源代码对齐工具。一般大家有自己喜欢的风格，可以根据需要来设定indent的风格。

indent -kr -cli4 -nut -bl4 -bli0 <filename> 

## cproto

cproto 读入 C 源程序文件并自动为每个函数产生原型申明. 用 cproto 可以在写程序时为你节省大量用来定义函数原型的时间.

## gprof

gprof 是安装在你的 Linux 系统的 /usr/bin 目录下的一个程序. 它使你能剖析你的程序从而知道程序的哪一个部分在执行时最费时间.gprof 将告诉你程序里每个函数被调用的次数和每个函数执行时所占时间的百分比. 你如果想提高你的程序性能的话这些信息非常有用.为了在你的程序上使用 gprof, 你必须在编译程序时加上 -pg 选项. 这将使程序在每次执行时产生一个叫 gmon.out 的文件. gprof 用这个文件产生剖析信息.在你运行了你的程序并产生了 gmon.out 文件后你能用下面的命令获得剖析信息:

gprof <program_name>

## hexdump

可用参数

	[-bcCdovx] [-e format_string] [-f format_file] [-n length] [-s skip] file ...

	

参数含义

	-b	单字节八进制显示，十六进制显示偏移量，每行显示16个字符，每字符用三位显示，不足补零，列间以空格分隔

	-c	单字节字符显示，十六进制显示偏移量，每行显示16个字符，每字符三位显示，不足补空格，列间以空格分隔

	-C	标准十六进制+ascii码显示，十六进制显示偏移量，每行16个字符，每字符两位显示，不足补0，结尾显示当前16位数据的ascii码值，以|框住

	-d	双字节十进制显示，十六进制显示偏移量，每行8组（16字节）每组5位，不足补零，列间以空格分隔，以无符号10进制数值显示

	-e format_string

		以指定的格式显示

	-f format_file

		根据format file中的格式进行输出，忽略formatfile中空行及以#开始的行会

	-n length

		只显示length个字节的数据

	-o	双字节八进制显示。十六进制显示偏移量，每行8组数据，每数据占两字节，6列，不足补零，以空格分隔

	-s offset

		跳过从开始的offset个字节，默认输入十进制，以0x或0X开始按16进制处理，否则如以0开始按八进制处理，如果以b/k/m结尾，则原数值乘以512/1024/1048576

	-v	显示所有数据，如果不包含这一选项，对于同上一行完全相同的数据，hexdump会以*代替显示

	-x	两位十六进制显示.十六进制显示偏移量，每行8组数据，每数据占两字节，4列，不足补零，以空格分隔

	





-e 指定格式字符串，格式字符串包含在一对单引号中，格式字符串形如：

'a/b "format1" "format2"'





每个格式字符串由三部分组成，每个由空格分隔，第一个形如a/b，b表示对每b个输入字节应用format1格式，a表示对每a个输入字节应用format2格式，一般a>b，且b只能为1，2，4，另外a可以省略，省略则a=1。format1和format2中可以使用类似printf的格式字符串，如：

%02d：两位十进制

%03x：三位十六进制

%02o：两位八进制

%c：单个字符等





还有一些特殊的用法：

%_ad：标记下一个输出字节的序号，用十进制表示

%_ax：标记下一个输出字节的序号，用十六进制表示



%_ao：标记下一个输出字节的序号，用八进制表示



%_p：对不能以常规字符显示的用.代替

同一行如果要显示多个格式字符串，则可以跟多个-e选项









例1：

输入：

hexdump -e '16/1 "%02X " "  |  "' -e '16/1 "%_p" "\n"' test  



输出：

00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F  |  ................  

10 11 12 13 14 15 16 17 18 19 1A 1B 1C 1D 1E 1F  |  ................  

20 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F  |   !"#$%&'()*+,-./  



00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F  |  ................

10 11 12 13 14 15 16 17 18 19 1A 1B 1C 1D 1E 1F  |  ................

20 21 22 23 24 25 26 27 28 29 2A 2B 2C 2D 2E 2F  |   !"#$%&'()*+,-./









例2：

输入：

hexdump -e '1/1 "0x%08_ax "' -e '8/1 "%02X " " *  "' -e '8/1 "%_p" "\n"' test  



输出：

0x00000000 00 01 02 03 04 05 06 07 *  ........  

0x00000008 08 09 0A 0B 0C 0D 0E 0F *  ........  

0x00000010 10 11 12 13 14 15 16 17 *  ........  

0x00000018 18 19 1A 1B 1C 1D 1E 1F *  ........  

0x00000020 20 21 22 23 24 25 26 27 *   !"#$%&'  

0x00000028 28 29 2A 2B 2C 2D 2E 2F *  ()*+,-./  



0x00000000 00 01 02 03 04 05 06 07 *  ........

0x00000008 08 09 0A 0B 0C 0D 0E 0F *  ........

0x00000010 10 11 12 13 14 15 16 17 *  ........

0x00000018 18 19 1A 1B 1C 1D 1E 1F *  ........

0x00000020 20 21 22 23 24 25 26 27 *   !"#$%&'

0x00000028 28 29 2A 2B 2C 2D 2E 2F *  ()*+,-./







例3：

输入：



hexdump -e '1/1 "%02_ad#    "' -e '/1 "hex = %02X * "' -e '/1 "dec = %03d | "' -e '/1 "oct = %03o"' -e '/1 " \_\n"' -n 20 test  



输出：

00#    hex = 00 * dec = 000 | oct = 000 _  

01#    hex = 01 * dec = 001 | oct = 001 _  

02#    hex = 02 * dec = 002 | oct = 002 _  

03#    hex = 03 * dec = 003 | oct = 003 _  

04#    hex = 04 * dec = 004 | oct = 004 _  

05#    hex = 05 * dec = 005 | oct = 005 _  

06#    hex = 06 * dec = 006 | oct = 006 _  

07#    hex = 07 * dec = 007 | oct = 007 _  

08#    hex = 08 * dec = 008 | oct = 010 _  

09#    hex = 09 * dec = 009 | oct = 011 _  

10#    hex = 0A * dec = 010 | oct = 012 _  

11#    hex = 0B * dec = 011 | oct = 013 _  

12#    hex = 0C * dec = 012 | oct = 014 _  

13#    hex = 0D * dec = 013 | oct = 015 _  

14#    hex = 0E * dec = 014 | oct = 016 _  

15#    hex = 0F * dec = 015 | oct = 017 _  

16#    hex = 10 * dec = 016 | oct = 020 _  

17#    hex = 11 * dec = 017 | oct = 021 _  

18#    hex = 12 * dec = 018 | oct = 022 _  

19#    hex = 13 * dec = 019 | oct = 023 _  



00#    hex = 00 * dec = 000 | oct = 000 _

01#    hex = 01 * dec = 001 | oct = 001 _

02#    hex = 02 * dec = 002 | oct = 002 _

03#    hex = 03 * dec = 003 | oct = 003 _

04#    hex = 04 * dec = 004 | oct = 004 _

05#    hex = 05 * dec = 005 | oct = 005 _

06#    hex = 06 * dec = 006 | oct = 006 _

07#    hex = 07 * dec = 007 | oct = 007 _

08#    hex = 08 * dec = 008 | oct = 010 _

09#    hex = 09 * dec = 009 | oct = 011 _

10#    hex = 0A * dec = 010 | oct = 012 _

11#    hex = 0B * dec = 011 | oct = 013 _

12#    hex = 0C * dec = 012 | oct = 014 _

13#    hex = 0D * dec = 013 | oct = 015 _

14#    hex = 0E * dec = 014 | oct = 016 _

15#    hex = 0F * dec = 015 | oct = 017 _

16#    hex = 10 * dec = 016 | oct = 020 _

17#    hex = 11 * dec = 017 | oct = 021 _

18#    hex = 12 * dec = 018 | oct = 022 _

19#    hex = 13 * dec = 019 | oct = 023 _

## GDB教程



LINUX下GDB调试 

http://blog.csdn.net/sco_field/article/details/4310987

## objdump（反汇编工具）

objdump –t

这个命令可以打印出bomb 的符号表。符号表包含了bomb中所有函数的名称和存储地址以及全局变量的名称。你可以通过查看函数名得到一些信息。

objdump –d

运用这个命令我们可以对bomb 中的代码进行反汇编。通过阅读汇编代码可以告诉你bomb 是如何运行的。虽然objdump –d 给了你很多的信息，但是它并不能告诉你所有的信息。例如：一个调用sscanf 函数的语句可能显示为：8048c36: e8 99 fc ff ff call 80488d4 <_init+0x1a0>，你还需要gdb 来帮助你确定这个语句的具体功能。

objdump打印符号表的格式：

shenyan@ubuntu:~/Temp$ objdump -t a.o

a.o:     file format elf32-i386

SYMBOL TABLE:

00000000 l    df *ABS* 00000000 a.c

00000000 l    d  .text 00000000 .text

00000000 l    d  .data 00000000 .data

00000000 l    d  .bss 00000000 .bss

00000000 l    d  .note.GNU-stack 00000000 .note.GNU-stack

00000000 l    d  .comment 00000000 .comment

00000000 g     F .text 00000005 f_test

00000005 g     F .text 00000027 main

00000000         *UND* 00000000 shared

00000000         *UND* 00000000 swap



1.段内偏移

2.符号作用域

3.符号类型：d ??；df 源文件名；F 函数名

4.符号所在段： *UND*外部链接符号，未在本目标文件定义

5.符号对应的对象占据的内存空间大小，没有实体对象大小为0，未定义的为0

6. 符号名

linux的strings命令

strings - 显示文件中的可打印字符，一般用来查看非文本文件的内容.

man strings

# strings /lib/tls/libc.so.6 | grep GLIBC

GLIBC_2.0

GLIBC_2.1

GLIBC_2.1.1

GLIBC_2.1.2

GLIBC_2.1.3

GLIBC_2.2

GLIBC_2.2.1

GLIBC_2.2.2

GLIBC_2.2.3

GLIBC_2.2.4

GLIBC_2.2.6

GLIBC_2.3

GLIBC_2.3.2

GLIBC_2.3.3

GLIBC_2.3.4

GLIBC_PRIVATE



这样就能看到glibc支持的版本。

## DevHelp 
# shell编程学习之路

3、用Shell编程，判断一文件是不是字符设备文件，如果是将其拷贝到 /dev 目录下。

参考程序：

#!/bin/sh

FILENAME=

echo “Input file name：”

read FILENAME

if [ -c "$FILENAME" ]

then

cp $FILENAME /dev

fi





7．某系统管理员需每天做一定的重复工作，请按照下列要求，编制一个解决 方案 ：

（1）在下午4 :50删除/abc目录下的全部子目录和全部文件；

（2）从早8:00～下午6:00每小时读取/xyz目录下x1文件中每行第一个域的全部数据加入到/backup目录下的bak01.txt文件内；

（3）每逢星期一下午5:50将/data目录下的所有目录和文件归档并压缩为文件：backup.tar.gz；

（4）在下午5:55将IDE接口的CD-ROM卸载（假设：CD-ROM的设备名为hdc）；

（5）在早晨8:00前开机后启动。



参考答案:

解决方案：

（1）用vi创建编辑一个名为prgx的crontab文件；

	prgx文件的内容：

50 16 * * * rm -r /abc/*



（2）、0 8-18/1 * * * cut -f1 /xyz/x1 >;>; /backup/bak01.txt

（3）、50 17 * * * tar zcvf backup.tar.gz /data

（4）、55 17 * * * umount /dev/hdc

（5）、由超级用户登录，用crontab执行 prgx文件中的内容：

root@xxx:#crontab prgx；在每日早晨8:00之前开机后即可自动启动crontab。

－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－

8．设计一个shell程序，在每月第一天备份并压缩/etc目录的所有内容，存放在/root/bak目录里，且文件名为如下形式yymmdd_etc，yy为年，mm为月，dd为日。Shell程序fileback存放在/usr/bin目录下。

参考答案：

（1）编写shell程序fileback：

#!/bin/sh

DIRNAME=`ls /root | grep bak`

if [ -z "$DIRNAME" ] ; then

mkdir /root/bak

cd /root/bak

fi

YY=`date +%y`

MM=`date +%m`

DD=`date +%d`

BACKETC=$YY$MM$DD_etc.tar.gz

tar zcvf $BACKETC /etc

echo "fileback finished!"

（2）编写任务定时器：

echo "0 0 1 * * /bin/sh /usr/bin/fileback" >; /root/etcbakcron

crontab /root/etcbakcron

或使用crontab -e 命令添加定时任务：

0 1 * * * /bin/sh /usr/bin/fileback



9．有一普通用户想在每周日凌晨零点零分定期备份/user/backup到/tmp目录下，该用户应如何做？

参考答案：（1）第一种方法：

用户应使用crontab –e 命令创建crontab文件。格式如下：

0 0 * * sun cp –r /user/backup /tmp

（2）第二种方法：

用户先在自己目录下新建文件file，文件内容如下：

0 * * sun cp –r /user/backup /tmp

然后执行 crontab file 使生效。

#五个常用的Linux监控脚本代码



为大家提供五个常用linux监控脚本(查看主机网卡流量、系统状况监控、监控主机的磁盘空间,当使用空间超过90％就通过发mail来发警告、监控CPU和内存的使用情况、全方位监控主机)，有需要的朋友不妨看看哦







1、查看主机网卡流量



#!/bin/bash

#network

#Mike.Xu

while : ; do

      time='date +%m"-"%d" "%k":"%M'

      day='date +%m"-"%d'

      rx_before='ifconfig eth0|sed -n "8"p|awk '{print $2}'|cut -c7-'

      tx_before='ifconfig eth0|sed -n "8"p|awk '{print $6}'|cut -c7-'

      sleep 2

      rx_after='ifconfig eth0|sed -n "8"p|awk '{print $2}'|cut -c7-'

      tx_after='ifconfig eth0|sed -n "8"p|awk '{print $6}'|cut -c7-'

      rx_result=$[(rx_after-rx_before)/256]

      tx_result=$[(tx_after-tx_before)/256]

      echo "$time Now_In_Speed: "$rx_result"kbps Now_OUt_Speed: "$tx_result"kbps"

      sleep 2

done

2、系统状况监控



#!/bin/sh

#systemstat.sh

#Mike.Xu

IP=192.168.1.227

top -n 2| grep "Cpu" >>./temp/cpu.txt

free -m | grep "Mem" >> ./temp/mem.txt

df -k | grep "sda1" >> ./temp/drive_sda1.txt

#df -k | grep sda2 >> ./temp/drive_sda2.txt

df -k | grep "/mnt/storage_0" >> ./temp/mnt_storage_0.txt

df -k | grep "/mnt/storage_pic" >> ./temp/mnt_storage_pic.txt

time=`date +%m"."%d" "%k":"%M`

connect=`netstat -na | grep "219.238.148.30:80" | wc -l`

echo "$time  $connect" >> ./temp/connect_count.txt

3、监控主机的磁盘空间,当使用空间超过90％就通过发mail来发警告



#!/bin/bash

#monitor available disk space

SPACE='df | sed -n '/ \ / $ / p' | gawk '{print $5}' | sed  's/%//'

if [ $SPACE -ge 90 ]

then

jbxue123@163.com

fi

4、 监控CPU和内存的使用情况



#!/bin/bash

#script  to capture system statistics

OUTFILE=/home/xu/capstats.csv

DATE='date +%m/%d/%Y'

TIME='date +%k:%m:%s'

TIMEOUT='uptime'

VMOUT='vmstat 1 2'

 USERS='echo $TIMEOUT | gawk '{print $4}' '

LOAD='echo $TIMEOUT | gawk '{print $9}' | sed "s/,//' '

FREE='echo $VMOUT | sed -n '/[0-9]/p' | sed -n '2p' | gawk '{print $4} ' '

IDLE='echo  $VMOUT | sed -n '/[0-9]/p' | sed -n '2p' |gawk '{print $15}' '

echo "$DATE,$TIME,$USERS,$LOAD,$FREE,$IDLE" >> $OUTFILE

5、全方位监控主机



#!/bin/bash

# check_xu.sh

# 0 * * * * /home/check_xu.sh



DAT="`date +%Y%m%d`"

HOUR="`date +%H`"

DIR="/home/oslog/host_${DAT}/${HOUR}"

DELAY=60

COUNT=60

# whether the responsible directory exist

if ! test -d ${DIR}

then

        /bin/mkdir -p ${DIR}

fi

# general check

export TERM=linux

/usr/bin/top -b -d ${DELAY} -n ${COUNT} > ${DIR}/top_${DAT}.log 2>&1 &

# cpu check

/usr/bin/sar -u ${DELAY} ${COUNT} > ${DIR}/cpu_${DAT}.log 2>&1 &

#/usr/bin/mpstat -P 0 ${DELAY} ${COUNT} > ${DIR}/cpu_0_${DAT}.log 2>&1 &

#/usr/bin/mpstat -P 1 ${DELAY} ${COUNT} > ${DIR}/cpu_1_${DAT}.log 2>&1 &

# memory check

/usr/bin/vmstat ${DELAY} ${COUNT} > ${DIR}/vmstat_${DAT}.log 2>&1 &

# I/O check

/usr/bin/iostat ${DELAY} ${COUNT} > ${DIR}/iostat_${DAT}.log 2>&1 &

# network check

/usr/bin/sar -n DEV ${DELAY} ${COUNT} > ${DIR}/net_${DAT}.log 2>&1 &

#/usr/bin/sar -n EDEV ${DELAY} ${COUNT} > ${DIR}/net_edev_${DAT}.log 2>&1 &

放在crontab里每小时自动执行：

0 * * * * /home/check_xu.sh

这样便会在/home/oslog/host_yyyymmdd/hh目录下生成各小时cpu、内存、网络，IO的统计数据。

如果某个时间段产生问题了，就可以去看对应的日志信息，看看当时的主机性能如何。

# shell “syntax error:unexpected end of file”

今天在写Shell时，运行时出现了这样的错误。

git-sync-tree.sh_temp: line 111: syntax error: unexpected end of file

网上Google了一下，网上都是说从windows下脚本传到Linux上可能会出现这样的问题，是因为Windows和Linux下的行末结束符是不一样的，曾经写过一篇博客：回车与换行的区别    当然，我今天遇到的不是这种情况导致的。

1. 如果确实是这种情况，在windows下写好了Shell 但是在linux下用：

sh -n [filesName]  检查语法总是出一个错误 syntax error:unexpected end of file

原因如下:

dos文件传输到unix系统时,会在每行的结尾多一个^M,在vi的时候,当你用如下命令：

vi dos.txt

:set fileformat=unix

:w

就会看到这些存在于每行结尾的^M符号，这个就是产生syntax error:unexpected end of file的原因

解决方案：

在vi下把这些^M都删除后即可。

也可以使用Linux下的工具：dos2unix也可轻松将一个windows下的文本文件转化为Unix兼容的格式。

2.我遇到的不是这样由于windows和Linux相互拷贝文件而导致的。这个是语法错误嘛，由于我这个shell脚本有点大，看了一阵子也没发现是那句话语法错误了，所以不得不用二分法来查找原因，不断注释一些代码，然后用sh -n test.sh来做语法检查，直到最后找到那一段或者哪一行代码引起的错误。我发现是下面这行代码引起的，你能看出其中的问题吗？^_^

[ -d /home/repo/${SPPATH} ] || { mkdir -p /home/repo/${SPPATH}; cd /home/repo/${SPPATH}; git init >> $GITLOG 2>&1 }

嗯，其实我用花括号{}是想把几个命令组合起来在当前shell中执行，然后我犯了一个语法错误，在最后的一个命令后没有加分号（;）。将这行改为如下即可（添加一个最后的分号）：

[ -d /home/repo/${SPPATH} ] || { mkdir -p /home/repo/${SPPATH}; cd /home/repo/${SPPATH}; git init >> $GITLOG 2>&1; }

关于当前shell中执行一组命令，特别要注意的是，在”{“的右边 和”}“的左边，至少要间隔一个以上的空格，而且每个命令都要以分号(;)作为结尾。

#怎样给变量传递执行命令结果

在linux shell脚本里，设置一个变量，但是变量是一个命令，需要将执行结果放到变量里，并输出，例如：ip='ifconfig eth0'  echo $ip，怎样可以叫页面显示的是eth0的网络状况？就是ifconfig eth0的结果？

ip=`ifconfig eth0`

echo $ip

使用反引号可以把一个命令的输出插到另一个命令中去。相同功能的写法还有$()，功能同` ` 效果是一样的。不过某些unix系统不支持$()这种写法。但是` `在任何unix或linux系统下都可以使用。

# shell 判断字符串是否存在包含关系

#! /bin/bash



var1="hello"

var2="he"



#方法1

if [ ${var1:0:2} = $var2 ]

then

    echo "1:include"

fi



#方法2

echo "$var1" |grep -q "$var2"

if [ $? -eq 0 ]

then

    echo "2:include"

fi



#方法3

echo "$var1" |grep -q "$var2" && echo "include" ||echo "not"



#方法4

[[ "${var1/$var2/}" != "$var2" ]] && echo "include" || echo "not"



其他方法：



expr或awk的index函数

${var#...}                  

${var%...}

${var/.../...}

#查看linux操作系统版本

##查看内核版本命令

jiangxin@Ubuntu:~$ cat /proc/version

Linux version 3.13.0-30-generic (buildd@allspice) (gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #54-Ubuntu SMP Mon Jun 9 22:45:01 UTC 2014

jiangxin@Ubuntu:~$ uname -r

3.13.0-30-generic

jiangxin@Ubuntu:~$ uname -a

Linux Ubuntu 3.13.0-30-generic #54-Ubuntu SMP Mon Jun 9 22:45:01 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

##查看linux版本

jiangxin@Ubuntu:~$ lsb_release -a

No LSB modules are available.

Distributor ID:	Ubuntu

Description:	Ubuntu 14.04 LTS

Release:	14.04

Codename:	trusty

jiangxin@Ubuntu:~$ cat /etc/debian_version 

jessie/sid

jiangxin@Ubuntu:~$ cat /etc/issue

Ubuntu 14.04 LTS \n \l

jiangxin@Ubuntu:~$ cat /etc/issue

Ubuntu 14.04 LTS \n \l

jiangxin@Ubuntu:~$ file /bin/bash 

/bin/bash: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=796da7aa73903b1e5608a8ff8433669b7e00e980, stripped

jiangxin@Ubuntu:~$ file /bin/cat 

/bin/cat: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=950f866ca2bc042f9ca643e1af0fde0e0c029dc3, stripped

[root@SOR_SYS ~]# cat /etc/redhat-release //Only for Redhat

Red Hat Enterprise Linux AS release 4 (Nahant Update 4)

[root@SOR_SYS ~]# rpm -q redhat-release //Only for Redhat

redhat-release-5Server-5.6.0.3

注:这种方式下可看到一个所谓的release号，比如上边的例子是5，这个release号和实际的版本之间存在一定的对应关系，如下：

redhat-release-3AS-1 -> Redhat Enterprise Linux AS 3

redhat-release-3AS-7.4 -> Redhat Enterprise Linux AS 3 Update 4

redhat-release-4AS-2 -> Redhat Enterprise Linux AS 4

redhat-release-4AS-2.4 -> Redhat Enterprise Linux AS 4 Update 1

redhat-release-4AS-3 -> Redhat Enterprise Linux AS 4 Update 2

redhat-release-4AS-4.1 -> Redhat Enterprise Linux AS 4 Update 3

redhat-release-4AS-5.5 -> Redhat Enterprise Linux AS 4 Update 4

jiangxin@Ubuntu:~$ cat /etc/debian_version //Only for Debian

jessie/sid

# C语言调试手段:锁定错误的实现方法

在项目开发工程中，如果能确定哪个文件下的哪个函数下的哪行出错--即锁定错误，那该多好啊，该文章就是为此而作的。首先来了解一下文件默认的输出信息的函数吧：



printf("line : %d\n", __LINE__);                   //当前行数

printf("filename : %s\n", __FILE__);             //当前文件名

printf("function : %s\n", __FUNCTION__);  //当前函数

printf("time : %s\n", __TIME__);                  //当前时间

printf ("date : %s\n",  __DATE__);              //当前日期



line : 10

filename : test.c

function : main.c

time : 14:13:51

date : Oct 13 2012



理论已足，那就来看看如何锁定错误吧：

一、源文件：



erroutput.c

#include <stdio.h>

#include <assert.h>

#define _DEBUG(msg...)    printf("[ %s,%s, %d ]=>",__FILE__, __FUNCTION__, __LINE__);  printf(msg);printf("\r\n")

#define _ERROR(msg...)    printf("[ error: %s, %d]=>", __FILE__,  __LINE__);printf(msg); printf("\r\n")

#define _ASSERT(exp)      \

                        do {\

                                if (!(exp)) {\

                                printf( "[ %s ]  ",#exp);printf("\r\n");\

                                assert(exp);\

                                }\

                        } while (0)

int main(void)

{

        char *p = NULL;

        _DEBUG("DEBUG!");

        _ERROR("ERROR!");

        _ASSERT(NULL != p);

        return 0;

}



二、输出：



[root@localhost for_test]# gcc erroutput.c

[root@localhost for_test]# ./a.out

[ erroutput.c,main, 17 ]=>DEBUG!

[ error: erroutput.c, 18]=>ERROR!

[ NULL != p ]

a.out: erroutput.c:19: main: Assertion `((void *)0) != p' failed.

已放弃



TI处理：

#ifdef DEBUG

    #define DBG(fmt, args...)  printf("Debug " fmt, ##args)// ##运算符用于把参数连接到一起。预处理程序把出现在##两侧的参数合并成一个符号。

#else

    #define DBG(fmt, args...)

#endif

#define ERR(fmt, args...)  printf("Error " fmt, ##args)

[root@localhost for_test]# cat debug_err.c

#include <stdio.h>

//#define DEBUG

int main(void)

{

       DBG("xxxx\n");

       ERR("xxxx\n");

       return 0;

}

[root@localhost for_test]# ./a.out

Error xxxx



#ifdef __DEBUG

    #define DBG(fmt, args...) fprintf(stderr,"Encode Debug: " fmt, ## args)

#else

    #define DBG(fmt, args...)

#endif

#define ERR(fmt, args...) fprintf(stderr,"Encode Error: " fmt, ## args)

#解决ubuntu下找不到libgtk-x11-2.0.so.0

The following error came up when I tried to run Adobe Acrobat Reader on ubuntu 12.10 

error while loading shared libraries: libgtk-x11-2.0.so.0: cannot open shared object file: No such file or directory

To fix this, simple install the package ia32-libs-gtk

$ sudo apt-get install ia32-libs-gtk

Now run the application again and the error should go away.

补充：

如果是ubuntu 14.04，则请先执行：

方法1：

sudo gedit /etc/apt/sources.list

然后在最后添加上： deb http://archive.ubuntu.com/ubuntu/ raring main restricted universe multiverse

方法2： 

echo "deb http://archive.ubuntu.com/ubuntu/ raring main restricted universe multiverse"  >>  sudo gedit /etc/apt/sources.list 

添加完源之后

sudo apt-get update

sudo apt-get install ia32-libs ia32-libs-gtk

这样就应该可以了。

# debian hosts文件中的 127.0.1.1 主机地址

有时候/etc/hosts文件会看到127.0.1.1这个地址,这是什么呢?

127.0.0.1这个loopback地址很常见，就是本地接口的回路/回环地址。但有时候/etc/hosts文件中还会出现127.0.1.1,这又是什么地址呢？这也是个本地回路/回环地址。

出现这个地址的原因是因为有些应用程序需要规范的全限定域名FQDN(Fully Qualified Domain Name)，FQDN不只需要主机名还需要主机域名，其表达形式为hostname.domainname

如果你的主机有一个静态IP地址，则FQDN名字解析到这个静态地址，否则解析到127.0.1.1这个本地回路地址。所以一般情况下不会看到127.0.1.1这个地址。

127.0.0.1一般只对应hostname，这也是二者的主要区别，如下

127.0.0.1 hostname

127.0.1.1 hostname.domainname

当然并一定非要用127.0.1.1这个IP,RFC规定的127.0.0.0/8这个IP段内的任意IP都可以，只要没有冲突，debian选择了127.0.1.1

查看主机名

# hostname

 hostname

查看FQDN名字

# hostname --fqdn

 hostname.domainname

# Linux下分割合并文 

切割合并文件在linux下用split和cat就可以完成。下面举些实例进行说明。

1.文件切割

文件切割模式分为两种：文本文件、二进制模式。

1.1文本模式

文本模式只适用于文本文件，用这种模式切割后的每个文件都是可读的。文本模式又分为两种：

按最大文件大小切割；

按文本行数切割。

1.1.1最大文件大小切割

split -C 5k duanxin split

将文本文件duanxin按每块最大5k的大小进行切割，不打碎行。输出文件名类似splitaa, splitab……

split -b 5k duanxin split

每个分块（当然，最后一个不保证）大小都是5k，可能会打碎行。

1.1.2 按文本行数切割

split -l 100 duanxin split

每个分块100行，不考虑大小。日志分析时应该有用。

1.2 二进制模式

split -b 5k duanxin split

每个分块（当然，最后一个不保证）大小都是5k，基本不可读。任何类型文件都可以用这种切割模式。

2.文件合并

cat split* >newduanxin

不管用什么方式切割，合并方法不变。

3.其它

split可以用-a选项指定输出文件名的长度。如

split -l 100 -a 3 duanxin split

则输出文件出类似于splitaaa,splitaab。不指定时默认为2。

用-b或-C指定分块大小时，可用的单位有，b for 512bytes, k for 1Kbytes, m for 1 Megbytes.

split 参数：

-a, --suffix-length=N   指定输出文件名的后缀，默认为2个

-b, --bytes=SIZE        指定输出文件的字节数

-C, --line-bytes=SIZE  每一输出档中，单行的最大 byte 数

-d, --numeric-suffixes  使用数字代替字母做后缀

-l, --lines=NUMBER    NUMBER 值为每一输出档的列数大小

# ubuntu下终端路径只显示当前目录

最近一直在用终端操作，看着他长长的路径名实在不爽， 动手来改改咯～

$: sudo vim ~/.bashrc

这个文件记录了用户终端配置

找到

if [ "$color_prompt " = yes ]; then

    PS1 ='{debian_chroot:+(debian_chroot)}

\033[01;32m

\u@\h

\033[00m

:

\033[01;34m

\W 

\033[00m

\$ '

else

    PS1 ='{debian_chroot:+(debian_chroot)}\u@\h:\W \$ '

 将蓝色的w由小写改成大写，可以表示只显示当前目录名称.

# ubuntu终端颜色消失的问题

ubuntukylin 13.10    ls后终端显示的所有输出都是黑底白字，没有彩色，用su后ls却有彩色 

echo $PS1  输出二者也有差异，一看发现用户目录下.bashrc没有，  

cp /etc/skel/.bashrc  ~/ 

后问题解决，如果要改颜色配置，可以修改PS1的值。 

#通过find命令寻找文件并拷贝到指定目录

有这样的一个需求，需要将一部分符合条件的文件从一个目录拷贝到另一个目录中，可以通过使用find命令从源目录查找到符合条件的文件然后使用cp命令拷贝到目标目录

方法一 

命令如下： 

find src_dir -name "access.log.2011102[2-6]*" -exec cp {} dst_dir \; 

拷贝文件到远程主机上的目标目录的命令： 

find src_dir -name "access.log.2011102[2-6]*" -exec scp {} 用户名@主机ip:dst_dir \; 

方法二 

find src_dir -name "access.log.2011102[2-6]*" |xargs -i cp {} dst_dir 

或 

find src_dir -name "access.log.2011102[2-6]*" |xargs -I {} cp {} dst_dir 

拷贝文件到远程主机上的目标目录的命令： 

find src_dir -name "access.log.2011102[2-6]*" |xargs -i scp {} 用户名@主机ip:dst_dir 

或 

find src_dir -name "access.log.2011102[2-6]*" |xargs -I {} scp {} 用户名@主机ip:dst_dir 

src_dir 源目录 

dst_dir 目标目录 

access.log.2011102[2-6]* 文件名的正则表达式，获取文件的条件 

方法三 

find命令结合cp命令，拷贝某个目录下所有文件到另一个目录中 



要求整个目录完全拷贝到另一个目录，并且忽略个别目录，脚本如下： 

find ./ -path '/tmp/mnt/disk1/ignore' -prune -o \( -name '*' ! -name "*.tmp" \) | xargs cp "目的目录" "{}" \;



在上面这个脚本中，当执行到“| xargs cp”时，假设输入的字符串类似如下： 

/tmp/mnt/disk1/tt.txt 

/tmp/mnt/disk1/test/dd.txt 



要求执行“xargs cp”后，相应拷贝成如下的目录结构 

(即：原来disk1目录下所有文件都拷贝到src目录下，目录结构不变)： 

/tmp/mnt/src/tt.txt 

/tmp/mnt/src/test/dd.txt

# ubuntu登录输入用户名密码后重新跳回登录界面

现象：在Ubuntu 14.04登陆界面输入密码之后，黑屏一闪后，又跳转到登录界面。

原因：主目录下的.Xauthority文件拥有者变成了root，从而以用户登陆的时候无法都取.Xauthority文件。

说明：Xauthority，是startx脚本记录文件。Xserver启动时，读文件~/.Xauthority,读入对应其display的记录。当一个需要显示的客户程序启动调用XOpenDisplay()也读这个文 件，并把找到的magic code 发送给Xserver。

当Xserver验证这个magic code正确以后，就同意连接啦。观察startx脚本也可以看到，每次startx运行，都在调用xinit以前使用了xauth的add命令添加了一个新的记录到~/.Xauthority，用来这次运行X使用认证

解决方法：我们需要将.Xauthority的拥有者改为登陆用户（或者干脆将.Xauthority删除，此法转自网上，本人未验证）

开机后在登陆界面按下shift + ctrl + F1进入tty命令行终端登陆后输入： 

$ cd ~

$ sudo chown groupname:username .Xauthority

然后再次输入：

ls .Xauthority -l

成功后显示如下：

-rw------- 1 hp hp 80 1月 27 10:41 .Xauthority

此时拥有者已经变为用户。按下shift + ctrl + F7切换回图形登陆界面登陆即可。

# watchdog

Linux 自带了一个 watchdog 的实现，用于监视系统的运行，包括一个内核 watchdog module 和一个用户空间的 watchdog 程序。内核 watchdog 模块通过 /dev/watchdog 这个字符设备与用户空间通信。用户空间程序一旦打开 /dev/watchdog 设备（俗称“开门放狗”），就会导致在内核中启动一个1分钟的定时器（系统默认时间），此后，用户空间程序需要保证在1分钟之内向这个设备写入数据（俗称“定期喂狗”），每次写操作会导致重新设定定时器。如果用户空间程序在1分钟之内没有写操作，定时器到期会导致一次系统

reboot 操作（“狗咬人了”呵呵）。通过这种机制，我们可以保证系统核心进程大部分时间都处于运行状态，即使特定情形下进程崩溃，因无法正常定时“喂狗”，Linux系统在看门狗作用下重新启动（reboot），核心进程又运行起来了。多用于嵌入式系统。



打开 /dev/watchdog 设备（“开门放狗”）：



int fd_watchdog = open("/dev/watchdog", O_WRONLY);

if(fd_watchdog == -1) {

	int err = errno;

	printf("\n!!! FAILED to open /dev/watchdog, errno: %d, %s\n", err, strerror(err));

	syslog(LOG_WARNING, "FAILED to open /dev/watchdog, errno: %d, %s", err, strerror(err));

}

每隔一段时间向 /dev/watchdog 设备写入数据（“定期喂狗”）：



//feed the watchdog

if(fd_watchdog >= 0) {

	static unsigned char food = 0;

	ssize_t eaten = write(fd_watchdog, &food, 1);

	if(eaten != 1) {

		puts("\n!!! FAILED feeding watchdog");

		syslog(LOG_WARNING, "FAILED feeding watchdog");

	}

}

关闭 /dev/watchdog 设备，通常不需要这个步骤：



close(fd_watchdog);

所需头文件：



#include <unistd.h>

#include <sys/stat.h>

#include <syslog.h>

#include <errno.h>

# tailf

tailf命令几乎等同于tail -f，严格说来应该与tail --follow=name更相似些。当文件改名之后它也能继续跟踪，特别适合于日志文件的跟踪。与tail -f不同的是，如果文件不增长，它不会去访问磁盘文件，这样带来的好处是如果没有新的日志产生，日志文件的时间戳(access time)就不会改变。tailf特别适合那些便携机上跟踪日志文件，因为它能省电，因为减少了磁盘访问嘛。

格式：tailf logfile

动态跟踪日志文件logfile，最初的时候打印文件的最后10行内容。

Ctrl+C 停止

# vimrc，bashrc中rc的含义

rc (像是 ".cshrc" 或 "/etc/rc" 中的 rc 这两个字母) = "RunCom" 

"rc" 是取自 "runcom", 来自麻省理工学院在 1965 年发展的 CTSS系统。相关文献曾记载这一段话: '具有从档案中取出一系列命令来执行的功能；这称为 "run commands" 又称为 "runcom"，而这种档案又称为一个 runcom (a runcom)。' 

Brian Kernighan 与 Dennis Ritchie 告诉 Vicki Brown 说: "rc" 也是Plan 9 作业系统 shell 的名字。

#.cshrc文件是干什么用的?

这个是个隐藏文件  ，在你使用的用户家目录下的

是csh 这个shell(csh)的配置文件，你对csh的更改都会记录在这个文件中，下次你再启动csh的时候会读取这个文件。

# There are unfinished transactions remaining

今天在服务器用yum安装东西的时候,老是报:There are unfinished transactions remaining. You might consider running yum-complete-transaction first to finish them.意思是:有未完成的yum事务,建议先运行yum-complete-transaction命令清除.问了下开发,原来有强制结束yum过,好吧,对于我这样有点轻微强迫症的人来说,不允许服务器出现这些信息的.

解决办法:

代码如下:

# 安装 yum-complete-transaction（这是一个能发现未完成或被中断的yum事务的程序）

yum -y install yum-utils

# 清除yum缓存

yum clean all

# 运行 yum-complete-transaction,清理未完成事务

yum-complete-transaction --cleanup-only

ps:

yum会把下载的软件包和header存储在cache中,而不会自动删除.可用yum clean headers清除header,yum clean packages清除下载的rpm包,yum clean all全清.

# yum提示another app is currently holding the yum lock;waiting for it to exit

可能是系统自动升级正在运行，yum在锁定状态中。

可以通过强制关掉yum进程：

#rm -f /var/run/yum.pid

然后就可以使用yum了。

#杂项

GTK+2.0编程范例作者宋国伟邮箱：

gwsong52@sohu.com

待解决问题：

G_CALLBACK()与  GTK_SIGNAL_FUNC()区别

# shell编程讲义

## 【1】SHELL范式

规定一个范式，有利于统一程序风格，增加可读性。对于编写SHELL，拷贝修改即可。

范式:

ASSIGN SHELL/指定壳

DESCRIPTION/程序说明

BODY/程序体

扩展：

1 ASSIGN SHELL/指定壳，如果不指定壳，默认使用Bourne SHELL，建议使用KSH

#!SHELL路径

1.1	 CSH
1.2	
#!/bin/csh

1.3	 BSH
1.4	
#!/bin/sh

1.5	 KSH
1.6	
#!/bin/ksh



2 DESCRIPTION/程序说明

#PROCEDURE NAME/程序名称

#PROCEDURE FUNCTION/程序功能说明

#AUTHOR/作者

#DATE/开发时间

#INPUT/输入

#OUTPUT/输出

#CALL/调用函数说明

#HISTORY/变更历史



3 BODY/程序体

INCLUDE LIBRARY /包含库文件

VARIABLE DEFINE/变量定义

FUNCTION DEFINE/函数定义

MAIN/程序入口

3.1 INCLUDE LIBRARY /包含库文件

. LIBRARY FILE/库文件名称

3.2 FUNCTION DEFINE/函数定义

#FUNCRION: FUNCTION NAME

#DESC    : FUNCTION DESC

#INPUT   : INPUT DESC

#OUTPUT  : OUTPUT DESC

FUNCTION()

{



}

3.3 MAIN/程序入口(建议为)

程序启动说明

程序执行步骤

程序结束

exit 0



范式样例：

#!/bin/ksh

 

#################################################################################

# 程序名  ： update.sh							        					#

# 功能简介： 本程序完成********升级								#

# 作者    :  *********0                                                     #

# 开发时间： 2002-05-05   												#

#	     															#

# 函数说明： 函数定义													#

#	        CheckBackupDir()	检查备分目录，不完毕则创建					#

#	        CheckDbinstallDir()	检查SMP的数据库安装脚本目录					#

#            CheckIfUpgraded()	检查是否已经升级							#

#	        UpdateSMPDir()		升级SMP的目录结构							#

#            BackupDb()			备分数据库的脚本、数据						#

#            BackupFile()		备分SMP目录的文件							#

#            UpdateDb()			升级数据库                         		     #

#            UpdateFile()		升级文件 	                	    		 	     #

#																	#

# 修改历史： First Programming			   								#

# 日期    ：															#

# 作者	  ：															#

# 修改说明：															#

#################################################################################



#应用库函数，要求库函数文件与当前SHELL同一目录

. ./comm_func.sh.rc



#定义变量

#程序名称

ProgName="SMP Platform Upgrade"



#标题

Title="WINV200R002 D039P2"



#目录和文件定义

WorkDir=`pwd`

LogDir=$WorkDir/log

TempDir=$WorkDir/temp



#日志与标志文件

ErrFile=$LogDir/update.err

LogFile=$LogDir/update.log

FlagFile=$LogDir/flag.flg



########################函数定义####################################



####################################################################

# 函数：PrintUsage

# 目的：定义打印用法函数。

# 输入：

# 输出：屏幕

####################################################################

PrintUsage()

{

    echo "***************************************************************"

    echo "      NAME : ${ProgName}                                     "

    echo "   VERSION : ${Title}                                        "

    echo "    SYSTEM : WIN SMP                                         "

    echo "      DESC : SMP platform or service upgrade                 "

    echo "    NOTICE :                                                 "

    echo " COPYRIGHT : 2002, HUAWEI Tech. Co. Ltd.                     "

    echo "***************************************************************"

    echo " 1. Execute backup operation"

    echo " 2. Execute upgrade operation"

    echo " 3. Execute rollback operation"    

    echo " 0. Exit"

    echo "Please input operation choice [0-3]:"

}

…

###########               Main            ##############

…

exit 0

#####################  END OF PROCEDURE  ###############



##【2】SHELL编程语法

Script是以行为单位，我们所写的Script会被分解成一行一行来执行。而每一行可以是命令、注解、或是流程控制指令等。如果某一行尚未完成，在行末加上"\" ，这个时候下一行的内容就会接到这一行的後面，成为同一行。



当Script中出现"#"时，再它後面的同一行文字即为注解，Shell会对其翻译。 在Script中要执行一个命令的方法和在命令列中一样，你可以前台或后台执行，执行命令时也会需要设定一些环境变量。 



Script的流程控制和一般高级语言的流程控制没有什麽两样，也和高级语言一样有副程式。这些使得Script的功能更加强大。 



1 SHELL基本术语与关键字

.            	当前shell程序相同目录

..            	当前shell程序的上一级目录

break    		退出for、while、until或case语句

cd          		改变到当前目录

continue 		执行循环的下一步

echo       		反馈信息到标准输出

eval        		读取参数，执行结果命令

exec       		执行命令，但不在当前shell

exit         	退出当前shell

export    		导出变量，使当前shell可利用它

pwd        		显示当前目录

read       		从标准输入读取一行文本

readonly 		使变量只读

return     		退出函数并带有返回值

set         		控制各种参数到标准输出的显示

shift       		命令行参数向左偏移一个

test         	评估条件表达式

times      		显示shell运行过程的用户和系统时间

trap       		当捕获信号时运行指定命令

ulimit    		显示或设置shell资源

umask     		显示或设置缺省文件创建模式

unset  			从shell内存中删除变量或函数

wait       		等待直到子进程运行完毕，报告终止



2变量

Shell的类型只有字串变量，所以要使用数值运算则必须靠外部命令达成目的。而其变量种类有下列几种： 

2.1 普通变量 

这是最常使用的变量，我们可以任何不包含空白字元的字串来当做变量名称。 设定变量值时则用下列方式： 

var=string   #不能是var = string，即等号两边不能有空格。与判断语句正好相反，判断语句表的=或者其他符号两边必须有空格，否则为赋值运算

取用变量时则在变量名称前加上一"$" 号，或者${name}。 

name=Tom 

echo name

echo $name 

结果如下：

name

Tom



2.2环境变量

和使普通变量相似，只不过此种变量会将其值传给其所执行的命令。要将一使 用者变量设定为系统变量，只要加上： 

export var或者export var=var_value 或者setenv var var_valued

name=Tom

export name



以下是使用者一进入系统之後就已设定好的系统变量： 

$HOME 使用者自己的目录 

$PATH 执行命令时所搜寻的目录 

$TZ 时区 

$MAILCHECK 每隔多少秒检查是否有新的信件 

$PS1 在命令列时的提示号 

$PS2 当命令尚未打完时，Shell要求再输入时的提示号 

$MANPATH man 指令的搜寻路径 



2.3 只读的使用者变量 

和使用者变量相似，只不过这些变量不能被改变。要将变量设成只读的 ，只要加上： 

readonly var 



而若只打readonly则会列出所有只读的变量（ksh支持readonly命令。csh不支持，但是在shell程序中可以使用readonly修饰某个变量）。还有一点，系统变量不可以设定成只读的。 

name=Tom 

readonly name

echo $name

name=John

echo $name

(假设文件保存为aa)

结果如下：

aaa

aa[4]: name: This variable is read only



2.4 特殊变量 

有些变量是一开始执行Script时就会设定，并且不以加以修改，但我们不叫它只读的系统变量，而叫它特殊变量，因为这些变量是一执行程式时就有了，况且使用者无法将一般的系统变量设定成只读的。以下是一些等殊变量：

$0 这个程式的执行名字 

$n 这个程式的第n个参数值，n=1..9 

$* 这个程式的所有参数 

$# 这个程式的参数个数 

$$ 这个程式的PID 

$! 执行上一个背景指令的PID 

$? 执行上一个指令的返回值 



$n，n只能为0-9的原因，是Bourne Shell的位置参数变量为$1~$9, 因此通过位置变量$n只能访问前9个参数。当你执行这个程式时的参数数目超过9 时，我们可以使用shift 命令将参数往前移一格，如此即可使用第10个以後的参数。除此之外，可以用set 命令改变$n及$*，方法如下： 

set string 



如此$*的值即为string，而分解後则会放入$n。如果set命令後面没有参数， 则会列出所有已经设定的变量以及其值。 

echo Filename: $0

echo Arguments: $*

echo No. of args.: $# 

echo 2nd arg.: $2 

shift 

echo No. of args.: $#

echo 2nd arg.: $2 

set hello, everyone 

echo Arguments: $* 

echo 2nd arg.: $2 



结果如下：

Filename: ex1

Arguments: this is a test

No. of args.: 4

2nd arg.: is

No. of args.: 3

2nd arg.: a

Arguments: hello, everyone

2nd arg.: everyone



2.5 数组变量 （ksh支持）

name[index]=value

其中name为数组名称,index为数组下标，在ksh中数组最大支持1024,即index为0~1023.

或者

set –A name value1 value2…valuen

引用数组变量

${name[index]}

应用所有项：

${name[*]}    #或者

${name[@]}



如：

set –A ser pps ppip mvpn

echo ${ser[2]}

echo ${ser[*]}

打印为：

mvpn

pps ppip mvpn



如：

set –A ser pps ppip mvpn

echo $ser[2]

echo $ser[*]

打印为：

pps[2]

pps[*]



2.6 SHELL变量 

SHELL程序中可以直接使用一些变量。常用有：

SECONDS			#ftp程序中判断超时经常使用这个变量

IFS				#域分割符，缺省为空格或者TAB键，可以由用户指定



3引用

某些字符在SHELL中具备特殊的含义：

如：& * + ^ $ ` " | ? [ ] ; ^ < >

可以使用双引号或者单引号或者\去掉特殊字符的含义，使成为一个普通字符.

3.1	 ””可以去掉除$, \, ``之外的所有特殊字符的含义。
3.2	
比如：

>echo *    		#输出当前某个的所有目录与文件

>echo “*”		#输出*字符

>echo “`date`”	#输出为date命令打印的时间“Tue Sep 17 11:31:58 MDT 2002”

>echo “$PATH”	#输出当前用户的搜索路径

>echo “a\na”		#输出为2行，一行一个a，此时\为特殊字符

3.3	 ‘’单引号可以去掉\去掉引号以内包含的任何特殊字符的含义，使成为一个普通字符.
3.4	
比如：

>echo ‘*’		#输出*字符

>echo ‘`date`’	#输出`date`

>echo ‘$PATH’	#输出$PATH

>echo ‘a\na’		#输出为2行，一行一个a，此时\为特殊字符



3.5	 \可以去掉& * + ^ $ ` " | ?的特殊含义，\本身的特殊含义可以用\去掉，比如\\后面一个\就是普通字符
3.6	
如：

>echo \*			#输出*



4标准输入与输出

当我们在shell中执行命令的时候，每个进程都和三个打开的文件相联系，并使用文件描述符来引用这些文件。由于文件描述符不容易记忆， shell同时也给出了相应的文件名。下面就是这些文件描述符及它们通常所对应的文件名：

文件文件描述符

输入文件—标准输入0

输出文件—标准输出1

错误输出文件—标准错误2

系统中实际上有1 2个文件描述符，但是正如我们在上表中所看到的， 0、1、2是标准输入、输出和错误



command > filename 把把标准输出重定向到一个新文件中

command >> filename 把把标准输出重定向到一个文件中(追加)

command 1 > fielname 把把标准输出重定向到一个文件中

command > filename 2>&1 把把标准输出和标准错误一起重定向到一个文件中

command 2 > filename 把把标准错误重定向到一个文件中

command 2 >> filename 把把标准输出重定向到一个文件中(追加)

command >> filename 2>&1 把把标准输出和标准错误一起重定向到一个文件中(追加)

command < filename >filename2 把command命令以filename文件作为标准输入，以filename2文件作为标准输出

command < filename 把c o m m a n d命令以f i l e n a m e文件作为标准输入

command << delimiter 把从标准输入中读入，直至遇到d e l i m i t e r分界符

command <&m 把把文件描述符m作为标准输入

command >&m 把把标准输出重定向到文件描述符m中

command <&- 把关闭标准输入



比如常用dbaccess执行一个SQL串：

>dbaccess $TELLIN_DBNAME <<EOF >$errorfile 2>&1

delete from basetab_pps where msisdn=’13000000000’

EOF



5重新定向

输入定向：可以从文件或者标准输入设备得到输入

<

输出定向：

>	#将命令的屏幕输出定向到文件

>>  #将命令的屏幕输出定向到文件，采用Append方式

管道定向：

| 	#将一个命令的输出定向到另外一个命令的输出（某些命令不支持直接|定向）

如：将一条SQL输出到dbaccess执行

>echo “update basetab_pps set multiserviceflag=’00000000000” where msisdn=’13501300000”|dbaccess $TELLIN_DBNAME

>ps –ef |grep “manager” |grep –v “grep” | wc –l   #多次管道定向



得到命令返回值，输出到变量：

var=`command`

如：

>echo Time=`date "+%y-%m-%d %H:%M:%S"`		#输出Time=02-09-17 18:30:06



6基本流程语句

6.1 顺序

6.2 条件语句if-then-fi

if  condition 

then

   ...

fi



我们经常使用的书写方式：使用;符号，在一行中包含多条命令与语句

if  condition  ；then

   ...

fi



6.3 条件语句if-then-else-fi

If  condition 

then

   ...

else

   ...

fi

        

if condition1

then

   ...

elif condition2

then

   ...

else

   ...

fi

      

6.4 while条件循环

while express

do

   ...

done 

#从循环中退出使用 break和continue命令

      

6.5 for循环

for var in arg1 arg2 ... argn

do 

  ...

done

#从循环中退出使用 break和continue命令



6.6 until循环

until express

do

...



done

#从循环中退出使用 break和continue命令

      

6.7 case选择语句

case var in

var1) 

    ...

    ;;

var2|var3) 

    ...

    ;;

*)

    ;;

esac

             

如升级程序选择菜单就是利用case建立的：

while true

do

     #执行

     echo ""

     if [ "-${OprChc}" = "-1" ]; then

               Backup   #备份

     elif [ "-${OprChc}" = "-2" ]; then

               Upgrade  #升级

     elif [ "-${OprChc}" = "-3" ]; then

               Rollback #回滚       

     elif [ "-${OprChc}" = "-0" ]; then

               Log "Goodbye!"

               Log ""

               break        

     else

               echo "Invalid input , please input again!"

     fi

            

      echo ""

      PrintUsage  

      read OprChc

done  



6.8 select选择语句(ksh支持)

select选择语句一般与case语句联合使用，用户生成用户交互菜单。语法为：

select var in value1 value2 value3 … valuen

do

   …

done

select执行时会根据value项生成一个列表，并且每一项之前给一个从1开始递增的数字。用户选择某个数字，相当于选择value对应项，赋值给var变量。如：

1)	value1
2)	
3)	value2
4)	
5)	value3
6)	
…

n)	valuen
o)	
#?



一般do done之间使用case语句。语法扩展为：

select var in value1 value2 value3 … valuen

do

   case $var in

      value1)

         …

         ;;

      value2)

         …

         ;;

      value3)

         …

         ;;

      …

      valuen)

         …

         ;;

      *)

   esac

done



7 比较操作

比较操作一般用在条件判断中，以下语法使用条件判断为例：

7.1 字符串比较

1）字符串相等比较

if [ $str = “value” ]; then        #注意等号两边比较有空格，否则为赋值运算

…

fi



2）字符串是否为空

if [ “-$str” = “-” ]; then         #-没有任何含义，只是为了增加可读性

…

fi



if [ “X$str” = “X” ]; then         #X没有任何含义，只是为了增加可读性

…

fi



3）字符串不相等比较

if [ $str != “value” ]; then       #注意等号两边比较有空格，否则为赋值运算

…

fi



if [ ! $str = “value” ]; then      #！为not的含义，即取反

…

fi



7.2 数字比较

1）大于、大于等于

if [ $str -gt 100 ]; then        #-gt表示大于

…

fi



if [ $str -ge 100 ]; then        #-ge表示大于等于

…

fi



2）小于、小于等于

if [ $str -lt 100 ]; then        #-lt表示小于

…

fi



if [ $str -le 100 ]; then        #-le表示小于等于

…

fi



2）等于、不等于

if [ $str –eq 100 ]; then        #-eq表示等于

…

fi



if [ $str -ne 100 ]; then        #-ne表示不等于

…

fi



if [ ! $str -eq 100 ]; then        #!表示取否，-eq表示等于

…

fi



7.3 判断条件连接

1）与/and，即要求表达式1与表达式2同时为真

if express1 && express 2 ;           #&&表示与/and含义 -a

then

…

fi



if [ str1 = “aa” ] && [ str2 = “bb” ] ;     

then

…

fi





2）或/or，即要求表达式1或者表达式2之一为真

if express1 || express 2 ;             #||表示或/or含义 -o

then

…

fi



if [ str1 = “aa” ] || [ str2 = “bb” ] ;     

then

…

fi



3）取反，

if ! express1 ;                    #！表示去反

then

…

fi



if [ ! $? –eq 0 ]; 

then

…

fi





8 SHELL函数



可以将SHELL中需要重复执行的代码写成函数，与C编程的函数一致。

8.1 函数格式

定义函数的格式为：

函数名（）

{

   ...

}

或者

函数名（）{

   ...

}

两者方式都可行。如果愿意，可在函数名前加上关键字function，建议增加。

function 函数名（）

{

 ...

}



8.2 向函数传入参数

函数可以带参数调用，调用方式为

函数名称  参数列表



函数取得传入的参数，与SHELL得到调用的参数完全一致：

判断参数个数：

$#

取参数：

$1  $2 …



8.3	 函数返回参数
8.4	
函数可以使用return 返回调用参一个值。调用者可以在调用函数后得到函数的返回值：

$?得到,如：

#调用格式：aaa  parameter

aaa()

{

   return 1

}



#错误用法

a=`aaa para`   #无法得到返回值1



#正确用法

aaa para

ret=$?



如果使用exit，将退出SHELL程序



8.5	 将常用函数写成库函数
8.6	
为了重复利用代码，可以将函数写成库函数的方式，然后在SHELL中包含进行即可使用：

. libraryfile



9其他基本语法

9.1 条件连接符

and与 

命令行：command1 && command2   #如果command1执行成功，执行commnad2

如：rm * && echo "File successfully removed"

(建议不要使用以上语法，因为语法不常用，可读性不强)

表达式：express1 && express2

如：if [ $1 -eq 1 ] && [ $1 -eq 1 ]

    then

       ...

    fi



or或

命令行：command1 || command2    #仅当前一个命令执行出错时才执行后一条命令

如：rm * || echo "File removed failed"

(建议不要使用以上语法，因为语法不常用，可读性不强)

表达式：express1 || express2

如：if [ $1 -eq 1 ] || [ $1 -eq 1 ]

    then

       ...

    fi



9.2 包含库函数

#. 空格之后将文件的路径， 一般放在程序的起始部分

. ./comm_func.sh.rc



9.3 信号处理

trap "echo ___ $0 interrupted ___; exit 1" 2



9.4 分割符

SHELL默认的分割符IFS为空格与TAB键。程序中可以使用定制的分割符

如：从dbaccess下载数据没有指定delimiter时，字段分割为”|”

OLD_IFS=$IFS

IFS=”|”

Read col1 col2 col3 < datafile

…

IFS=$OLD_IFS



9.5终端的一些知识

1） 使字符显示方式正常或者反转显示

echo “\033[m\c”    #正常显示

echo “\033[7m\c”   #反转显示



2）设置图形模式或者字符模式

echo “\033(B\c”    #字符模式

echo “\033(0\c”    #图形模式



3）从终端得到一个字符

TTY=`tty`

$1='`dd if=$TTY bs=1 count=1 2>/dev/null`'



4）定位光标位置

echo "\033[$1;$2H\c"   #其中$1表示行，$2表示列



5) 设置终端参数

stty可以用来设置与限制终端属性，如：终端与计算机之间的传输率、退格、中断等。

echo[-echo]   	是否回显

intr				生成中断信号，默认使用del按键生成

erase			退格键，即擦除前面一个字符

##【3】常用概念命令与操作

1文件

1.1 文件类型，ls –al 中第一列的第一个字符：

drwxr-xr-x  12 smp20      sms           1024 Aug 13 15:36 .dt

d 目录。

l 符号链接(指向另一个文件)。

s 套接字文件。

b 块设备文件。比如informix操作的存储文件为块设备

c 字符设备文件。比如/dev/null空设备

p 命名管道文件。即进程通信使用的PIPE文件

- 普通文件，或者更准确地说，不属于以上几种类型的文件



1.2 文件权限，ls –al 中第一列的第2-10个字符

(2-4字符)	文件属主的权限

(5-7字符) 	同组用户的权限

(8-10字符) 	其他用户的权限



1.3 改变权限位

chmod命令的一般格式为：

chmod [who] operator [permission] filename

who的含义是：

u 文件属主权限。

g 同组用户权限。

o 其他用户权限。

a 所有用户(文件属主、同组用户及其他用户)。

operator的含义：

+ 增加权限。

- 取消权限。

= 设定权限。

permission的含义：

r 读权限。

w 写权限。

x 执行权限。

s 文件属主和组set-ID。

t 粘性位*。

l 给文件加锁，使其他用户无法访问。

或者：

chmod 权限值 filename

文件属主		同组用户		其他用户

rwx			rwx			rwx

4+2+1 		4+2+1 		4+2+1



1.4 目录权限位

目录的读权限位意味着可以列出其中的内容。写权限位意味着可以在该目录中创建文件，如果不希望其他用户在你的目录中创建文件，可以取消相应的写权限位。执行权限位则意味着搜索和访问该目录



1.5 改变文件的属主

chown命令的一般形式为：

chown -R -h owner file

-	R选项意味着对所有子目录下的文件也都进行同样的操作。- h选项意味着在改变符号链接文件的属主时不影响该链接所指向的目标文件。一旦将文件的所有权交给另外一个用户，就无法再重新收回它的所有权
-	


1.6 umask

umask命令确定了你创建文件的缺省模式。这一命令实际上和chmod命令正好相反

umask命令是在/etc/profile文件中设置的，每个用户在登录时都会引用这个文件，所以如果希望改变所有用户的umask，可以在该文件中加入相应的条目。如果希望永久性地设置自己的umask值，那么就把它放在自己$HOME目录下的. profile或.bash_profile文件中。

对于SMP或者SCP，我们定义在.cshrc中，这样登陆即生效。如：umask 002，这样创建的文件的权限为777-002=775



1.7 判断文件某些特性

-r file   #是否存在并且可读

-w file   #是否存在并且可写

-s file   #是否存在并且文件大小大于0

-f file   #是否存在并且是规则文件

-d file   #是否存在并且为目录

-x file   #是否存在并且可以执行

-p file   #是否存在并且为管道文件



1.8 文件记录循环处理

使用while循环读取文件记录进行处理。其中文件输入采用 < 定向符。循环表达式为read命令，语法如下：

while read var1 var2 …

do

    #处理代码

done < filename



其中：

1一次读取一行数据。

2 可以将文件中一行数据以空格或者TAB键格开的域（字段）内容读入变量。如果变量数量小于域（字段）数量，则将前面部分一一对应，最后剩余域的所有内容读入最后一个变量。比如：

行：AAA BBB CCC

while read var1 var2 

do

done

则var1=’AAA’, var2=’BBB CCC’

2	如果想使用其他字符间隔域（字段），可以修改IFS得到，比如：修改为|
3	
OLD_IFS=$IFS

IFS=|

while read var1 var2..

do 

done



#恢复IFS原内容

IFS=$OLD_IFS





2数值操作

可以使用:expr或者bc命令，KSH可以使用let

使用 expr 应用程序

2.1	expr
2.2	
n1=3

n2=5

n=`expr $n1 + $n2 `  

注意：+等操作符2侧需要使用空格格开



如：

>expr 10000 + 1111    #相加

>expr 10000 \* 1111   #相乘



ksh 中可使用 let

n1=3

n2=5

let n=n1+n2



2.2 bc

使用bc可以计算任意长度的计算，不会溢出

>echo "1000000000000000000000000000000*1111" | bc

111100000000000000000000000000000



2.3 进制转换

可使用printf命令转换

比如：16 to 10

     十六进制数前加“0x"

     test1=`printf "%d" 0x9d83000`



 比如：10 to 16

     test2=`printf "%x" 83000



3合并与分割

常用的合并与分割命令有：

? sort

? cut

? split



3.1	 sort排序
3.2	
sort -cmur -o 输出文件 –t 分割符 +n 输入文件

下面简要介绍一下s o r t的参数：

-c 测试文件是否已经分类。

-m 合并两个分类文件。

-u 删除所有复制行。

-r 逆向排序DESC，默认为正向ASC



如：将basetab_pps文件按第4个字段逆向排序

sort –t\| -r +3 basetab_pps.unl > basetab_pps.unl.sort

注意：不能使用-t|，因为|在SHELL中属于管道符号，需要使用\|



3.3	 cut切割
3.4	
cut用来从标准输入或文本文件中剪切列或域。剪切文本可以将之粘贴到一个文本文件。

下一节将介绍粘贴用法。

cut一般格式为：

cut [options] file1 file2

下面介绍其可用选项：

-c list 指定剪切字符数。

-f field 指定剪切域数。

-d 指定与空格和tab键不同的域分隔符。

-c用来指定剪切范围，如下所示：

-c1，5-7 剪切第1个字符，然后是第5到第7个字符。

-c1-50 剪切前50个字符。

-f 格式与-c相同。

-f1，5 剪切第1域，第5域。

-f1，10-12 剪切第1域，第1 0域到第1 2域。



如：从字符串中”aaabb:aaaaa:bbb”将”aaaaa”切割出来

>echo ”aaabb:aaaaa:bbb” | cut –d “:” –f2



3.5	 split
3.6	
split用来将大文件分割成小文件。有时文件越来越大，传送这些文件时，首先将其分割可能更容易。使用vi或其他工具诸如sort时，如果文件对于工作缓冲区太大，也会存在一些问题。因此有时没有选择余地，必须将文件分割成小的碎片。

Split命令一般格式：

split –output-file-line input-filename output-filename

这里output-file-size指的是文本文件被分割的行数。Split查看文件时，output-file-line选项

指定将文件按每个最多1000行分割。如果有个文件有2800行，那么将分割成3个文件，分别有1000、1000、800行。每个文件格式为x[aa]到x[zz]，x为文件名首字母， [aa]、[zz]为文件名剩余部分顺序字符组合，



4匹配或者过滤操作

4.1 grep的使用

grep可以从输入的字符中，过滤某些或者过滤掉某个特定字符的命令。

一般使用为：

grep “特征字符串”  inputFile

grep –v “特征字符串”  inputFile



4.2  awk命令的使用

awk是可以使用很复杂，但是能完成某些特定功能，并且常使用的一个命令。使用用法：

awk [–F 分隔符] ‘模式’ inputfile

-F可以指定域或者列之间的分割符，如果不指定，使用默认的分割符（空格或者TAB）。比如对于分割unload命令下载的文件， 可以指定 –F |

对于模式中的使用分割符分割后的域，标记$1，$2 . . . $n，$0标识所有的域。

为打印一个域或所有域，使用p r i n t命令

比如打印当前目录的所有文件的大小名称:

>ls –al | awk ‘{ print $5, $9}’   #大小与文件名称使用空格格开，即$5,$9使用空格连接

>ls –al | awk ‘{ print $5”|”$9}’  #大小与文件名称使用|格开,即$5,$9使用|连接

使用BEGIN模式打印头部信息：

>ls –al | awk ‘BEGIN {print “size  filename”} { print $5”\t”$9}’  #相当于打印列的标题

使用END模式打印尾部信息：

>ls –al | awk ‘{print $5”\t”$9} END{print “finished”}’  #在列出文件后，加上finished字符



awk中使用正则表达式

awk中正则表达式匹配操作用到的字符有：

\ ^ $ . [] | () * + ?

用法：

awk [-F 分割符] ‘{if (express) 操作}’

即指定域满足express表达式的行，才打印出来.

如打印目录文件中包含sms的文件：

>ls –al | awk ‘{if ( $9~/sms/) print $0}’

如打印目录文件大小大于100000字节的文件：

>ls –al | awk ‘{if ( $5>100000) print $0}’



awk中还有很多用法，在此不列出来



4.3 sed命令



5信号处理

信号就是系统向脚本或命令发出的消息，告知它们某个事件的发生。这些事件通常是内存错误，访问权限问题或某个用户试图停止你的进程。信号实际上是一些数字。下表列出了最常用的信号及它们的含义列出所有信号：

>kill –l

HUP INT QUIT ILL TRAP IOT EMT FPE KILL BUS SEGV SYS PIPE ALRM TERM USR1

USR2 CLD PWR VTALRM PROF IO WINCH STOP TSTP CONT TTIN TTOU



一些信号的含义：

1 SIGHUP 	挂起或父进程被杀死

2 SIGINT 	来自键盘的中断信号，通常是< C T R L - C >

3 SIGQUIT 	从键盘退出

9 SIGKILL 	无条件终止

11 SIGSEGV 	段（内存）冲突

15 SIGTERM 	软件终止（缺省杀进程信号）



5.1 发出信号：

kill –信号  进程号

注明：kill –9 进程号  杀死进程时，操作系统直接将进程从内核清除，不作退出的处理



5.2 检测信号或者捕捉信号

有些信号可以被应用程序或脚本捕获，并依据该信号采取相应的行动。另外一些信号不

能被捕获。例如，如果一个命令收到了信号9，就无法再捕捉其他信号。

当脚本捕捉到一个信号后，它可能会采取下面三种操作之一：

1) 不采取任何行动，由系统来进行处理。

2) 捕获该信号，但忽略它。

3) 捕获该信号，并采取相应的行动



如果需要捕捉信号后，采用自定义的操作，可以使用trap命令：

trap name signal(s)

其中，name是捕捉到信号以后所采取的一系列操作。实际生活中， name一般是一个专门用来处理所捕捉信号的函数。Name需要用双引号（“ ”）引起来。Signal就是待捕捉的信号。

下表列出了一些最常见的trap命令用法：

trap "" 2 3 			忽略信号2和信号3，用户不能终止该脚本

trap"commands" 2 3 	如果捕捉到信号2或3，就执行相应的commands命令

trap 2 3 			复位信号2和3，用户可以终止该脚本



如：收到3( SIGQUIT 	从键盘退出),打印一行“proc received SIGQUIT and exit”

#!/bin/ksh



trap “fun_exit” 3



fun_exit()

{

   echo “proc received SIGQUIT and exit”

   exit 1

}



echo “start running”



exit 0



6 eval命令

eval命名可以执行之后跟随的命令或者变量所赋的值或者表达式。比如：

用法1：

eval echo “aaa”

用法2：

command=env

eval $env

command=”echo aaa”

eval $command

用法3:

value=0

eval [ $? -gt $value ]&&j=1

eval [ $? -gt $value ]&& echo “successfully”

eval var=$#

eval命令在执行程序运行过程中赋值命令的变量非常有用。比如在SHELL编制的人机交互界面中，选中某个菜单项后执行没个命令或者函数，脚本本身不可能为每个菜单项case一遍。



##【4】其他

4.1 使用不同的壳执行命令文件

1) 如果Script的第一个非空白字元不是"#"，则它会使用Bourne Shell。 

2) 如果Script的第一个非空白字元是"#"时，但不以"#!"开头时，则它会使用C Shell。 

3) 如果Script以"#!"开头，则"#!"後面所写的就是所使用的Shell，而且要将整个路径名称指出来，这里建议使用第三种方式指定Shell ，以确保所执行的就是所要的。Bourne Shell的路径名称为/bin/sh ，而C Shell 则为/bin/csh。 我们一般使用ksh， 路径为/bin/ksh



4.2 使用不同SHELL的区别

  BSH: 

      设置环境变量使用export var=var_value; var=var_valu; export var

  CSH/KSH:

      设置环境变量使用setenv var var_value



一些KSH独有的特征：

1)KSH环境变量

HISTSIZE:历史命令数量，默认为128,可以在.chsrc中将其设置为其他值

TMOUT   :超时自动退出，用于一段时间没有键入命令，强制退出    

1)	别名
2)	
可以定义自己的标识，标识定义的命令。比如：

alias dba dbaccess $TELLIN_DBNAME

3)	支持数组变量
4)	


4.3 SHELL程序的返回值不能超出255，否则返回值将不确定

  

4.4  read命令将输入的多余的part给最后一个变量

>read var1 var2

aa bb cc

>echo $var1

aa

>echo $var2

bb cc



4.5 调试

使用-x

1) 在SHELL程序指定执行为调试模式

#!/bin/sh –x



2) 在命令行中指定调试模式执行

指定SHELL –x 程序名称，如：

sh –x update_iuser214.sh



4.6 执行SHELL

前台执行：

>sh 程序名称

>程序名称

后台执行：

>sh 程序名称  &

>程序名称     &



4.7 移植性

目前智能业务部的设备选型中，小型机从IBM/HP/SUN 3家中选择。相应我们的SHELL一般需要在AIX,HP-UX,SunOS上应当保持一致。即SHELL程序一般需要在3中操作系统上进行移植。

可以使用uname –s确定机器的操作系统，比如：

#机器类型

OsType=`uname -s`

if [ "-$OsType" = "-SunOS" ]; then

    …

elif [ "-$OsType" = "-HP-UX" ]; then

    …

elif [ "-$OsType" = "-AIX" ]; then

    …

else

   echo "ERROR: system not support this machine type $OsType"

   eixt 1

fi



大部分常见的UNIX命令在以上3中操作是一致的，但是某些命令则具有差异(如ftp的ls在HP-UX为nlist)。如果碰到与操作系统相关的地方，则需要根据操作系统作相应处理。





附录：

一个SHELL编制的人机交互界面，里面使用的SHELL语法比较深入。如果能读懂或者编制同样程序，则表明你的SHELL教本功底已经足够深厚。如果不能读懂，可以挑战一下自己。

# Linux下打包压缩war和解压war包

把当前目录下的所有文件打包成game.war

jar -cvfM0 game.war ./

-c   创建war包

-v   显示过程信息

-f    

-M

-0   这个是阿拉伯数字，只打包不压缩的意思





解压game.war到当前目录

jar -xvf game.war



# Ubuntu开机直接进入控制台

只需编辑文件`/etc/default/grub`，把 `GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash”`改成`GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash text”`，然后再运行`sudo update-grub`即可。

在控制台下想进入x-window，可以在root用户下输入：`gdm`或者`startx`

修改Ubuntu默认启动进入文本模式后，重新启动后停在Checking battery state问题。没关系，实际系统已经启动，按键 ALT+F1 即可进入输入用户名登录得字符提示界面。


