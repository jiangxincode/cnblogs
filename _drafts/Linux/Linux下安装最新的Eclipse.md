
测试环境：

* OS：Ubuntu 14.04
* Eclipse：Eclipse Kepler (4.3.2)
* JDK：

Ubuntu软件源中提供的Eclipse版本太老了，下面介绍如何在Ubuntu 14.04下安装Eclipse Kepler (4.3.2)。其它Linux和Eclipse版本的安装也可参考本文。

* 如果系统中存在OpenJDK或者其它版本的Oracle JDK，需要首先将他们删除（如果你对它们的安装目录以及对应关系非常清晰，也可以在不删除的情况下安装成功）。

    sudo apt-get purge openjdk*

* 添加 PPA 源

    sudo add-apt-repository ppa:webupd8team/java

* 更新源数据库

    sudo apt-get update

* 安装 Oracle Java 7

    sudo apt-get install oracle-java7-installer

* 下载 Eclipse 最新版

    访问官方网站下载需要的 Eclipse 版本：http://www.eclipse.org/downloads/?osType=linux&release=undefined

* 解压 Eclipse

    cd /opt/ && sudo tar -zxvf ~/Downloads/eclipse-*.tar.gz

* 创建 Eclipse 快捷方式

    在/usr/share/applications/下创建文件eclipse.desktop，并添加如下内容：
  
    [Desktop Entry]
    Name=Eclipse 4
    Type=Application
    Exec=/opt/eclipse/eclipse
    Terminal=false
    Icon=/opt/eclipse/icon.xpm
    Comment=Integrated Development Environment
    NoDisplay=false
    Categories=Development;IDE;
    Name[en]=Eclipse