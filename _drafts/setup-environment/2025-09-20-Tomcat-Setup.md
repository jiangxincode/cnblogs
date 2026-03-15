# Tomcat安装

## 安装Tomcat 11

```shell
ubuntu@ubuntu:/usr/local$ sudo mkdir tomcat
ubuntu@ubuntu:/usr/local$ sudo chown -R ubuntu:ubuntu tomcat
ubuntu@ubuntu:/usr/local$ cd tomcat/
# 下载对应版本的tomcat，例如apache-tomcat-11.0.11.tar.gz
ubuntu@ubuntu:/usr/local/tomcat$ tar -zxvf apache-tomcat-11.0.11.tar.gz
```

在`/etc/profile`中添加环境变量

```shell
export CATALINA_BASE=/usr/local/tomcat/apache-tomcat-11.0.11
export CATALINA_HOME=/usr/local/tomcat/apache-tomcat-11.0.11
export PATH=$PATH:$CATALINA_HOME/lib:$CATALINA_HOME/bin
```

```shell
ubuntu@ubuntu:/usr/local/tomcat$ cd
ubuntu@ubuntu:~$ source /etc/profile
```

后台启动tomcat，且终端退出仍能正常运行: `nohup startup.sh &`
关闭tomcat: `shutdown.sh`
查看启动日志: `tail -f $CATALINA_HOME/logs/catalina.out`
端口占用查询: `sudo netstat -tulpn | grep 8080`
进程查询: `ps -ef | grep tomcat`

在浏览器中访问下面地址，查看能否正常访问：<http://124.222.145.48:8080/>

将要部署的war包放到$CATALINA_HOME/webapps/目录下，然后重启tomcat
shutdown.sh; startup.sh ; tail -f $CATALINA_HOME/logs/catalina.out

http://124.222.145.48:8080/java-web-test/index.jsp
