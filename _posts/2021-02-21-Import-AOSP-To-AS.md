---
title: "将AOSP源码导入到Android Studio进行查看"
categories:
  - Blog
tags:
  - Android
  - Android Studio
  - AOSP
toc: true
---

## 生成iml和ipr文件

```shell
source build/envsetup.sh
lunch aosp_x86-eng
make idegen
development/tools/idegen/idegen.sh
```

说明：

1. 执行`source build/envsetup.sh`和`./build/envsetup.sh`是一样的。
2. 可以直接执行`lunch aosp_x86-eng`直接根据传入参数进行构建，也可以输入`lunch`根据提示选择对应的target。
3. 执行完`lunch`命令后直接执行`make idegen`即可，有些教程说需要先执行`make`命令，这是不需要的，我们只需要构建`idegen`模块，不需要构建所有模块。后者要花费很长时间，而且对机器性能要求很高。命令执行过程中有些提示选项，如果没有报错导致中断，可以暂时忽略。有的教程使用`mmm development/tools/idegen/`代替`make idegen`，他们的功能是类似的。
4. 执行`development/tools/idegen/idegen.sh`，可能会提示权限相关问题，如果没有中断程序可以暂时忽略，有的教程建议增加`sudo`前缀提升命令执行权限，这里不推荐，因为之前如果`source build/envsetup.sh`是以普通用户执行的，所有的构建环境都是以普通用户为前提的，提升权限可能会导致问题，比如`java: 未找到命令`
5. 以上命令成功执行后会在根目录生成`android.iml`/`android.ipr`，两个文件。

## 将代码导入到Android Studio

绝大部分人的AOSP源码是放置到远程Linux机器上的，如果本地机和远程机间网络带宽很高，可以直接通过Samba服务器在本地机中访问远程机的AOSP源码，或者通过VNC Viewer/VNC Client的方式在远程机上安装AS。网络不是很好可以选择在本地机上创建一个目录，然后把`android.iml`/`android.ipr`以及需要查看的AOSP源码目录同步到该目录中，同步方式有很多，比如FTP/rsync等。

如果使用rsync进行同步，可以参考以下命令：

```shell
rsync -az --progress --delete --exclude=".git" ${USER_NAME}@${IP}:/${REMOTE_DIR} ${LOCAL_DIR}
```

比如：

```shell
rsync -az --progress --delete --exclude=".git" jiangxin@192.168.1.181:/home/jiangxin/aosp/frameworks /drives/d/aosp/
```

如果使用FTP命令，由于文件数目较多，直接下载或者上传目录耗时比较长，可以考虑使用`tar`将需要的文件和目录打包，然后再进行同步。

我选择的是把`android.iml`/`android.ipr`以及`frameworks`目录同步到本地。打开Android Studio，`Open an Existed Project`，选择`android.ipr`，导入时间根据机器性能以及源码规模相关，可能比较长。

* `android.iml`文件中有目录的配置，如果打开整个工程非常慢，可以把里面无关的目录删除或者改到excludeFolder中。
* 如果代码跳转到jar包的反编译文件中而不是导入的源码中，可以`File->Project Structure->Project Settings->Moudules->Dependencies`，把`Module source`调整到最顶端（Alt+Up）。
* Android Studio默认只能打开10个代码文件，且文件打开多了以后显示不开的文件还会被隐藏，需要点击最右边的箭头才能查看。而最致命的是，如果不小心修改了某个文件，在标签页上，不会有任何的提示。`File->Settings->Editor->General->Editor Tabs`根据自己的习惯进行配置。
* Android Studio只支持Java代码，C++代码只有最基础的着色功能。
* 如果想要支持断点调试，按照如下步骤操作：
  * `File->Project Structure->Project Settings->Project->Project SDK`，选择`Android API .. Platform`
  * `Run->Edit Configurations->Add New Configuration->Android App`，然后直接保存。
  * 此时可以使用Attach To Process进行调试。调试要注意源码和手机版本匹配。service相关代码需要attach到system_process进程。

## 另一种利用Android Studio查看AOSP源码的方式

还有另一种不需要`android.iml`/`android.ipr`就可以查看AOSP源码的方式：

1. 使用Android Studio创建一个简单的demo工程，确保编译通过。
2. 在`app/build.gradle`文件的`android`节点下增加如下配置，其中路径是自己想查看的AOSP源码路径，可以是本地路径也可以是远程路径：

```gradle
    sourceSets {
        main.java.srcDirs += 'D:\\Code\\sync\\android-11.0.0_r27\\frameworks\\base\\services\\core\\java'
        main.resources.srcDirs += 'D:\\Code\\sync\\android-11.0.0_r27\\frameworks\\base\\core\\res\\res'
    }
```

当然这种方式如果在自己想要查看的路径比较多时，自己手工配置路径会比较麻烦。

## 参考资料

* Android Studio导入整个Android系统源码: <https://blog.csdn.net/QQxiaoqiang1573/article/details/72903237>
* 使用Android Studio导入Android系统源码: <https://blog.csdn.net/turtlejj/article/details/83857897>
* AndroidStudio工程导入部分Android源码: <https://blog.csdn.net/mcsbary/article/details/90721626>
