---
title: "彻底搞懂Ubuntu系统上的包管理"
categories:
  - linux
tags:
  - Linux
  - Ubuntu
  - Debian
  - apt
  - aptitude
toc: true
---

## 关联阅读

* What is the difference between dpkg and aptitude/apt-get? <https://askubuntu.com/questions/309113/what-is-the-difference-between-dpkg-and-aptitude-apt-get>
* A snap is a bundle of an app and its dependencies that works without modification across Linux distributions: <https://snapcraft.io/>

`apt-get update`, `apt-get upgrade`, `apt-get upgrade`, `do-release-upgrade`, `apt-get remove`, `aptitude remove`...

相信很多人都接触过这些软件包更新、升级、删除的Linux命令，但是始终没能彻底理清他们的关系。这里我希望用一篇文章彻底解释清楚他们的区别。首先根据功能大类进行划分：

* 软件包更新升级相关：
  * `apt-get update`
  * `apt-get upgrade`
  * `apt-get upgrade`
  * `do-release-upgrade`
* 软件包删除相关：
  * `apt-get remove`
  * `apt-get autoremove`
  * `aptitude remove`

当然也可以从另一个维度进行划分，`apt-get update`，`apt-get upgrade`，`apt-get dist-upgrade`，`apt-get remove`，`apt-get autoremove`都是`apt-get`命令使用不同参数，根据**掌握了man和-h就是掌握了所有Linux命令**这一原则，你只要能够敲出`man apt-get`，`man aptitude`就能了解这些命令的具体作用，而且是最权威、最即时的说明。我这里也只是对这行命令的manual做个归纳概括。

## 软件包更新升级

* `apt-get update`: 从`/etc/apt/sources`指定的软件源中重新同步软件包索引文件，这样就可以让我们知道哪些软件包有更新了。每次执行`apt-get upgrade`，`apt-get dist-upgrade`前都应该先执行`apt-get update`。
* `apt-get upgrade`: 系统将现有的软件包进行升级，如果有相依性的问题，而此相依性需要安装其它新的软件包或影响到其它软件包的相依性时，此软件包就不会被升级，会保留下来。
* `apt-get dist-upgrade`: 功能和`apt-get upgrade`类似，区别是可以解决相依性的问题，如果有相依性问题，需要安装/移除新的软件包，就会试着去安装/移除它。所以这个命令是有些风险的。例如软件包A原先依赖B/C/D，现在A依赖B/C/E。这种情况下，`apt-get dist-upgrade`会删除D安装E，并把A升级，而`apt-get upgrade`会认为依赖关系改变而拒绝升级A。
* `do-release-upgrade`: 是Ubuntu发行版自己提供的一个命令（它没有对应的man手册，但是可以通过<http://manpages.ubuntu.com/manpages/bionic/man8/do-release-upgrade.8.html>了解详细内容），比如当你想通过命令行将Ubuntu 18.04 LTS升级到Ubuntu 20.04 LTS，就可以使用这个命令。当然你也可以通过把/etc/apt/sources.list中的版本代号改掉，然后继续使用`apt-get update`+`apt-get dist-upgrade`来升级，但是这相对比较麻烦。

## 软件包删除

* `apt-get remove`的行为我们很好理解，就是删除某个包的同时，删除依赖于它的包，例如：A依赖于B，B依赖于C，`apt-get remove`删除B的同时，将删除A(很好理解，A依赖于B，B被删了，A也就无法正常运行了)。

* `apt-get autoremove`与`aptitude remove`效果相同，我们先了解下这两者的瓜葛：`apt-get`一开始并没有记录auto-install的信息，在06年的0.6.44.2exp1版本增加了类似于aptitude的auto-install记录(/var/lib/apt/extended_states)。此后，aptitude在07年的0.4.5.1版本转向使用apt-get的auto-install记录，而抛弃了自己原先的记录方式，再随后apt-get在07年的0.7.7版本增加了autoremove的选项。

依赖关系是一个复杂而交错的链条，我们把举几个例子来看看它们的行为。以下图中，绿色圆是为了满足依赖关系而apt-get或aptitude自动安装上的包，蓝色圆是管理员使用`apt-get install`或`aptitude install`手动安装的包。

### 例子1

1. C依赖于或推荐B软件包(apt-get和aptitude在安装软件时除了安装必要的依赖包，默认也会安装推荐的包)
2. B依赖于或推荐A，A被其他手动安装的包依赖

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210725160952042-1417840439.png)

* `apt-get remove C`将删除C，同时提示你用`apt-get autoremove`去清除B
* `apt-get autoremove C`将删除B，C
* `aptitude remove C`将删除B，C

删除C，那么B这个包既是自动安装的，且没有其他手动安装的包依赖于它，则可以判定B也是没必要的。

### 例子2

1. 在例子1的基础上，D依赖于或者推荐B，且D没有被其他手动安装的包依赖
这样的情况一般出现在用apt-get remove某个手动安装的包之后

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210725161024049-1957944143.png)

* `apt-get remove C`将删除C，同时提示你用`apt-get autoremove`去清除B，D
* `apt-get autoremove`C将删除B，C，D
* `aptitude remove C`将删除B，C，D

删除C，那么B，D这两个包既是自动安装的，且没有其他手动安装的包依赖于它们，则可以判定B，D也是没必要的。

### 例子3

1.在例子2的基础上，有个手动安装的包E推荐D(既E Recommends D，手动安装E时，也会把D装上)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210725161407635-132563814.png)

* `apt-get remove C`将删除C，同时提示你用`apt-get autoremove`去清除B，D
* `apt-get autoremove C`将删除B，C，D
* `aptitude remove C`将删除B，C，D

删除C，那么B，D这两个包既是自动安装的，且没有其他手动安装的包依赖于它们，则可以判定B，D也是没必要的，虽然D被E Recommend，但为啥是这么设计的，我也没猜出开发人员的想法。

### 例子4

1.在例子3的基础上，D变成依赖于B，E变成依赖于D

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210725161119892-1372692114.png)

* `apt-get remove C`将删除C
* `apt-get autoremove C`将删除C
* `aptitude remove C`将删除C

只删除C，因为B被D依赖，D被E依赖，间接来说，E不能没有B，D而正常运行，所以B，D被保留。

### 例子5

1.在例子4的基础上，D变成推荐B，E依然依赖于D

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210725161438557-691000730.png)

* `apt-get remove C`将删除C，同时提示你用`apt-get autoremove`去清除B
* `apt-get autoremove C`将删除B，C
* `aptitude remove C`将删除B，C

删除C，而B没有被其他手动安装的包直接依赖或者间接依赖(我指那些一层层depend on的关系)，D被E依赖，所以B不是必要的，可以删除，而D不能删除。
