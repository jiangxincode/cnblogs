
* VirtualBox Images: http://www.osboxes.org/virtualbox-images
* VirtualBoxes – Free VirtualBox® Images: https://virtualboxes.org/images


## Virtualbox 网络

* https://www.virtualbox.org/manual/ch06.html#network_nat

## VT-x features locked or unavailable in MSR

* https://forums.virtualbox.org/viewtopic.php?f=6&t=43403&sid=5ccd991da007192f4c429c657b725eae

## 访问USB子系统失败

解决ubuntu下virtualbox访问usb子系统失败

http://blog.coltcn.com/2012/03/13/virtualbox-error-failed-to-access-usb-subsystem/

## ubuntu用户不在sudoers文件中问题

http://blog.csdn.net/killzero/article/details/10298845

## 安装CentOS后安装增强功能

1.启动CentOS，以root身份登录，进入桌面环境。

2.执行如下命令：

    yum upadate
    yum install kernel-devel 　
    yum install gcc

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


## virtualbox命令行共享CentOS目录

1. 安装virtualbox增强工具

2. 设置共享文件夹

完成后点击"设备(Devices)" -> 共享文件夹(Shared Folders)菜单，添加一个共享文件夹，选项固定和临时是指该文件夹是否是持久的。共享名可以随意取，如"yongfu"，尽量使用英文名称，不要有空格。

3. 挂载共享文件夹

在命令行终端下输入：

    mkdir /mnt/yongfu
    mount -t vboxsf yongfu /mnt/yongfu

其中"yongfu"是之前创建的共享文件夹的名字。现在虚拟机和主机可以互传文件了。如不想每次都手动挂载，可以在/etc/fstab中添加一项

    yongfu /mnt/yongfu vboxsf rw,gid=100,uid=1000,auto 0 0

这样就能够自动挂载了。

4. 卸载的话使用下面的命令

    umount -f /mnt/yongfu

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

## VirtualBox扩容

* https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi
* http://www.cnblogs.com/zhcncn/articles/2948508.html
* http://blog.csdn.net/ganshuyu/article/details/17954733