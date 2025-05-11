
## 漏洞介绍
国外的研究人员zero thoughts发现了一个Spring框架的反序列化远程代码执行漏洞。
spring-tx.jar包中的org.springframework.transaction.jta.JtaTransactionManager类存在JNDI反序列化问题。只要创建一个JtaTransactionManager 对象让userTransactionName指向我们注册的RMI链接（如rmi://x.x.x.x:1099/Object）然后将对象发送到有漏洞的服务器，即可执行远程命令。具体细节可以分析漏洞作者的POC代码。
漏洞发现者的博客
http://zerothoughts.tumblr.com/post/137769010389/fun-with-jndi-remote-code-injection

## 漏洞影响
受影响漏洞服务器主要需要满足如下条件：
1. CLASSPATH 中包含了 spring-tx.jar，spring-commons.jar，javax.transaction-api.jar
2. 存在反序列化接口如RMI, JMS, IIOP等
出现漏洞的关键jar包 spring-tx.jar，并不是spring最基本的包，默认并不使用，所以并不是所有使用了spring框架的应用都受影响，需要具体检查是否包含了spring-tx.jar包。

## POC简要复现

### 环境描述：
Java环境——这里使用的是JDK1.7版本
Maven环境——见下面的maven包 apache-maven-3.3.9-bin.zip
Spring漏洞利用POC——spring-jndi-master.zip

### 环境搭建：
1. Java环境安装，略
2. Maven安装
直接解压apache-maven-3.3.9-bin.zip ，添加环境变量，然后用mvn –v测试是否安装成功
如我的maven路径：C:\java\apache-maven-3.3.9
添加环境变量：
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202821982-69117379.jpg)

![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204518857-1749610613.jpg)




Mvn –v测试
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202836779-545034073.jpg)


### 服务器搭建：
Poc里面有两个文件夹server和client
Server用于搭建包含spring的服务器环境，client用于构建反序列化对象并发送给server
服务器搭建命令如下
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204558763-1304386556.jpg)


首先进入server目录
然后用mvn install安装spring环境
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204631747-497529942.jpg)


Mvn就是开始安装的maven，server目录下有pom.xml文件。 Mvn install会根据里面的内容来下载安装spring等组件。 最后会将jar包放到target中。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202851997-113319886.jpg)


java -cp “target/*” ExploitableServer 9999命令在9999端口起到有漏洞的服务器程序。
ExploitableServer.java比较简单，创建socket等待连接，读取对象。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202905060-1768836079.jpg)


这样便开启了一个连接
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204710263-796332784.jpg)



### 客户端攻击对象构建：
命令与上面相似：
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204733497-644156748.jpg)


进入目录，安装spring组件，调用代码向服务器发送指令。
Mvn install，客户端也需要安装spring的组件，来使得客户端的java代码能够构造spring对象。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202924732-1594908968.jpg)


java -cp “target/*” ExploitClient 127.0.0.1 9999 127.0.0.1
“target/* 指定spring路径
ExploitClient 为客户端的main程序
127.0.0.1 9999 127.0.0.1三个参数分别对应为
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204820310-1583787682.jpg)


客户端包含三个文件
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722204840544-827705142.jpg)


ExploitClient是主程序，包含序列化的过程，一些主要出现漏洞的类，以及数据的发送。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722202947466-1449976164.jpg)


HttpFileHandler 主要是构建字节流
ExportObject 是功能代码，构建自己的java代码，服务器有权限就能执行。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722203002966-1760284078.jpg)


### 执行结果：
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722203016904-1695498001.jpg)


### 自检与修复：
由于主要出现漏洞的地方在于Spring-tx.jar包的JtaTransactionManager类中。 可以检测项目中是否有使用spring-tx.jar包。如果有使用可以对JtaTransactionManager类进行重写。同时有防火墙的用户可以先对数据包中的JtaTransactionManager数据进行过滤，直到源码修复。
POC网络传输数据如下，可以先对使用了JtaTransactionManager的报文进行拦截。
![](http://images2015.cnblogs.com/blog/611264/201607/611264-20160722203027982-33447734.jpg)