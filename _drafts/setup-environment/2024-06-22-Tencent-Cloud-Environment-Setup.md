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

## 安装JDK

略

## 安装Tomcat

略

## 安装MySQL

略

## 部署项目

war包放到$CATALINA_HOME/webapps/目录下，然后重启tomcat
shutdown.sh; startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

http://124.222.145.48:8080/java-web-test/index.jsp

## 安装Apache

略
