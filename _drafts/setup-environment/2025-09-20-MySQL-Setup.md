# MySQL安装

## Ubunut安装/卸载Mysql（apg-get方式）

### 安装

```shell
jiangxin@db01:~$ uname -a #查看内核和操作系统信息
Linux db01 4.4.0-66-generic #87-Ubuntu SMP Fri Mar 3 15:29:05 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
jiangxin@db01:~$ head -n 1 /etc/issue #查看Linux发行版信息
Ubuntu 16.04.1 LTS \n \l
jiangxin@db01:~$ sudo netstat -tap | grep mysql #查看是否系统中已经安装mysql
jiangxin@db01:~$ sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```

安装过程中会要求输入mysql的root账号密码，如下所示：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image102.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image103.png)

```shell
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