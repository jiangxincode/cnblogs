欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju


出现`Read-only file system`问题，不是因为文件或者文件夹的权限不对，而是要push的目录对应的分区是以只读方式挂载的，网上给出的解决办法是重新以读写方式挂载对应分区，以`/system`分区为例，使用命令：`mount -o remount rw /system`，当然如果你想重新挂载系统分区需要有root权限。

但是你会发现，当你在adb shell中使用该方式重新挂载分区后，退出adb shell后用adb push命令向`/system`分区推送文件时仍然报错`Read-only file system`，这是因为在adb shell中重新挂载分区只针对当前的shell有效，在退出后该挂载方式失效。所以即使你打开两个cmd/powershell窗口，一个窗口使用adb shell重新挂载分区，在另一个窗口adb push也是不行的。

我这边最终尝试可行的方法是通过手机内置存储卡(外置SD卡也可以，但是有的手机没有外置SD卡)中转下，例如我想把计算机上的SystemUI.apk文件拷贝到手机的/system/app目录下，可以按照下面方式操作：

```powershell
PS C:\Users\jiang> adb push .\SystemUI.apk /sdcard
.\SystemUI.apk: 1 file pushed. 3.9 MB/s (2621700 bytes in 0.648s)
PS C:\Users\jiang> adb shell
shell@hwH60:/ $ su - root
130|root@hwH60:/ # mount -o remount rw /system
root@hwH60:/ # cp /sdcard/SystemUI.apk  /system/app/
shell@hwH60:/ $ cd /system/app
root@hwH60:/system/app # chmod 644 SystemUI.apk
```