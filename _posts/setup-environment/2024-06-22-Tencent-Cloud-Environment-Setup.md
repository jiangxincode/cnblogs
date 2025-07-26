---
title: "腾讯云环境构建"
categories:
  - setup-environment
tags:
  - 环境搭建
  - 腾讯云
toc: true
---

## 开启root用户

```bash
ubuntu@ubuntu:~$ sudo passwd root
```

## 修改主机名

```bash
ubuntu@ubuntu:~$ sudo vim /etc/hostname
```

修改成ubuntu

```bash
ubuntu@ubuntu:~$ sudo reboot
```

## 调整SSH配置

```bash
# 注意是sshd_config，不是ssh_config
ubuntu@ubuntu:~$ sudo vim /etc/ssh/sshd_config
```

修改或者取消注释如下内容

```bash
# 允许root用户登录
PermitRootLogin yes

# 防止SSH经常断连
ClientAliveInterval 30
ClientAliveCountMax 86400
```

```bash
ubuntu@ubuntu:~$ sudo service ssh restart
```

## 安装JDK 17

```bash
ubuntu@ubuntu:/usr/local$ sudo mkdir java
ubuntu@ubuntu:/usr/local$ sudo chown ubuntu:ubuntu java
```

上传`jdk-8u371-linux-x64.tar.gz`到`java`目录

```bash
ubuntu@ubuntu:/usr/local$ cd java/
ubuntu@ubuntu:/usr/local/java$ tar -zxvf jdk-17_linux-x64_bin.tar.gz

ubuntu@ubuntu:/usr/local/java $ cd
ubuntu@ubuntu:~$ sudo vim /etc/profile
```

在文件末尾添加如下内容：

```bash
export JAVA_HOME=/usr/local/java/jdk-17.0.7
export PATH=$JAVA_HOME/bin:$PATH
```

```bash
ubuntu@ubuntu:~$ source /etc/profile
ubuntu@ubuntu:~$ java -version
java 17.0.7 2023-04-18 LTS
Java(TM) SE Runtime Environment (build 17.0.7+8-LTS-224)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.7+8-LTS-224, mixed mode, sharing)
```

## 安装Tomcat 8.5

ubuntu@ubuntu:/usr/local$ sudo mkdir tomcat
ubuntu@ubuntu:/usr/local$ sudo chown -R jiangxin:jiangxin tomcat
ubuntu@ubuntu:/usr/local$ cd tomcat/
ubuntu@ubuntu:/usr/local/tomcat$ tar -zxvf apache-tomcat-8.5.88.tar.gz
ubuntu@ubuntu:/usr/local/tomcat$ cd

ubuntu@ubuntu:~$ sudo vim /etc/profile

export CATALINA_BASE=/usr/local/tomcat/apache-tomcat-8.5.88
export CATALINA_HOME=/usr/local/tomcat/apache-tomcat-8.5.88
export PATH=$PATH:$CATALINA_HOME/lib:$CATALINA_HOME/bin

ubuntu@ubuntu:~$ source /etc/profile

本次会话启动tomcat
startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

后台启动tomcat
nohup startup.sh &

关闭tomcat
shutdown.sh

端口占用查询
sudo netstat -tulpn | grep 8080

进程查询
ps -ef | grep tomcat

在浏览器中访问下面地址，查看能否正常访问：

http://124.222.145.48:8080/

## 安装Tomcat 9

ubuntu@ubuntu:/usr/local$ sudo mkdir tomcat
ubuntu@ubuntu:/usr/local$ sudo chown -R jiangxin:jiangxin tomcat
ubuntu@ubuntu:/usr/local$ cd tomcat/
ubuntu@ubuntu:/usr/local/tomcat$ tar -zxvf apache-tomcat-9.0.75.tar.gz
ubuntu@ubuntu:/usr/local/tomcat$ cd

ubuntu@ubuntu:~$ sudo vim /etc/profile

export CATALINA_BASE=/usr/local/tomcat/apache-tomcat-9.0.75
export CATALINA_HOME=/usr/local/tomcat/apache-tomcat-9.0.75
export PATH=$PATH:$CATALINA_HOME/lib:$CATALINA_HOME/bin

ubuntu@ubuntu:~$ source /etc/profile

本次会话启动tomcat
startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

后台启动tomcat
nohup startup.sh &

关闭tomcat
shutdown.sh

端口占用查询
sudo netstat -tulpn | grep 8080

进程查询
ps -ef | grep tomcat

在浏览器中访问下面地址，查看能否正常访问：

http://124.222.145.48:8080/

## 安装Tomcat 10

ubuntu@ubuntu:/usr/local$ sudo mkdir tomcat
ubuntu@ubuntu:/usr/local$ sudo chown -R jiangxin:jiangxin tomcat
ubuntu@ubuntu:/usr/local$ cd tomcat/
ubuntu@ubuntu:/usr/local/tomcat$ tar -zxvf apache-tomcat-10.1.9.tar.gz
ubuntu@ubuntu:/usr/local/tomcat$ cd

ubuntu@ubuntu:~$ sudo vim /etc/profile

export CATALINA_BASE=/usr/local/tomcat/apache-tomcat-10.1.9
export CATALINA_HOME=/usr/local/tomcat/apache-tomcat-10.1.9
export PATH=$PATH:$CATALINA_HOME/lib:$CATALINA_HOME/bin

ubuntu@ubuntu:~$ source /etc/profile

本次会话启动tomcat
startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

后台启动tomcat
nohup startup.sh &

关闭tomcat
shutdown.sh

端口占用查询
sudo netstat -tulpn | grep 8080

进程查询
ps -ef | grep tomcat

在浏览器中访问下面地址，查看能否正常访问：

http://124.222.145.48:8080/

## 安装MySQL

参考前文

## 部署项目

war包放到$CATALINA_HOME/webapps/目录下，然后重启tomcat
shutdown.sh; startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

http://124.222.145.48:8080/java-web-test/index.jsp

## 安装Apache

安装Apache作为HTTP文件下载服务器

```bash
ubuntu@ubuntu:~$ sudo apt-get install apache2
```

尝试启动Apache2服务

```bash
ubuntu@ubuntu:~$ /etc/init.d/apache2 start
Starting apache2 (via systemctl): apache2.service==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to start 'apache2.service'.
Authenticating as: qcloud (ubuntu)
Password:
==== AUTHENTICATION COMPLETE ===
.
```

直接访问<http://124.222.145.48:80/>，既可看到对应的Apache2默认页面。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2025-07-26_12-25-59.png)

存放的目录为`/var/www/html/`，想要下载的文件直接放到这个目录下，然后直接访问既可。

<http://124.222.145.48/download/>

```bash

命令汇总

```bash
# 启动Apache2服务
/etc/init.d/apache2 start

# 查看Apache2服务状态
/etc/init.d/apache2 status

# 停止Apache2服务
/etc/init.d/apache2 stop

# 重启Apache2服务
/etc/init.d/apache2 restart
```
