---
title: "Aloys的环境搭建手册"
categories:
  - setup-environment
tags:
  - 环境搭建
toc: true
---


## Ubuntu 16.04安装SQLLite3

```shell
jiangxin@db01:~$ sudo apt-get install sqlite3
jiangxin@db01:~$ sqlite3 test.db
SQLite version 3.11.0 2016-02-15 17:29:24
Enter ".help" for usage hints.
sqlite> create table mytable(id integer primary key, value text);
sqlite> insert into mytable(id, value) values(1, 'Micheal');
sqlite> select * from mytable;
1|Micheal
sqlite> .help
.backup ?DB? FILE      Backup DB (default "main") to FILE
.bail on|off           Stop after hitting an error.  Default OFF
.binary on|off         Turn binary output on or off.  Default OFF
.changes on|off        Show number of rows changed by SQL
.clone NEWDB           Clone data into NEWDB from the existing database
.databases             List names and files of attached databases
.dbinfo ?DB?           Show status information about the database
.dump ?TABLE? ...      Dump the database in an SQL text format
                         If TABLE specified, only dump tables matching
                         LIKE pattern TABLE.
.echo on|off           Turn command echo on or off
.eqp on|off            Enable or disable automatic EXPLAIN QUERY PLAN
.exit                  Exit this program
.explain ?on|off|auto? Turn EXPLAIN output mode on or off or to automatic
.fullschema            Show schema and the content of sqlite_stat tables
.headers on|off        Turn display of headers on or off
.help                  Show this message
.import FILE TABLE     Import data from FILE into TABLE
.indexes ?TABLE?       Show names of all indexes
                         If TABLE specified, only show indexes for tables
                         matching LIKE pattern TABLE.
.limit ?LIMIT? ?VAL?   Display or change the value of an SQLITE_LIMIT
.load FILE ?ENTRY?     Load an extension library
.log FILE|off          Turn logging on or off.  FILE can be stderr/stdout
.mode MODE ?TABLE?     Set output mode where MODE is one of:
                         ascii    Columns/rows delimited by 0x1F and 0x1E
                         csv      Comma-separated values
                         column   Left-aligned columns.  (See .width)
                         html     HTML <table> code
                         insert   SQL insert statements for TABLE
                         line     One value per line
                         list     Values delimited by .separator strings
                         tabs     Tab-separated values
                         tcl      TCL list elements
.nullvalue STRING      Use STRING in place of NULL values
.once FILENAME         Output for the next SQL command only to FILENAME
.open ?FILENAME?       Close existing database and reopen FILENAME
.output ?FILENAME?     Send output to FILENAME or stdout
.print STRING...       Print literal STRING
.prompt MAIN CONTINUE  Replace the standard prompts
.quit                  Exit this program
.read FILENAME         Execute SQL in FILENAME
.restore ?DB? FILE     Restore content of DB (default "main") from FILE
.save FILE             Write in-memory database into FILE
.scanstats on|off      Turn sqlite3_stmt_scanstatus() metrics on or off
.schema ?TABLE?        Show the CREATE statements
                         If TABLE specified, only show tables matching
                         LIKE pattern TABLE.
.separator COL ?ROW?   Change the column separator and optionally the row
                         separator for both the output mode and .import
.shell CMD ARGS...     Run CMD ARGS... in a system shell
.show                  Show the current values for various settings
.stats on|off          Turn stats on or off
.system CMD ARGS...    Run CMD ARGS... in a system shell
.tables ?TABLE?        List names of tables
                         If TABLE specified, only list tables matching
                         LIKE pattern TABLE.
.timeout MS            Try opening locked tables for MS milliseconds
.timer on|off          Turn SQL timer on or off
.trace FILE|off        Output each SQL statement as it is run
.vfsinfo ?AUX?         Information about the top-level VFS
.vfslist               List all available VFSes
.vfsname ?AUX?         Print the name of the VFS stack
.width NUM1 NUM2 ...   Set column widths for "column" mode
                         Negative values right-justify
sqlite> .quit
jiangxin@db01:~$\
```

由于Sqlite本身不支持远程访问，如果需要在Windows上连接远程Linux上的Sqlite，需要在Linux上共享文件给Windows。
共享方式见：
Ubuntu创建共享文件夹并支持Windows访问：http://jingyan.baidu.com/article/2fb0ba40a8283500f2ec5f35.html


在Windows上打开资源浏览器，在输入框输入\\192.168.1.150
然后输入用户名、密码即可

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image104.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image105.png)

将之前创建的test.db移到share/sqlite目录：

jiangxin@db01:~$ mv test.db share/sqlite/

在Windows上用dbeaver连接Linux上的远程数据库

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image106.png)

## 安装Prometheus
下载地址：
https://prometheus.io/download/

jiangxin@tomcat:~$ sudo mkdir /usr/local/prometheus
jiangxin@tomcat:~$ sudo chown -R jiangxin:jiangxin /usr/local/prometheus
jiangxin@tomcat:~$ cd /usr/local/prometheus/
jiangxin@tomcat:/usr/local/prometheus$ ls
prometheus-1.7.1.linux-amd64.tar.gz
jiangxin@tomcat:/usr/local/prometheus$ tar -zxvf prometheus-1.7.1.linux-amd64.tar.gz
jiangxin@tomcat:/usr/local/prometheus$ cd prometheus-1.7.1.linux-amd64/

jiangxin@tomcat:/usr/local/prometheus/prometheus-1.7.1.linux-amd64$ sudo vim /etc/profile

export PROMETHEUS_HOME=/usr/local/prometheus/prometheus-1.7.1.linux-amd64
export PATH=$PATH:$PROMETHEUS_HOME

jiangxin@tomcat:/usr/local/prometheus/prometheus-1.7.1.linux-amd64$ source /etc/profile
jiangxin@tomcat:/usr/local/prometheus/prometheus-1.7.1.linux-amd64$ cd
### 启动
jiangxin@tomcat:~$ prometheus -config.file=${PROMETHEUS_HOME}/prometheus.yml
INFO[0000] Starting prometheus (version=1.7.1, branch=master, revision=3afb3fffa3a29c3de865e1172fb740442e9d0133)  source="main.go:88"
INFO[0000] Build context (go=go1.8.3, user=root@0aa1b7fc430d, date=20170612-11:44:05)  source="main.go:89"
INFO[0000] Host details (Linux 4.4.0-78-generic #99-Ubuntu SMP Thu Apr 27 15:29:09 UTC 2017 x86_64 tomcat (none))  source="main.go:90"
INFO[0000] Loading configuration file /usr/local/prometheus/prometheus-1.7.1.linux-amd64/prometheus.yml  source="main.go:252"
INFO[0000] Loading series map and head chunks...         source="storage.go:428"
INFO[0000] 0 series loaded.                              source="storage.go:439"
INFO[0000] Starting target manager...                    source="targetmanager.go:63"
INFO[0000] Listening on :9090                            source="web.go:259"




### 查看界面
http://192.168.1.130:9090/metrics

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image189.png)



http://192.168.1.130:9090/graph

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image190.png)

## Windows 10系统下搭建Jenkins环境

主要参考：
http://www.cnblogs.com/edward2013/p/5269465.html
但是没有安装ant，而且java、maven、tomcat都是使用的压缩包方式安装。

## 配置AOSP源码查看环境

### 在Windows上安装Repo，同步AOSP代码【不推荐】

第一个想到的方案是在Windows上配置Repo，然后下载AOSP源码，参考：
Windows安装repo的真正解决方案：https://ysy950803.blog.csdn.net/article/details/104188793
但是就像Repo官网（https://gerrit.googlesource.com/git-repo/+/HEAD/docs/windows.md）说的那样：
Repo is primarily developed on Linux with a lot of users on macOS. Windows is, unfortunately, not a common platform. There is support in repo for Windows, but there might be some rough edges.
Keep in mind that Windows in general is “best effort” and “community supported”. That means we don't actively test or verify behavior, but rely heavily on users to report problems back to us, and to contribute fixes as needed.
Windows版的Repo虽然可用，但是可能会出现各种各样的问题，这些问题可能会让我们在解决环境问题上分心过多，所以不推荐这种方式。

### 在Linux上安装Repo，同步AOSP代码【推荐】

根据实际情况有两种工作模式：
1、	Linux作为AOSP代码的同步、存储、查看、修改、编译环境，大部分工作都是在Linux上完成，Android Studio也是安装在Linux上，这种我觉得是最完美的模式。但是要求Linux的性能足够好。由于我这边没有实际的Linux机器，是在Windows上用虚拟机配置的Linux环境，所以没有采用这种方法。
2、	Linux作为AOSP代码的同步、存储、编译环境，查看和修改工作在Windows上完成，具体的实现方式有两种：
a)	用Samba服务器把Linux上的AOSP代码共享到Windows平台，然后在Windows平台上安装IDE环境，直接打开远程AOSP代码目录，查看和修改，这种方式的优点是配置简单，不用代码同步。但是我这边网速一般，而AOSP代码量太大，导致Android Studio经常卡死，所以我也放弃了这种方式。
b)	将android.iml/android.ipr以及常用的仓（比如frameworks/base frameworks/native等）使用rsync等工具同步到Windows平台，然后在Windows上使用Android Studio导入，进行查看和修改，修改完成后通过Beyondcompare工具将修改的内容同步到Linux平台进行编译等工作。这个各方面折中的方案。后续主要介绍这种工作环境的配置。

#### 安装配置Linux环境

如果已经有Linux机器，本步骤省略。我采用在Windows上安装虚拟机，然后通过虚拟机安装Linux（Ubuntu）。
同时按需安装Git/Vim/OpenSSH Server等工具，安装方式不再赘述，网上有很多。

#### 下载AOSP源码

在配置好的Linux环境中下载AOSP源码，Google官方的下载AOSP源码的方式：https://source.android.com/docs/setup/build/downloading。
但是由于墙的原因，这种方式不容易实现，所以推荐使用清华的镜像，使用指导：https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/。
Repo的使用方式可以参考：Repo实践指南：https://www.cnblogs.com/jiangxinnju/p/14274982.html

#### 配置Windows上的工具
1、	安装SSH客户端工具，这里推荐MobaXTerm，因为它不仅免费还自带了rsync命令行工具，可以非常方便从Linux上同步代码到Windows。
a)	mkdir -p /drives/d/Code/sync/aosp/frameworks
b)	rsync -az --progress --delete --exclude=".git" android@192.168.1.125:/home/android/aosp/frameworks/base /drives/d/Code/sync/aosp/frameworks/
c)	rsync -az --progress --delete --exclude=".git" android@192.168.1.125:/home/android/aosp/frameworks/native /drives/d/Code/sync/aosp/frameworks/
2、	安装BeyondCompare工具，方便对比，将修改的代码同步到Linux环境。
3、	安装Android Sudio，将AOSP源码导入到Android Studio进行查看：https://www.cnblogs.com/jiangxinnju/p/14426645.html
4、	安装Source Insight工具，AS查看AOSP的Java代码比较合适，但是C/C++代码不支持跳转，着色也比较差，看这部分代码还是SI比较好用。

## TensorFlow环境搭建

### 预备条件
	Ubuntu 22.04.2 LTS
	配置好固定IP，安装SSH(Server)/Samba等基础网络连接软件

