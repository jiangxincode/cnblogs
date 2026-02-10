---
title: "Awesome ADB"
categories:
  - android
tags:
  - Android
  - adb
toc: true
---

ADB（Android Debug Bridge）是Android SDK中的一个命令行工具，用于与Android设备进行通信和调试。以下是一些常用的ADB命令汇总。

## 一些比较好的文章

* Android Native 之 adbd进程分析: <https://blog.csdn.net/qq_27672101/article/details/148332643>
* Android 系统内的守护进程 - core类中的服务 (1) : adbd: <https://blog.csdn.net/Xiaoma_Pedro/article/details/103919142>
* awesome-adb: <https://github.com/mzlogin/awesome-adb>
* ADB: <http://adbshell.com/>
* 解决adb push时出现的"Read-only file system"问题: <https://www.cnblogs.com/jiangxinnju/p/8186390.html>
* android adb push 与 adb install的比较（两种安装APK的方法）: <http://blog.csdn.net/liranke/article/details/6795984>
* Android 8.0 adb shell dumpsys activity activities | findstr mFocusedActivity 获取当前的 activity 显示空的: <https://www.cnblogs.com/yinzhuoqun/p/9090030.html>
* Android adb shell svc 知识详解: <https://blog.csdn.net/wenzhi20102321/article/details/132779708>

## 常用命令

```shell
ps --help
ps -o help # 查看输出的字段说明

# 查看system_server进程的PID
ps -ef | grep system_server # 方法一
pidof system_server # 方法二

# 查看某进程的UID
ps -ef | grep system_server
cat /proc/<pid>下的内容

# 查看某进程的UID中的某个线程的信息
ps -T -p 3254 | grep Fingerprint

# 查看某个进程的adj值
cat /proc/<pid>/oom_score_adj

# 查看某个进程是否被冷冻
ps -A | grep system_server 看是否处于do_freezer_trap状态

adb shell dumpsys SurfaceFlinger | grep -i "Display 0 HWC layers"

adb shell cmd window tracing level all
adb shell dumpsys window debugConfiguration
adb shell cmd window tracing start|stop

adb exec-out dumpsys window --proto > window_dump.pb

adb shell service call SurfaceFlinger 1025 i32 1
adb shell service call SurfaceFlinger 1025 i32 0
adb shell service list | grep SurfaceFlinger


adb shell pm list packages
adb shell pm path pkgName
adb shell pm disable pkgName


dumpsys package pkgName | gre userId

dumpsys package pkgName | grep targetSdk

adb shell setprop persist.log.tag M

adb shell cat dev/kmsg # 实时kmsg日志

adb shell logcat -G 16M
adb shell logcat -v threadtime -c

adb shell "mount -o remount,rw /system"
adb remount

adb shell dumspys battery set level 8

adb unistall pkgName
adb shell "dd if=/dev/zero of=/data/local/tmp/test.txt bs=1M count=10"

adb shell setprop persist.sys.dalvik.vm.lib.2 art
adb shell getprop persist.sys.dalvik.vm.lib.2

adb shell settings put global window_animation_scale 0.0
adb shell am broadcast -a android.intent.action.CLOSE_SYSTEM_DIALOGS

adb shell svc power stayon true

adb shell ime list -s
adb shell settings get secure default_input_method


adb shell wm logging enable-text WM_DEBUG_KEEP_SCREEN_ON
```

## 解决adb push时出现的"Read-only file system"问题

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

## 手机连手机ADB

比如A手机通过ADB控制B手机，A手机安装termux

* <https://termux.dev/cn/>
* <https://github.com/termux/termux-app>

安装后在A手机上打开termux，安装adb

```shell
pkg update && pkg upgrade //会提示没选安装源，直接回车就行，自动会处理
pkg install android-tools //安装adb
```

A、B手机连接同一个wifi
B手机在开发者选项打开adb无线调试，记录IP地址和端口
A手机上执行`adb connect ip:port`即可连接
A手机上赋予文件系统权限：`termux-setup-storage`
手动选赋予权限，执行后，会在Termux的主目录下创建一个`storage`子目录(`/data/data/com.termux/files/sdcard`)，并建立与手机外部存储的符号链接。

## Android真机安装sqlite3的方法

Android版本: 4.4.2

```powershell
PS C:\Users\jiang> adb shell
shell@hwH60:/ $ su - root

# 此时输入sqlite3 发现命令无法使用
root@hwH60:/ # sqlite3
tmp-mksh: sqlite3: not found

# find一下相关文件，确定到底需要安装哪些内容，如果已经找到则不需要安装对应文件
root@hwH60:/ # find . -name "sqlite3"
root@hwH60:/ # find . -name "libsqlite.so"
root@hwH60:/ # find . -name "libsqlite_jni.so"

root@hwH60:/ # exit
shell@hwH60:/ $ exit

# 从https://files.cnblogs.com/files/jiangxinnju/sqlite3.zip处下载文件并解压。

# 将相关文件放到内置存储卡中，为什么不直接放到/system/xbin/和/system/lib/可以参考<http://www.cnblogs.com/jiangxinnju/p/8186390.html>
PS D:\> adb push sqlite3 /storage/emulated/0/
PS D:\> adb push libsqlite.so /storage/emulated/0/
PS D:\> adb push libsqlite_jni.so /storage/emulated/0/

PS D:\> adb shell
shell@hwH60:/ $ su - root

# 为什么需要重新挂载/system分区可以参考<http://www.cnblogs.com/jiangxinnju/p/8186390.html>
root@hwH60:/ # mount -o remount rw /system

# 将需要的文件从内置存储卡中转移到目标目录
root@hwH60:/ # cp /storage/emulated/0/sqlite3  /system/xbin/                              <
root@hwH60:/ # cp /storage/emulated/0/libsqlite.so  /system/lib/
root@hwH60:/ # cp /storage/emulated/0/libsqlite_jni.so  /system/lib/

# 修改对应文件的权限
root@hwH60:/ # chmod 4755 /system/xbin/sqlite3
root@hwH60:/ # chmod 0644 /system/lib/libsqlite.so
root@hwH60:/ # chmod 0644 /system/lib/libsqlite_jni.so

# 执行sqlite3命令，发现已经可以使用
root@hwH60:/ # sqlite3
SQLite version 3.7.11 2012-03-20 11:35:50
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite> .exit

root@hwH60:/ # exit

# 删除内置存储卡中的文件
shell@hwH60:/ $ rm -rf /storage/emulated/0/sqlite3
shell@hwH60:/ $ rm -rf /storage/emulated/0/libsqlite.so
shell@hwH60:/ $ rm -rf /storage/emulated/0/libsqlite_jni.so

```
