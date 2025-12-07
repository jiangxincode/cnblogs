---
title: "Aloys的环境搭建手册"
categories:
  - setup-environment
tags:
  - 环境搭建
toc: true
---

## Windows 10系统下搭建Jenkins环境

主要参考：
http://www.cnblogs.com/edward2013/p/5269465.html
但是没有安装ant，而且java、maven、tomcat都是使用的压缩包方式安装。

## 配置AOSP源码查看环境

### 在Windows上安装Repo，同步AOSP代码【不推荐】

第一个想到的方案是在Windows上配置Repo，然后下载AOSP源码，参考：
Windows安装repo的真正解决方案：<https://ysy950803.blog.csdn.net/article/details/104188793>
但是就像Repo官网<https://gerrit.googlesource.com/git-repo/+/HEAD/docs/windows.md>说的那样：

  Repo is primarily developed on Linux with a lot of users on macOS. Windows is, unfortunately, not a common platform. There is support in repo for Windows, but there might be some rough edges.
  Keep in mind that Windows in general is “best effort” and “community supported”. That means we don't actively test or verify behavior, but rely heavily on users to report problems back to us, and to contribute fixes as needed.

Windows版的Repo虽然可用，但是可能会出现各种各样的问题，这些问题可能会让我们在解决环境问题上分心过多，所以不推荐这种方式。

### 在Linux上安装Repo，同步AOSP代码【推荐】

根据实际情况有两种工作模式：

1. Linux作为AOSP代码的同步、存储、查看、修改、编译环境，大部分工作都是在Linux上完成，Android Studio也是安装在Linux上，这种我觉得是最完美的模式。但是要求Linux的性能足够好。由于我这边没有实际的Linux机器，是在Windows上用虚拟机配置的Linux环境，所以没有采用这种方法。
2. Linux作为AOSP代码的同步、存储、编译环境，查看和修改工作在Windows上完成，具体的实现方式有两种：
   1. 用Samba服务器把Linux上的AOSP代码共享到Windows平台，然后在Windows平台上安装IDE环境，直接打开远程AOSP代码目录，查看和修改，这种方式的优点是配置简单，不用代码同步。但是我这边网速一般，而AOSP代码量太大，导致Android Studio经常卡死，所以我也放弃了这种方式。
   2. 将android.iml/android.ipr以及常用的仓（比如frameworks/base frameworks/native等）使用rsync等工具同步到Windows平台，然后在Windows上使用Android Studio导入，进行查看和修改，修改完成后通过Beyondcompare工具将修改的内容同步到Linux平台进行编译等工作。这个各方面折中的方案。后续主要介绍这种工作环境的配置。

#### 安装配置Linux环境

如果已经有Linux机器，本步骤省略。我采用在Windows上安装虚拟机，然后通过虚拟机安装Linux（Ubuntu）。
同时按需安装Git/Vim/OpenSSH Server等工具，安装方式不再赘述，网上有很多。

#### 下载AOSP源码

在配置好的Linux环境中下载AOSP源码，Google官方的下载AOSP源码的方式：<https://source.android.com/docs/setup/build/downloading>。
但是由于墙的原因，这种方式不容易实现，所以推荐使用清华的镜像，使用指导：<https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/>。
Repo的使用方式可以参考：Repo实践指南：<https://www.cnblogs.com/jiangxinnju/p/14274982.html>

#### 配置Windows上的工具

1. 安装SSH客户端工具，这里推荐MobaXTerm，因为它不仅免费还自带了rsync命令行工具，可以非常方便从Linux上同步代码到Windows。
2. 安装BeyondCompare工具，方便对比，将修改的代码同步到Linux环境。
3. 安装Android Sudio，将AOSP源码导入到Android Studio进行查看：<https://www.cnblogs.com/jiangxinnju/p/14426645.html>
4. 安装Source Insight工具，AS查看AOSP的Java代码比较合适，但是C/C++代码不支持跳转，着色也比较差，看这部分代码还是SI比较好用。

## TensorFlow环境搭建

### 预备条件
	Ubuntu 22.04.2 LTS
	配置好固定IP，安装SSH(Server)/Samba等基础网络连接软件

