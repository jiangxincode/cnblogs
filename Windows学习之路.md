# 瘦身右键里的“发送到”

xp是在“C:\Documents and Settings\Administrator\SendTo”下，win7位置有所不同。当然了这些文件夹肯定是默认隐藏的，如果你看不到，别忘了先进文件夹选项显示隐藏文件和文件夹。我只保留了，“桌面快捷方式”一个，其余杀之！

# 不修改权限，修改hosts和service文件

win7的用户权限管理比较严格，默认情况下你是无法直接修改hosts和service这样的文件，提示无权限。网上有很多教程，讲解如何获取管理员或文件权限，如果你只是想修改类似这样的文件，不用动那么大的干戈，一个小小的动作就行。复制hosts、service文件系统文件夹之外的其他地方，任意编辑器修改-》保存，再paste回去覆盖掉系统同名文件，done.



# Windows/system32权限问题

由于权限问题，无法修改其中的文件，可以右键取得管理员权限。

# Windows 8如何删除服务

现在的流氓软件，越来越多把自己注册为一个服务。对于这些流氓软件，需要删除相关的exe文件，使它不能再运行，或者直接清除这个服务本身，使计算机重启的时候，它不会再启动。删除的办法有两个：

1.用sc.exe这个Windows命令。开始--运行--cmd.exe,然后输入sc就可以看到了。使用办法很简单：sc delete "服务名" (如果服务名中间有空格，就需要前后加引号)。如 sc delete KSD2Service

2.直接进行注册表编辑(不推荐)。打开注册表编辑器，找到下面的键值：

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services 

一般服务会以相同的名字在这里显示一个主健，直接删除相关的键值便可。

注：

1.如果服务显示的是rundll32.exe,并且这个文件是位于system32目录下，那么就不能删除这个rundll32.exe文件，它是Windows系统的文件。这时只要清除相关的服务就可以了

2.如果一个服务删除了马上又自动建立了，说明后台有进程在监视、保护。需要先在进程管理器中杀掉相应的进程，或者启动后按F8,到安全模式下删除。

# 在windows的资源管理器当前路径打开一个命令行

快捷键Alt+D选中地址栏，然后直接敲cmd

注：你还能在资源管理器的地址栏启动其他程序，比如写字板(notepad)。

或者：Shift加右键，选择在此处打开命令窗口


# Powershell常用命令：

* 同时打开多个powershell窗口：Win+R+powershell 多次即可
* 查看powershell命令帮助 help [cmd]：help Remove-Item
* 删除文件夹：Remove-Item path –Recurse –Forse


# 如何改变PowerShell启动的默认目录 

为什么要修改PowerShell默认的启动目录, 如果你习惯操作一些特殊的命令行程序, 而又不习惯把它们放在默认的home路径下, 修改默认的启动位置, 可以让你在每次启动Powershell的时候不用执行切换目录的操作.

PowerShell的默认启动路径其实就是执行PowerShell时指定的默认工作目录. 你可以编辑PowerShell的快捷方式, 在启动位置中输入一个你希望的默认位置. 这样再执行PowerShell时, 它默认的启动路径就是新的位置了.

除了这个方法, 你还可以通过修改特定的profile来实现这个操作, 简单的在profile中加入cd XXX即可.

最后说一下$home这个变量, 它是 HOMEPATH 和 HOMEDRIVE两个环境变量组合成的. 这两个环境变量存储在注册表中.  这两个变量我不推荐修改, 因为不知道会产生哪些副作用...但是理论上修改这些变量可以修改用户的主目录位置.



# Beyond Compare对比.class文件

使用Beyond Compare扩展插件可以直接对比编译的.class文件，而不会显示一大堆乱码。

* windows：http://www.scootersoftware.com/download.php?zz=kb_moreformats_win
* linux：http://www.scootersoftware.com/download.php?zz=kb_moreformats_nix

# 解决xshell中vim显示中文乱码的问题

打开一个用utf8编码的中文文件，在vim中，执行

```vimscript
    set encoding=utf-8 termencoding=gbk fileencoding=utf-8后可正常显示中文咯。
```

* encoding是设置档案的当前编码
* termencoding是用于vim屏幕的显示编码，由于xshell默认用于显示屏幕的编码是gbk,所以此处设置为gbk。同理，假设你修改了xshell的默认编码为utf-8，那么此处自然应该utf-8
* fileencoding档案保存时的编码，此编码应和encoding保持一致，否则会弹出警告

至于xshell，打开file->Properties，点击Terminal节点，修改Terminal Type为linux(键盘映射模式，默认为xtrem，此种模式下对于vim小键盘输入数字会出现乱字符号)，修改Encoding为uft-8(一般情况下linux系统采用此编码，可用locale命令查看自己系统的默认编码，修改为一致的就行)。

同理，也可以修改xftp的编码为utf-8以正常显示中文。


# VirtualBox

## Windows 8.1+VirtualBox较新版本打开虚拟机时报错

报错信息：
```
    Unable to load R3 module D:\Program Files\Oracle\VirtualBox/VBoxDD.dll
    (VBoxDD):GetLastError=1790
    (VERR_UNRESOLVED_ERROR)
```
解决办法是在Windows/system32下：

* themeui.dll.old.tweakcube替换themeui.dll
* uxtheme.dll.old.tweakcube替换uxtheme.dll

如果是Windows 7中遇到类似问题，参考：
http://jingyan.baidu.com/article/ab69b270bb7b2a2ca6189f6d.html

