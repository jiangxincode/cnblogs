---
title: "Repo实践指南"
categories:
  - android
tags:
  - Android
  - Repo
toc: true
---

Android使用Git作为代码管理工具，开发了Gerrit进行代码审核以便更好的对代码进行集中式管理，还开发了Repo命令行工具，对Git命令进行封装，将几百个Git库有效的进行组织。Repo并不是用来取代Git，而是用Python对Git进行了一定的封装，简化了对多个Git版本库的管理。对应Repo管理的任何一个版本库，都需要使用Git命令进行操作。

## Repo工作流

下图是Repo工作流，大体分为如下几个核心步骤：

1. 运行`repo init`，克隆Android的一个清单库。这个清单库是通过XML技术建立的版本库清单。清单库中的manifest.xml文件，列出了几百个版本库的克隆方式。包括版本库的地址和工作区地址的对应关系，以及分支的对应关系。
2. 运行`repo sync`，分别克隆这几百个版本库到本地的工作区。
3. 运行`repo start`创建并切换到本地工作分支。
4. 本地修改代码，通过Git相关命令在某些项目中进行操作。
5. 通过`repo upload`命令将代码修改发布到代码审核服务器。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/1.png)

## Repo引导脚本下载

在使用Repo前我们需要下载一个Repo引导脚本，Repo的核心功能不在其中，该引导脚本只是下载并加载完整Repo程序的工具。

```shell
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

这里需要提到一点的是早期的Repo引导脚本是一个Shell脚本，第一行就是`#!/bin/sh`，然后通过以下代码完成Shell向Python的转换，不过在较新版本中都是直接使用Python，第一行变成了`#!/usr/bin/env python`。现在网络上的很多介绍都过时了。

```shell
magic='--calling-python-from-/bin/sh--'
"""exec" python -E "$0" "$@" """#$magic"
```

## Repo清单库介绍

一个清单库可以包含多个清单文件和多个分支，每个清单文件和分支都有对应的版本。清单文件以XML格式组织。举个例子：

```shell
repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-11.0.0_r27
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

  <remote  name="aosp"
           fetch=".."
           review="https://android-review.googlesource.com/" />
  <default revision="refs/tags/android-11.0.0_r27"
           remote="aosp"
           sync-j="4" />

  <project path="build/make" name="platform/build" groups="pdk" >
    <copyfile src="core/root.mk" dest="Makefile" />
    <linkfile src="CleanSpec.mk" dest="build/CleanSpec.mk" />
    <linkfile src="buildspec.mk.default" dest="build/buildspec.mk.default" />
    <linkfile src="core" dest="build/core" />
    <linkfile src="envsetup.sh" dest="build/envsetup.sh" />
    <linkfile src="target" dest="build/target" />
    <linkfile src="tools" dest="build/tools" />
  </project>
  <project path="build/blueprint" name="platform/build/blueprint" groups="pdk,tradefed" />
  ...
</manifest>
```

* remote元素，定义了名为aosp的远程版本库，其库的基址为<https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform>，还定义了代码审核服务器的地址<https://android-review.googlesource.com/>。当然，还可以定义更多的remote元素。
* default元素，设置各个项目默认远程版本库为aosp，默认的的分支为`refs/tags/android-11.0.0_r27`。当然各个project元素还可以定义自己的remote和revision覆盖默认的配置。
* project元素，用于定义一个项目，path属性表示在工作区克隆的位置，name属性表示该项目的远程版本库的相对路径。
* project元素的子元素copyfile，定义了项目克隆后的一个附件动作，从src拷贝文件到dest。

## 通过Repo下载AOSP系统源码

现在你可以通过Repo下载AOSP源码了，但是由于墙的原因，我们没有办法直接下载，需要通过一些AOSP镜像，其中使用比较多的是清华的镜像，具体下载方式请参考官方介绍：<https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/>

### Repo下载AOSP过程中可能遇到的问题

1. 某些project找不到：

```shell
...
Checking out projects:  58% (432/733) platform/frameworks/hardware/interfaceserror: Cannot checkout platform/frameworks/layoutlib: ManifestInvalidRevisionError: revision refs/tags/android-10.0.0_r47 in platform/frameworks/layoutlib not found
error: in `sync -c -j4`: revision refs/tags/android-10.0.0_r47 in platform/frameworks/layoutlib not found
```

这个问题我一直没有找到根因，可能是镜像的问题，也可能是网络的问题。解决方式发现哪个project找不到就单独同步该项目，然后再整体同步。

```shell
repo sync -c platform/frameworks/layoutlib
repo sync -c -j4
```

## Repo常用指令

Repo子命令实际上是Git命令的封装。每一个Repo子命令都对应于repo源码树中subcmds目录下的一个同名的Python文件。每一个repo子命令都可以通过下面的命令获得帮助。

```shell
repo help <command>
```

当然你也可以参考Repo官方的介绍：<https://source.android.com/setup/develop/repo>

### repo init

```shell
repo init –u URL [OPTIONS]
```

常用参数如下，其它参数通过repo help init查询：

* -u(--manifest-url):设定清单库的Git服务器地址
* -m(--manifest-name):当有多个清单文件时，指定清单库中的某个清单为有效的清单文件。默认为default.xml
* -b(--manifest-branch):选择一个maniest仓库中的一个特殊的分支

命令repo init 要完成如下操作：

* 完成repo工具的完整下载，执行的Repo脚本只是引导程序
* 克隆清单库manifest.git (地址来自于-u 参数)
* 克隆的清单库位于manifest.git中，克隆到本地`.repo/manifests`。在之前的Repo版本中清单`.repo/manifest.xml`只是符号链接，它指向`.repo/manifests/default.xml`。在目前的repo版本中清单`.repo/manifest.xml`是一个实际的文件，通过include的方式引用`.repo/manifests/default.xml`
* 如果`.repo/manifests`中有多个xml文件，`repo init`可以任意选择其中一个，默认选择是default.xml
* 在`.repo/manifests`中执行`git branch -a | cut -d / -f 3`可以查看本地存放的已有的所有分支信息，但是该信息只是同步到你上次下载时的信息，如果需要最新信息需要先在该目录中执行`git pull`操作。

```shell
repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-11.0.0_r27 # 在当前目录出现了.repo文件夹
repo init -u git://192.168.0.125/manifest.git –m android.xml # 选择的是android.xml里面的配置，.repo/manifest.xml便指向.repo/manifests/android.xml
```

### repo sync

```shell
repo sync [<project>…]
```

用于参照清单文件`.repo/manifest.xml`克隆并同步版本库。如果某个项目版本库尚不存在，则执行repo sync 命令相当于执行git clone，如果项目版本库已经存在，则相当于执行下面的两条指令：

```shell
git remote update # 相当于对每一个remote源执行了fetch操作
git rebase origin/branch # 针对当前分支的跟踪分支执行rebase操作
```

如果直接执行`repo sync`会同步所有project，如果后面指定project则只会同步指定的project。如`repo sync platform/build`。

### repo rebase

### repo smartsync

可以通过一些选项设置同步的方式，比如是否在遇到第一个错误的时候就停止，是否强制删除含有未提交修改的项目等等。

### repo start

```shell
repo start  <newbranchname> [--all | <project>…]
```

刚克隆下来的代码是没有分支的，`repo start`实际是对`git checkout –b`命令的封装。为指定的项目或所有项目（若使用—all参数），以清单文件中为设定的分支，创建特性分支。这条指令与`git checkout –b`还是有很大的区别的，`git checkout –b`是在当前所在的分支的基础上创建特性分支，而`repo start`是在清单文件设定分支的基础上创建特性分支。

```shell
repo start stable --all # 假设清单文件中设定的分支是gingerbread-exdroid-stable，那么执行以上指令就是对所有项目，在gingerbread-exdroid-stable的基础上创建特性分支stable
repo start stable platform/build platform/bionic # 假设清单文件中设定的分支是gingerbread-exdroid-stable，那么执行以上指令就是对platform/build、platform/bionic项目，在gingerbread-exdroid-stable的基础上创建特性分支stable
```

### repo checkout

```shell
repo checkout <branchname>  [<project>…]
```

实际上是对`git checkout`命令的封装，检出之前由`repo start`创建的分支。但不能带-b参数，所以不能用此命令来创建特性分支。

```shell
repo checkout aosp-dev 
repo checkout aosp-dev  platform/build  platform/bionic
```

### repo branches

读取各个项目的分支列表并汇总显示。该命令实际上通过直接读取`.git/refs`目录下的引用来获取分支列表，以及分支的发布状态等。

```shell
repo branches [<project>…]
```

```shell
repo branches 
repo branches platform/build platform/bionic
```

### repo diff

```shell
repo diff [<project>…]
```

实际是对git diff 命令的封装,用于分别显示各个项目工作区下的文件差异。

```shell
repo diff # 查看所有项目
repo diff platform/build platform/bionic # 只查看其中两个项目
```

### repo stage

实际是对`git add --interactive`命令的封装、用于挑选各个项目工作区中的改动以加入暂存区。

```shell
repo stage -i [<project>…]
```

-i代表`git add --interactive`命令中的`--interactive`，给出个界面供用户选择。

### repo prune

实际上是对`git branch –d`命令的封装，该命令用于扫面项目的各个分支，并删除已经合并的分支，用法如下：

```shell
repo prune [<project>…]
```

### repo abandon

实际上是对`git branch –D`命令的封装，用法如下：

```shell
repo abandon <branchname> [<project>…]
```

### repo status

实际上是对`git diff-index`、`git diff-filse`命令的封装，同时显示暂存区的状态和本地文件修改的状态

```shell
repo status platform/bionic
```

以上的实例输出显示了platform/bionic项目分支的修改状态

* 每个小节的首行显示羡慕名称，以及所在分支的名称
* 第一个字母表示暂存区的文件修改状态
  * -:没有改变
  * A:添加（不在HEAD中，在暂存区中）
  * M：修改（在HEAD中，在暂存区中，内容不同）
  * D:删除（在HEAD中，不在暂存区）
  * R：重命名（不在HEAD中，在暂存区，路径修改）
  * C：拷贝（不在HEAD中，在暂存区，从其他文件拷贝）
  * T：文件状态改变（在HEAD中，在暂存区，内容相同）
  * U：未合并，需要冲突解决
* 第二个字母表示工作区文件的更改状态
  * -：新/未知（不在暂存区，在工作区）
  * m：修改（在暂存区，在工作区，被修改）
  * d：删除（在暂存区，不在工作区）
* 两个表示状态的字母后面，显示文件名信息。如果有文件重名还会显示改变前后的文件名及文件的相似度

### repo remote

```shell
repo remote add <remotename>  <url> [<project>…] 
repo remote rm <remotename>  [<project>…]
```

```shell
repo remote add origin_1 ssh://192.168.0.125/git_repo # 这个指令是根据xml文件添加的远程分支，方便于向服务器提交代码，执行之后的build目录下看到新的远程分支org
repo remote rm origin_1 # 删除远程仓库
```

### repo push

```shell
repo push <remotename> [--all |<project>…]
```

这是新添加的指令，用于向服务器提交代码，repo会自己查询需要向服务器提交的项目并提示用户。

```shell
repo push org
```

### repo forall

```shell
repo forall [<project>…] –c <command>
```

迭代器，可以在所有指定的项目中执行同一个shell指令

* -c:后面所带的参数着是shell指令
* -p:在shell指令输出之前列出项目名称
* -v:列出执行shell指令输出的错误信息

额外的环境变量:

* REPO_PROJECT:指定项目的名称
* REPO_PATH:指定项目在工作区的相对路径
* REPO_REMOTE:指定项目远程仓库的名称
* REPO_LREV:指定项目最后一次提交服务器仓库对应的哈希值
* REPO_RREV:指定项目在克隆时的指定分支，manifest里的revision属性

 另外，如果-c后面所带的shell指令中有上述环境变量，则需要用单引号把shell指令括起来。

```shell
repo forall -c 'echo $REPO_PROJECT' # 输出项目的名称
repo forall -p -c git merge aosp-my-dev # 把所有项目多切换到master分支，该指令将会把aosp-my-dev分支合并到master分支
repo forall -c git tag aosp-mytag-1.0 # 在所有项目下打标签
repo forall -c 'git remote add origin_1 ssh://jiangxin@192.168.0.125/$REPO_PROJECT.git' # 引用环境变量REPO_PROJECT添加远程仓库
repo forall -c git remote add origin_1 # 删除远程仓库
repo forall –c git branch aosp-dev # 切换分支
repo forall –c git checkout –b aosp-dev # 创建分支
repo forall -c git reset --hard # 当repo sync时如果提示discarding xx commits时可以通过该命令废弃所有提交，然后继续repo sync
repo forall -p -c "git log -S fitsSystemWindows --pretty=oneline --since=2024-01-01 --until=2024-12-31 author:jiangxin" # 在所有项目中查找fitsSystemWindows的提交记录
```

### repo grep

相当于对git grep 的封装，用于在项目文件中进行内容查找。

### repo manifest

显示manifest文件内容，可以通过-o参数输出到指定的文件中。

```shell
repo manifest –o android.xml
```

### repo version

显示Repo的版本号，还会同时显示Git/Python等依赖的应用版本。

### repo upload

repo upload相当于git push，但是又有很大的不同。它不是将版本库改动推送到克隆时的远程服务器，而是推送到代码审核服务器(Gerrit软件架设)的特殊引用上，使用SSH协议。代码审核服务器会对推送的提交进行特殊处理，将新的提交显示为一个待审核的修改集，并进入代码审查流程，只有当审核通过后，才会合并到官方正式的版本库中。

```shell
repo upload [--re --cc] {[<project>]… | --replace <project>}
```

* -h, --help:显示帮助信息
* -t:发送本地分支名称到Gerrit代码审核服务器
* --replace:发送此分支的更新补丁集
* --re=REVIEWERS:要求指定的人员进行审核
* --cc=CC:同时发送通知到如下邮件地址

### repo download

主要用于代码审核者下载和评估贡献者提交的修订。

```shell
repo download {project change [patchset]}…
```

### repo selfupdate

用于repo自身的更新
