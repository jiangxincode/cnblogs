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