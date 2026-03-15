# MySQL安装

## Ubunut安装/卸载Mysql（apg-get方式）

### 安装

```shell
jiangxin@db01:~$ sudo netstat -tap | grep mysql #查看是否系统中已经安装mysql
jiangxin@db01:~$ sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```

MySQL安装后的目录结构如下(此结构只针对于使用apt-get install 在线安装情况)：

* 数据库存放目录： /var/lib/mysql/
* 相关配置文件存放目录： /usr/share/mysql
* 相关命令存放目录： /usr/bin(mysqladmin mysqldump等命令)
* 启动脚步存放目录： /etc/rc.d/init.d/

### 卸载

```shell
jiangxin@db01:~$ ps aux | grep mysql
mysql     1942  3.5 14.8 1115880 150404 ?      Ssl  10:45   0:00 /usr/sbin/mysqld
jiangxin  1980  0.0  0.0  15984   948 pts/0    S+   10:45   0:00 grep --color=auto mysql
jiangxin@db01:~$ mysqladmin -u root -p shutdown
Enter password: 
jiangxin@db01:~$ ps aux | grep mysql
jiangxin  1984  0.0  0.0  15984   964 pts/0    S+   10:46   0:00 grep --color=auto mysql
jiangxin@db01:~$ sudo apt-get autoremove --purge mysql-*
...
jiangxin@db01:~$ dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P 
...
jiangxin@db01:~$ su – root
root@db01:~# rm -rf /var/lib/mysql
root@db01:~# rm -rf /etc/mysql
```

### MySQL简单管理

```shell
#启动MySQL服务
sudo service mysql start
#停止MySQL服务
sudo service mysql stop
#修改 MySQL 的管理员密码
sudo mysqladmin -u root password newpassword

#正常情况下，mysql占用的3306端口只是在IP 127.0.0.1上监听，拒绝了其他IP的访问。取消本地监听限制需要修改 mysqld.cnf 文件

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
# 找到此内容并且注释
bind-address = 127.0.0.1
```

使用mysql命令登录MySQL

```shell
# 对于mysql 8+版本，在ubuntu上安装mysql的时候root用户默认认证方式为auth_socket。
# 这个时候只有使用ubuntu的root账户登录时候才能够通过`mysql -u root`登录数据库进行配置操作。
jiangxin@db01:~$ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6
Server version: 5.7.17-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

## Ubuntu安装MySQL(安装包方式)

```shell
root@ubuntu:~# mkdir /usr/local/mysql
root@ubuntu:~# cd /usr/local/mysql/
root@ubuntu:/usr/local/mysql# groupadd mysql
root@ubuntu:/usr/local/mysql# useradd -r -g mysql -s /bin/false mysql
root@ubuntu:/usr/local/mysql# tar zxvf mysql-5.7.19-linux-glibc2.12-x86_64.tar.gz
root@ubuntu:/usr/local/mysql# cd mysql-5.7.19-linux-glibc2.12-x86_64/
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# mkdir mysql-files
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# chmod 750 mysql-files
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# chown -R mysql .
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# chgrp -R mysql .
# 安装过程中会生成一个随机密码，需要记录下来
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# bin/mysqld --initialize --user=mysql
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# bin/mysql_ssl_rsa_setup

# 添加环境变量
root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# sudo vim /etc/profile

export MYSQL_HOME=/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64
export PATH=$PATH:$MYSQL_HOME/bin

root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# source /etc/profile

root@ubuntu:/usr/local/mysql/mysql-5.7.19-linux-glibc2.12-x86_64# cd
root@ubuntu:~# mysqld_safe --user=mysql &
[1] 1931893
root@ubuntu:~# Logging to '/usr/local/mysql/data/ubuntu.err'.
2023-05-19T15:00:22.730000Z mysqld_safe Starting mysqld daemon with databases from /usr/local/mysql/data

root@ubuntu:~# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.19

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit
Bye
root@ubuntu:~# mysqladmin -uroot -p'/2jW>kFeerno' password test
mysqladmin: [Warning] Using a password on the command line interface can be insecure.
Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.
root@ubuntu:~# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.19 MySQL Community Server (GPL)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> select `user`, `host` from mysql.user;
+---------------+-----------+
| user          | host      |
+---------------+-----------+
| mysql.session | localhost |
| mysql.sys     | localhost |
| root          | localhost |
+---------------+-----------+
3 rows in set (0.00 sec)

mysql> update mysql.user set host = '%' where user = 'root';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
```

## Windows 10安装MySQL5.5 安装

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image177.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image178.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image179.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image180.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image181.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image182.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image183.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image184.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image185.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image186.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image187.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image188.jpg)

## MySQL常用语句

```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)
```

* INFORMATION_SCHEMA：提供了访问数据库元数据的方式。元数据是关于数据的数据，如数据库名、表名、列的数据类型或访问权限等。有些时候用于表述该信息的其他术语包括“数据词典”和“系统目录”。你可以讲INFORMATION_SCHEMA看成一个信息数据库，其中保存着关于MySQL服务器所维护的所有其他数据库的信息。在INFORMATION_SCHEMA中，有数个只读表。它们实际上是视图，而不是基本表，因此你将无法看到与之相关的任何文件。每位MySQL用户均有权访问这些表，但仅限于表中的特定行，在这类行中含有用户具有恰当访问权限的对象。
* PERFORMANCE_SCHEMA：主要用于收集数据库服务器性能参数。MySQL用户是不能创建存储引擎为PERFORMANCE_SCHEMA的表。performance_schema提供以下功能：提供进程等待的详细信息，包括锁、互斥变量、文件信息；保存历史的事件汇总信息，为提供MySQL服务器性能做出详细的判断；对于新增和删除监控事件点都非常容易，并可以随意改变mysql服务器的监控周期，例如（CYCLE、MICROSECOND）。通过以上得到的信息，DBA能够较明细得了解性能降低可能是由于哪些瓶颈。
* mysql：这个是mysql的核心数据库，类似于sql server中的master表，主要负责存储数据库的用户、权限设置、关键字等mysql自己需要使用的控制和管理信息。不可以删除，如果对mysql不是很了解，也不要轻易修改这个数据库里面的表信息。
* test：这个是安装时候创建的一个测试数据库，和它的名字一样，是一个完全的空数据库，没有任何表，可以删除。

## MySQL常见错误及其解决方式

### ERROR 1130: Host 10.0.0.1 is not allowed to connect to this MySQL server

在用远程连接MySQL服务器的数据库，不管怎么弄都是连接不到，错误代码是1130，ERROR 1130: Host 10.0.0.1 is not allowed to connect to this MySQL server
猜想是无法给远程连接的用户权限问题。结果这样子操作MySQL库，即可解决。在本机登入MySQL后，更改 “mysql” 数据库里的 “user” 表里的 “host” 项，从”localhost”改称'%'。

```SQL
mysql -u root -p
use mysql; 
select `Host`, `User` from `user` where `User` = 'root';
update user set host = '%' where user ='root'; 
flush privileges; 
select `Host`, `User` from `user` where `User` = 'root';
```

第一句是以权限用户root登录；第二句：选择mysql库；第三句：查看mysql库中的user表的host值；第四句：修改host值（以通配符%的内容增加主机/IP地址），当然也可以直接增加IP地址；第五句：刷新MySQL的系统权限相关表；第六句：再重新查看user表时。重启mysql服务即可完成。

### ERROR 1044 (42000):Access denied for user

这个问题主要是因为授权用户本身的权限不足引起的。我们以root用户为例，需要注意到地方有以下几个方面：

* MySQL的user表很重要。必须保证root用户在user表里面有两条记录，也就是
root localhost ……..
root 127.0.0.1 …….

* 保证root用户拥有所有权限,也就是user表里面的所有字段里面对应的内容是Y
* 在my.ini后者my.cnf里面有这个配置项的时候
bind-address=localhost
启用这个配置项可以保证安全

### Error: 1265 SQLSTATE: 01000 (WARN_DATA_TRUNCATED

* 字符长度太短；
* 乱码，更改统一的字符类型，比如更改字符类型为utf8；
* 如果是 Enum，则可能是添加的字符不在enum类型范围内；
* 另一可能是在alter table更改列设置时，影响原来存入的值，这时可将原值update为需要的类型值或删除这些原值再alter table

### error while loading shared libraries: libtinfo.so.5

ncurses包（ncurses-libs-5.6）已经安装，运行mysql时仍然提示：

mysql: error while loading shared libraries: libtinfo.so.5: cannot open shared object file: No such file or directory

此时只需要创建软连接即可，创建命令如下：

```shell
ln -s /usr/lib/libncurses.so.5 /lib/libtinfo.so.5
```

其中`libncurses.so.5`到底在哪个目录，不同的OS可能有所不同（比如SUSE X64就是在`/lib64`目录下），可以尝试使用`ldd mysql`命令查看mysql依赖的其它库在哪个目录，然后在对应目录查找是否有`libncurses.so.5`

### No curses/termcap library found

源码安装MySQL 5.1.30，在./configure阶段报错如下：

```
checking for tgetent in -lncurses... no
checking for tgetent in -lcurses... no
checking for tgetent in -ltermcap... no
checking for tgetent in -ltinfo... no
checking for termcap functions library... configure: error: No curses/termcap library found
```

原因是缺少ncurses的相关库，按照下面方式安装ncurses即可：

```sh
# RedHat系列
yum list|grep ncurses
yum -y install ncurses-devel
yum install ncurses-devel

# Debian系列
apt-cache search ncurses
apt-get install libncurses5-dev
```
