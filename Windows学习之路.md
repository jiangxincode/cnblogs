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

# 同时打开多个powershell窗口

Win+R+powershell 多次即可


# Beyond Compare对比.class文件

使用Beyond Compare扩展插件可以直接对比编译的.class文件，而不会显示一大堆乱码。

* windows：http://www.scootersoftware.com/download.php?zz=kb_moreformats_win
* linux：http://www.scootersoftware.com/download.php?zz=kb_moreformats_nix

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

