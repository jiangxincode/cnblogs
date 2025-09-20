Windows信息：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image001.png)

将要配置的集群信息：
利用Virtualbox，安装三台Ubuntu 16.04.1版本的虚拟机，其中一台担任DataNode、SecondaryNameNode、ResourceManager的角色，另外两台担任DataNode、NodeManager的角色。具体组网如下：

主机名|IP|掩码|网关|DNS服务器|角色
---|---|---|---|---|---
DESKTOP-LSB0HI4|192.168.1.100|255.255.255.0|192.168.1.1|114.114.114.114|主机
Ubuntu-01|192.168.1.160|255.255.255.0|192.168.1.1|114.114.114.114|DataNode/SecondaryNameNode/ResourceManager/master/worker/zookeeper/HMaster/hive/pig
Ubuntu-02|192.168.1.170|255.255.255.0|192.168.1.1|114.114.114.114|DataNode/NodeManager/worker/zookeeper/HRegion
Ubuntu-03|192.168.1.180|255.255.255.0|192.168.1.1|114.114.114.114|DataNode/NodeManager/ worker/zookeeper/HRegion

## 安装VirtualBox

首先需要在主机中安装虚拟机VirtualBox，此次我安装的版本为VirtualBox-5.1.14-112924-Win。

下载地址：<https://www.virtualbox.org/>

单机VirtualBox-5.1.14-112924-Win.exe，按照所给的说明进行安装：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image002.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image003.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image004.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image005.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image006.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image007.png)


## 安装Linux(Ubuntu)

安装Virtualbox之后，需要在其中安装Linux服务器。我使用的Linux发行版本为：ubuntu-16.04.1-desktop-amd64。

下载地址：<https://www.ubuntu.com/download>

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image008.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image009.png)

此处需要为虚拟机分配内存大小，建议内存充足的朋友多分配一些。此处我分配了512MB内存，但是之后又修改为1024MB。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image010.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image011.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image012.png)

此处需要分配虚拟机的硬盘容量，请硬盘容量充足的朋友多分配一些。另外虚拟硬盘最好存储在SSD这样的高速存取设备上，提升虚拟机相应速度。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image013.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image014.png)

将共享剪贴板和拖放功能均选为双向：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image015.png)

此处将虚拟机内存修改为1024MB。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image016.png)

点击右侧的关盘图标，选择我们之前下载的ubuntu-16.04.1-desktop-amd64.iso

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image017.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image018.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image019.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image020.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image021.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image022.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image023.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image024.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image025.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image026.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image027.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image028.png)


## 复制虚拟机

安装Ubuntu-16.04.1-01之后，复制该虚拟机，创建Ubuntu-16.04.1-02、Ubuntu-16.04.1-03

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image029.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image030.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image031.png)

复制之后效果如下图：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image032.png)

## 配置各个虚拟机

```shell
hadoop@Ubuntu-01:~$ sudo apt-get install lrzsz
hadoop@Ubuntu-01:~$ sudo apt-get install vim
```

### 配置网络

将服务器的IP分配方式改为固定IP，点击系统设置-网络-选项-IPv4设置。按照下图进行设置。注意不要忘了DNS服务器的配置，否则会导致虚拟机无法上外网。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image033.png)
配置完网络之后，尝试主机和虚拟机互相ping，如果均能ping同则说明网络配置正常。否则需要检查防火墙等配置。此次安装过程中，主机可以ping通虚拟机，但是虚拟机无法ping通主机。关闭Windows机器防火墙后，问题解决。


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image034.png)

### 安装openssh-server

为了之后方便主机与虚拟机之间，以及各个虚拟机之间方便通讯，需要在虚拟机中安装openssh-server。（Ubuntu默认已经安装SSH Client）

```shell
sudo apt-get install openssh-server
```

安装之后就可以在Windows主机上利用XShell登陆各个虚拟机。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image035.png)


### 开启root用户

在之后的某些操作中（比如文件传输）经常需要root用户，但是Ubuntu默认是不开启root用户的，使用下面的命令进行开启：
sudo passwd root

### 修改主机名

复制的虚拟机的主机名均为Ubuntu-01，但为了以后集群中能够容易分辨各台服务器，需要给每台机器取个不同的名字。机器名由 /etc/hostname文件决定。
sudo vim /etc/hostname

在三台虚拟机上，分别配置为：
Ubuntu-01
Ubuntu-02
Ubuntu-03
重启三台虚拟机（sudo reboot），重新利用XShell进行登录，效果如下：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image036.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image037.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image038.png)

### 修改hosts

为了让主机与各个虚拟机以及各个虚拟机之间通讯更加方便，需要配置主机和三台虚拟机的hosts文件：

Windows主机（C:\windows\system32\drivers\etc）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image039.png)

Ubuntu-01（/etc/hosts）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image040.png)

Ubuntu-02（/etc/hosts）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image041.png)

Ubuntu-03（/etc/hosts）

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image042.png)



修改之前效果：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image043.png)


修改之后效果：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image044.png)

### 创建hadoop用户组和用户

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image045.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image046.png)

另外还需要给hadoop用户添加权限，打开/etc/sudoers文件，在root   ALL=(ALL:ALL)   ALL下添加hadoop   ALL=(ALL:ALL)  ALL， 
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image047.png)

创建hadoop用户之后，su到hadoop用户，进行后续操作。本文之后的所有操作，如无特殊说明均是指在hadoop用户下。

### 配置ssh免登陆

为了完成分布式计算系统，需要三台机器相互之间可以无密码访问（或者是master可以无密码访问2个slave）。
在个人目录/home/hadoop下新建.ssh文件夹，在.ssh中执行
`ssh-keygen -t rsa`
系统会问你一些配置，由于是初次实验，不需要这些内容，点回车继续下去即可。完成后会在.ssh/下生成id_rsa和id_rsa.pub两个文件，三台机器做同样处理。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image048.png)


接下来把它们的密钥相互交换，这样做的目的是把Ubuntu-01的密钥交给Ubuntu-02和Ubuntu-03，对Ubuntu-02和Ubuntu-03做同样处理，完成后每一个机器的/.ssh/中应该有3个密钥，一个是自己的，另两个是别人的。


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image049.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image050.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image051.png)

把自己的密钥连同别人的两个密钥加到授权密钥中

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image052.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image053.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image054.png)



接下来检验相互之间是否可以通过ssh实现无密码访问
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image055.png)

访问成功会显示欢迎信息，初次访问需要yes，之后就可以不直接访问了。

### 安装JDK

略

## 安装Hadoop

```shell
cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir hadoop
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop hadoop/

hadoop@Ubuntu-01:/usr/local$ cd hadoop/
hadoop@Ubuntu-01:/usr/local/hadoop$ tar -xzvf hadoop-2.7.3.tar.gz
hadoop@Ubuntu-01:/usr/local/hadoop$ rm hadoop-2.7.3.tar.gz

hadoop@Ubuntu-01:/usr/local/hadoop$ sudo vim /etc/profile

export HADOOP_HOME=/usr/local/hadoop/hadoop-2.7.3
export PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH

hadoop@Ubuntu-01:/usr/local/hadoop$ source /etc/profile
```

### 修改Hadoop配置文件

Hadoop配置文件均在/usr/local/hadoop/hadoop-2.7.3/etc/hadoop 下

#### hadoop-env.sh
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image059.png)

虽然已经在/etc/profile中设置了JAVA_HOME环境变量，但是此处仍然要进行配置。

#### yarn-env.sh
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image060.png)

由于已经设置了JAVA_HOME环境变量，此处可以不设置

#### slaves
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image061.png)

#### core-site.xml

```xml
<configuration>
 <property>
  <name>fs.defaultFS</name>
  <value>hdfs://Ubuntu-01:9000</value>
 </property>
 <property>
  <name>io.file.buffer.size</name>
  <value>131072</value>
 </property>
 <property>
  <name>hadoop.tmp.dir</name>
  <value>file:/usr/local/hadoop/hadoop-2.7.3/tmp</value>
  <description>Abasefor other temporary directories.</description>
 </property>
 <property>
  <name>hadoop.proxyuser.spark.hosts</name>
  <value>*</value>
 </property>
<property>
  <name>hadoop.proxyuser.spark.groups</name>
  <value>*</value>
 </property>
</configuration>
```

#### hdfs-site.xml

```xml
<configuration>

<property>
  <name>dfs.namenode.secondary.http-address</name>
  <value>Ubuntu-01:9001</value>
 </property>

  <property>
   <name>dfs.namenode.name.dir</name>
   <value>file:/usr/local/hadoop/hadoop-2.7.3/name</value>
 </property>

 <property>
  <name>dfs.datanode.data.dir</name>
  <value>file:/usr/local/hadoop/hadoop-2.7.3/tmp</value>
  </property>

 <property>
  <name>dfs.replication</name>
  <value>2</value>
 </property>

 <property>
  <name>dfs.webhdfs.enabled</name>
  <value>true</value>
 </property>

</configuration>
```

#### mapred-site.xml

```xml
<configuration>
 <property>
   <name>mapreduce.framework.name</name>
   <value>yarn</value>
 </property>
 <property>
  <name>mapreduce.jobhistory.address</name>
  <value>Ubuntu-01:10020</value>
 </property>
 <property>
  <name>mapreduce.jobhistory.webapp.address</name>
  <value>Ubuntu-01:19888</value>
 </property>


</configuration>
```

#### yarn-site.xml

```xml
<property>
   <name>yarn.nodemanager.aux-services</name>
   <value>mapreduce_shuffle</value>
  </property>
  <property>
   <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
   <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
  <property>
   <name>yarn.resourcemanager.address</name>
   <value>Ubuntu-01:8032</value>
  </property>
  <property>
   <name>yarn.resourcemanager.scheduler.address</name>
   <value>Ubuntu-01:8030</value>
  </property>
  <property>
   <name>yarn.resourcemanager.resource-tracker.address</name>
   <value>Ubuntu-01:8035</value>
  </property>
  <property>
   <name>yarn.resourcemanager.admin.address</name>
   <value>Ubuntu-01:8033</value>
  </property>
  <property>
   <name>yarn.resourcemanager.webapp.address</name>
   <value>Ubuntu-01:8088</value>
  </property>
  <property>
   <name>yarn.resourcemanager.hostname</name>
   <value>192.168.0.160</value>
  </property>

</configuration>
```

#### 将配置好的hadoop文件copy到另一台slave机器上

```shell
hadoop@Ubuntu-01:/usr/local/hadoop$ scp -r hadoop-2.7.3/ hadoop@Ubuntu-02:/usr/local/hadoop/
hadoop@Ubuntu-01:/usr/local/hadoop$ scp -r hadoop-2.7.3/ hadoop@Ubuntu-03:/usr/local/hadoop/
```


### 验证

#### 格式化namenode

```shell
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ hdfs namenode -format
17/02/12 14:00:27 INFO namenode.NameNode: STARTUP_MSG: 
/************************************************************
STARTUP_MSG: Starting NameNode
STARTUP_MSG:   host = Ubuntu-01/127.0.1.1
STARTUP_MSG:   args = [-format]
STARTUP_MSG:   version = 2.7.3
...
STARTUP_MSG:   build = https://git-wip-us.apache.org/repos/asf/hadoop.git -r baa91f7c6bc9cb92be5982de4719c1c8af91ccff; compiled by 'root' on 2016-08-18T01:41Z
STARTUP_MSG:   java = 1.8.0_121
************************************************************/
17/02/12 14:00:27 INFO namenode.NameNode: registered UNIX signal handlers for [TERM, HUP, INT]
...
17/02/12 14:00:33 INFO namenode.NameNode: SHUTDOWN_MSG: 
/************************************************************
SHUTDOWN_MSG: Shutting down NameNode at Ubuntu-01/127.0.1.1
************************************************************/
```


#### 启动hdfs

```shell
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ start-dfs.sh 
Starting namenodes on [Ubuntu-01]
Ubuntu-01: starting namenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-namenode-Ubuntu-01.out
Ubuntu-03: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-03.out
Ubuntu-02: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-02.out
Starting secondary namenodes [Ubuntu-01]
Ubuntu-01: starting secondarynamenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-secondarynamenode-Ubuntu-01.out
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ jps
9466 Jps
9147 NameNode
9357 SecondaryNameNode
```

#### 停止hdfs

```shell
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ stop-dfs.sh 
Stopping namenodes on [Ubuntu-01]
Ubuntu-01: stopping namenode
Ubuntu-02: stopping datanode
Ubuntu-03: stopping datanode
Stopping secondary namenodes [Ubuntu-01]
Ubuntu-01: stopping secondarynamenode
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ jps
9814 Jps
```

#### 启动yarn

```shell
hadoop@Ubuntu-01:~$ start-yarn.sh 
starting yarn daemons
starting resourcemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-resourcemanager-Ubuntu-01.out
Ubuntu-02: starting nodemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-nodemanager-Ubuntu-02.out
Ubuntu-03: starting nodemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-nodemanager-Ubuntu-03.out
hadoop@Ubuntu-01:~$ jps
6252 ResourceManager
6509 Jps
```

#### 停止yarn

```shell
hadoop@Ubuntu-01:~$ stop-yarn.sh 
stopping yarn daemons
stopping resourcemanager
Ubuntu-03: stopping nodemanager
Ubuntu-02: stopping nodemanager
Ubuntu-03: nodemanager did not stop gracefully after 5 seconds: killing with kill -9
Ubuntu-02: nodemanager did not stop gracefully after 5 seconds: killing with kill -9
no proxyserver to stop
```

#### 查看集群状态

```shell
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ hdfs dfsadmin -report
report: Call From Ubuntu-01/127.0.1.1 to Ubuntu-01:9000 failed on connection exception: java.net.ConnectException: 拒绝连接; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
hadoop@Ubuntu-01:/usr/local/hadoop/hadoop-2.7.3/etc/hadoop$ start-dfs.sh 
Starting namenodes on [Ubuntu-01]
Ubuntu-01: starting namenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-namenode-Ubuntu-01.out
Ubuntu-03: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-03.out
Ubuntu-02: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-02.out
Starting secondary namenodes [Ubuntu-01]
Ubuntu-01: starting secondarynamenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-secondarynamenode-Ubuntu-01.out
hadoop@Ubuntu-01:~$ hdfs dfsadmin -report
Configured Capacity: 82167201792 (76.52 GB)
Present Capacity: 67444781056 (62.81 GB)
DFS Remaining: 67444297728 (62.81 GB)
DFS Used: 483328 (472 KB)
DFS Used%: 0.00%
Under replicated blocks: 0
Blocks with corrupt replicas: 0
Missing blocks: 0
Missing blocks (with replication factor 1): 0

-------------------------------------------------
Live datanodes (2):

Name: 192.168.1.180:50010 (Ubuntu-03)
Hostname: Ubuntu-03
Decommission Status : Normal
Configured Capacity: 41083600896 (38.26 GB)
DFS Used: 241664 (236 KB)
Non DFS Used: 7351656448 (6.85 GB)
DFS Remaining: 33731702784 (31.42 GB)
DFS Used%: 0.00%
DFS Remaining%: 82.11%
Configured Cache Capacity: 0 (0 B)
Cache Used: 0 (0 B)
Cache Remaining: 0 (0 B)
Cache Used%: 100.00%
Cache Remaining%: 0.00%
Xceivers: 1
Last contact: Sun Feb 12 23:18:24 CST 2017


Name: 192.168.1.170:50010 (Ubuntu-02)
Hostname: Ubuntu-02
Decommission Status : Normal
Configured Capacity: 41083600896 (38.26 GB)
DFS Used: 241664 (236 KB)
Non DFS Used: 7370764288 (6.86 GB)
DFS Remaining: 33712594944 (31.40 GB)
DFS Used%: 0.00%
DFS Remaining%: 82.06%
Configured Cache Capacity: 0 (0 B)
Cache Used: 0 (0 B)
Cache Remaining: 0 (0 B)
Cache Used%: 100.00%
Cache Remaining%: 0.00%
Xceivers: 1
Last contact: Sun Feb 12 23:18:24 CST 2017
```

#### 查看HDFS前台

http://192.168.1.160:50070/
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image062.png)

#### 查看RM

http://192.168.1.160:8088/


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image063.png)

#### 查看Jobhistory

```shell
hadoop@Ubuntu-01:~$ mr-jobhistory-daemon.sh start historyserver
starting historyserver, logging to /usr/local/hadoop/hadoop-2.7.3/logs/mapred-hadoop-historyserver-Ubuntu-01.out
hadoop@Ubuntu-01:~$ mr-jobhistory-daemon.sh stop historyserver
stopping historyserver
```

http://192.168.1.160:19888/jobhistory

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image064.png)

#### 运行wordcount程序

创建 input目录

```shell
hadoop@Ubuntu-01:~$ mkdir input
```

在input创建f1、f2并写内容

```shell
hadoop@Ubuntu-01:~$ cat input/f1 
Hello world  bye jj
hadoop@Ubuntu-01:~$ cat input/f2
Hello Hadoop  bye Hadoop
```

在hdfs创建/tmp/input目录

```shell
hadoop@Ubuntu-01:~$ hadoop fs -mkdir /tmp
hadoop@Ubuntu-01:~$ hadoop fs -mkdir /tmp/input
```

将f1、f2文件copy到hdfs /tmp/input目录

```shell
hadoop@Ubuntu-01:~$ hadoop fs -put input/ /tmp
```

执行wordcount程序

```shell
hadoop@Ubuntu-01:~$ hadoop jar /usr/local/hadoop/hadoop-2.7.3/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /tmp/input /output
17/02/12 21:47:48 INFO client.RMProxy: Connecting to ResourceManager at Ubuntu-01/192.168.1.160:8032
17/02/12 21:47:49 INFO input.FileInputFormat: Total input paths to process : 2
17/02/12 21:47:49 INFO mapreduce.JobSubmitter: number of splits:2
17/02/12 21:47:50 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1486907123913_0001
17/02/12 21:47:50 INFO impl.YarnClientImpl: Submitted application application_1486907123913_0001
17/02/12 21:47:50 INFO mapreduce.Job: The url to track the job: http://Ubuntu-01:8088/proxy/application_1486907123913_0001/
17/02/12 21:47:50 INFO mapreduce.Job: Running job: job_1486907123913_0001
17/02/12 21:48:02 INFO mapreduce.Job: Job job_1486907123913_0001 running in uber mode : false
17/02/12 21:48:02 INFO mapreduce.Job:  map 0% reduce 0%
17/02/12 21:48:12 INFO mapreduce.Job:  map 100% reduce 0%
17/02/12 21:48:20 INFO mapreduce.Job:  map 100% reduce 100%
17/02/12 21:48:21 INFO mapreduce.Job: Job job_1486907123913_0001 completed successfully
17/02/12 21:48:21 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=84
		FILE: Number of bytes written=357236
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=243
		HDFS: Number of bytes written=36
		HDFS: Number of read operations=9
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters 
		Launched map tasks=2
		Launched reduce tasks=1
		Data-local map tasks=2
		Total time spent by all maps in occupied slots (ms)=16865
		Total time spent by all reduces in occupied slots (ms)=4585
		Total time spent by all map tasks (ms)=16865
		Total time spent by all reduce tasks (ms)=4585
		Total vcore-milliseconds taken by all map tasks=16865
		Total vcore-milliseconds taken by all reduce tasks=4585
		Total megabyte-milliseconds taken by all map tasks=17269760
		Total megabyte-milliseconds taken by all reduce tasks=4695040
	Map-Reduce Framework
		Map input records=2
		Map output records=8
		Map output bytes=75
		Map output materialized bytes=90
		Input split bytes=198
		Combine input records=8
		Combine output records=7
		Reduce input groups=5
		Reduce shuffle bytes=90
		Reduce input records=7
		Reduce output records=5
		Spilled Records=14
		Shuffled Maps =2
		Failed Shuffles=0
		Merged Map outputs=2
		GC time elapsed (ms)=426
		CPU time spent (ms)=1580
		Physical memory (bytes) snapshot=508022784
		Virtual memory (bytes) snapshot=5689307136
		Total committed heap usage (bytes)=263376896
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=45
	File Output Format Counters 
		Bytes Written=36
```

查看执行结果

```shell
hadoop@Ubuntu-01:~$ hadoop fs -cat /output/part-r-00000
Hadoop	2
Hello	2
bye	2
jj	1
world	1
```

## 安装Scala

scala-2.11.8.tgz
http://www.scala-lang.org/download/

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir scala
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop scala
hadoop@Ubuntu-01:/usr/local$ cd scala/
hadoop@Ubuntu-01:/usr/local/scala$ tar -zxvf scala-2.11.8.tgz


hadoop@Ubuntu-01:/usr/local/scala$ sudo vim /etc/profile
```

末尾加入：

```shell
export SCALA_HOME=/usr/local/scala/scala-2.11.8
export PATH=$PATH:$SCALA_HOME/bin
```

```shell
hadoop@Ubuntu-01:/usr/local/scala$ source /etc/profile
```
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image065.png)

另外两台机器进行类似操作安装scala

## 安装Spark

http://spark.apache.org/

spark-2.1.0-bin-hadoop2.7.tgz

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir spark
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop spark
hadoop@Ubuntu-01:/usr/local$ cd spark/
hadoop@Ubuntu-01:/usr/local/spark$ tar -zxvf spark-2.1.0-bin-hadoop2.7.tgz

hadoop@Ubuntu-01:/usr/local/spark$ sudo vim /etc/profile
```

```shell
export SPARK_HOME=/usr/local/spark/spark-2.1.0-bin-hadoop2.7
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
```

```shell
hadoop@Ubuntu-01:/usr/local/spark$ source /etc/profile
```

另外两台进行类似操作

### 配置

```shell
cd /usr/local/spark/conf
mv spark-env.sh.template spark-env.sh
vim spark-env.sh
```

```shell
HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
SPARK_MASTER_HOST=192.168.1.160
SPARK_MASTER_WEBUI_PORT=28686
SPARK_LOCAL_DIRS=/usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/local
SPARK_WORKER_DIR=/usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/worker
SPARK_DRIVER_MEMORY=4G
SPARK_WORKER_CORES=16
SPARK_WORKER_MEMORY=64g
SPARK_LOG_DIR=/usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/logs
# 下面的配置主要用于jobhistory，非必须
SPARK_HISTORY_OPTS="-Dspark.history.ui.port=18080 -Dspark.history.retainedApplications=3 -Dspark.history.fs.logDirectory=hdfs://Ubuntu-01:9000/spark/log"
```

```shell
mv spark-defaults.conf.template spark-defaults.conf
vim spark-defaults.conf
```

```shell
#下面的配置主要用于jobhistory，非必须

spark.eventLog.enabled true
spark.eventLog.dir hdfs://Ubuntu-01:9000/spark/log
spark.eventLog.compress true
```


复制spark目录

```shell
hadoop@Ubuntu-01:/usr/local/spark$ scp -r spark-2.1.0-bin-hadoop2.7/ hadoop@Ubuntu-02:/usr/local/spark
hadoop@Ubuntu-01:/usr/local/spark$ scp -r spark-2.1.0-bin-hadoop2.7/ hadoop@Ubuntu-03:/usr/local/spark
```

 
### 验证

```shell
hadoop@Ubuntu-01:~$ start-dfs.sh 
Starting namenodes on [Ubuntu-01]
Ubuntu-01: starting namenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-namenode-Ubuntu-01.out
Ubuntu-02: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-02.out
Ubuntu-03: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-03.out
Starting secondary namenodes [Ubuntu-01]
Ubuntu-01: starting secondarynamenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-secondarynamenode-Ubuntu-01.out
hadoop@Ubuntu-01:~$ jps
5057 SecondaryNameNode
4846 NameNode
5166 Jps
hadoop@Ubuntu-01:~$ start-yarn.sh 
starting yarn daemons
starting resourcemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-resourcemanager-Ubuntu-01.out
Ubuntu-02: starting nodemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-nodemanager-Ubuntu-02.out
Ubuntu-03: starting nodemanager, logging to /usr/local/hadoop/hadoop-2.7.3/logs/yarn-hadoop-nodemanager-Ubuntu-03.out
hadoop@Ubuntu-01:~$ jps
5568 Jps
5057 SecondaryNameNode
5223 ResourceManager
4846 NameNode
hadoop@Ubuntu-01:~$ start-master.sh 
starting org.apache.spark.deploy.master.Master, logging to /usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/logs/spark-hadoop-org.apache.spark.deploy.master.Master-1-Ubuntu-01.out
hadoop@Ubuntu-01:~$ jps
5649 Jps
5057 SecondaryNameNode
5223 ResourceManager
5597 Master
4846 NameNode
hadoop@Ubuntu-01:~$ start-slave.sh 192.168.1.160:7077
starting org.apache.spark.deploy.worker.Worker, logging to /usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/logs/spark-hadoop-org.apache.spark.deploy.worker.Worker-1-Ubuntu-01.out
hadoop@Ubuntu-01:~$ jps
5057 SecondaryNameNode
5223 ResourceManager
5672 Worker
5720 Jps
5597 Master
4846 NameNode 

hadoop@Ubuntu-01:~$ start-history-server.sh 
starting org.apache.spark.deploy.history.HistoryServer, logging to /usr/local/spark/spark-2.1.0-bin-hadoop2.7/tmp/logs/spark-hadoop-org.apache.spark.deploy.history.HistoryServer-1-Ubuntu-01.out

hadoop@Ubuntu-01:~$ run-example org.apache.spark.examples.SparkPi 2>%1 | grep "Pi is roughly"
Pi is roughly 3.140195700978505
hadoop@Ubuntu-01:~$ spark-submit $SPARK_HOME/examples/src/main/python/pi.py 2>%1 | grep "Pi is roughly"
Pi is roughly 3.146920
 
 
hadoop@Ubuntu-01:~$ spark-shell 
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
17/02/15 22:30:19 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
17/02/15 22:30:29 WARN metastore.ObjectStore: Version information not found in metastore. hive.metastore.schema.verification is not enabled so recording the schema version 1.2.0
17/02/15 22:30:29 WARN metastore.ObjectStore: Failed to get database default, returning NoSuchObjectException
17/02/15 22:30:32 WARN metastore.ObjectStore: Failed to get database global_temp, returning NoSuchObjectException
Spark context Web UI available at http://192.168.1.160:4040
Spark context available as 'sc' (master = local[*], app id = local-1487169020439).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.1.0
      /_/
         
Using Scala version 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_121)
Type in expressions to have them evaluated.
Type :help for more information.

scala> val textFile =sc.textFile("file:///usr/local/spark/spark-2.1.0-bin-hadoop2.7/README.md");
textFile: org.apache.spark.rdd.RDD[String] = file:///usr/local/spark/spark-2.1.0-bin-hadoop2.7/README.md MapPartitionsRDD[1] at textFile at <console>:24

scala> textFile.count();
res8: Long = 104

scala> textFile.first();
res9: String = # Apache Spark

scala> val linesWithSpark = textFile.filter(line=> line.contains("Spark"));
linesWithSpark: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[2] at filter at <console>:26

scala> linesWithSpark.count();
res10: Long = 20

scala> textFile.filter(line =>line.contains("Spark")).count();
res11: Long = 20

scala>
```

#### 前台界面

SPARK_MASTER_WEBUI: http://192.168.1.160:28686/
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image066.png)

SPARK_HISTORY：http://192.168.1.160:18080/

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image067.png)

### 关闭顺序

```shell
hadoop@Ubuntu-01:~$ stop-history-server.sh 
stopping org.apache.spark.deploy.history.HistoryServer
hadoop@Ubuntu-01:~$ stop-slaves.sh 
Ubuntu-02: stopping org.apache.spark.deploy.worker.Worker
Ubuntu-03: stopping org.apache.spark.deploy.worker.Worker
Ubuntu-01: stopping org.apache.spark.deploy.worker.Worker
hadoop@Ubuntu-01:~$ stop-master.sh 
stopping org.apache.spark.deploy.master.Master
hadoop@Ubuntu-01:~$ stop-yarn.sh 
stopping yarn daemons
stopping resourcemanager
Ubuntu-03: stopping nodemanager
Ubuntu-02: stopping nodemanager
no proxyserver to stop
hadoop@Ubuntu-01:~$ stop-dfs.sh 
Stopping namenodes on [Ubuntu-01]
Ubuntu-01: stopping namenode
Ubuntu-02: stopping datanode
Ubuntu-03: stopping datanode
Stopping secondary namenodes [Ubuntu-01]
Ubuntu-01: stopping secondarynamenode
```

### Scala-IDE搭建Spark源码分析环境

下载、解压Scala-IDE，下载地址为：
http://scala-ide.org/index.html
scala-SDK-4.5.0-vfinal-2.11-win32.win32.x86_64.zip

下载、安装SBT，下载地址为：
http://www.scala-sbt.org/
sbt-0.13.13.1.msi

在github上下载最新的Spark源码：

```shell
PS D:\temp\Scala> git clone https://github.com/apache/spark.git

PS D:\temp\Scala> cd .\spark\
```

输入sbt命令，首次会下载很多东西，速度比较慢，某些在墙外，所以需要提前搭建VPN。如果出错可以多执行几遍

```shell
PS D:\temp\Scala\spark> sbt
                                           ignoring option MaxPermSize=256m; support was removed in 8.0
[info] Loading project definition from D:\temp\Scala\spark\project
[info] Resolving key references (18753 settings) ...
[info] Set current project to spark-parent (in build file:/D:/temp/Scala/spark/)
```

在sbt提示符下输入eclipse，首次会下载很多东西，速度比较慢。如果出错多执行几遍。

```shell
> eclipse
[info] About to create Eclipse project files for your project(s).
[info] Resolving jline#jline;2.12.1 ...
[info] Successfully created Eclipse project files for project(s):
[info] spark-sql
[info] spark-sql-kafka-0-10
[info] spark-streaming-kafka-0-8-assembly
[info] spark-examples
[info] spark-streaming
[info] spark-mllib
[info] spark-catalyst
[info] spark-streaming-kafka-0-10-assembly
[info] spark-graphx
[info] spark-streaming-flume-sink
[info] spark-tags
[info] spark-assembly
[info] spark-mllib-local
[info] spark-tools
[info] spark-repl
[info] spark-streaming-flume-assembly
[info] spark-streaming-kafka-0-8
[info] old-deps
[info] spark-network-common
[info] spark-hive
[info] spark-streaming-flume
[info] spark-sketch
[info] spark-network-shuffle
[info] spark-core
[info] spark-unsafe
[info] spark-streaming-kafka-0-10
[info] spark-launcher
> exit
```

在Scala-IDE导入spark项目：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image068.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image069.png)

## 安装Zookeeper

https://zookeeper.apache.org/

zookeeper-3.4.9.tar.gz

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir zookeeper
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop zookeeper/
hadoop@Ubuntu-01:/usr/local$ cd zookeeper/
hadoop@Ubuntu-01:/usr/local/zookeeper$ tar -zxvf zookeeper-3.4.9.tar.gz

hadoop@Ubuntu-01:/usr/local/zookeeper$ sudo vim /etc/profile

export ZOOKEEPER_HOME=/usr/local/zookeeper/zookeeper-3.4.9
export PATH=$PATH:$ZOOKEEPER_HOME/bin

hadoop@Ubuntu-01:/usr/local/zookeeper$ source /etc/profile

hadoop@Ubuntu-01:/usr/local/zookeeper/ $ cd zookeeper-3.4.9/conf
hadoop@Ubuntu-01:/usr/local/zookeeper/zookeeper-3.4.9/conf$ cp zoo_sample.cfg zoo.cfg
hadoop@Ubuntu-01:/usr/local/zookeeper/zookeeper-3.4.9/conf$ vim zoo.cfg
```

将dataDir改为dataDir=/usr/local/zookeeper/zookeeper-3.4.9/data（该目录需要新建），在文件末位添加所有的主机，注意server后面的数字需要与myid文件中的数字保持一致。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image070.png)

```shell
hadoop@Ubuntu-01:/usr/local/zookeeper/zookeeper-3.4.9$ mkdir data
hadoop@Ubuntu-01:/usr/local/zookeeper/zookeeper-3.4.9$ cd data/
hadoop@Ubuntu-01:/usr/local/zookeeper/zookeeper-3.4.9/data$ vim myid
```

myid中写入1

对Ubuntu-02与Ubuntu-03机器进行类似操作，在各主机myid文件中写入各自的编号。

```shell
hadoop@Ubuntu-01:/usr/local/zookeeper$ scp -r zookeeper-3.4.9/ hadoop@Ubuntu-02:/usr/local/zookeeper/
hadoop@Ubuntu-01:/usr/local/zookeeper$ scp -r zookeeper-3.4.9/ hadoop@Ubuntu-03:/usr/local/zookeeper/
```

### 验证
在每台zookeeper机器上执行：

```shell
hadoop@Ubuntu-01:~$ zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED

hadoop@Ubuntu-02:~$ zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED

hadoop@Ubuntu-03:~$ zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED

hadoop@Ubuntu-01:~$ zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Mode: follower

hadoop@Ubuntu-02:~$ zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Mode: leader

hadoop@Ubuntu-03:~$ zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Mode: follower


hadoop@Ubuntu-01:~$ zkCli.sh -server Ubuntu-01:2181
Connecting to Ubuntu-01:2181
2017-02-18 22:32:23,226 [myid:] - INFO  [main:Environment@100] - Client environment:zookeeper.version=3.4.9-1757313, built on 08/23/2016 06:50 GMT
2017-02-18 22:32:23,231 [myid:] - INFO  [main:Environment@100] - Client environment:host.name=Ubuntu-01
2017-02-18 22:32:23,231 [myid:] - INFO  [main:Environment@100] - Client environment:java.version=1.8.0_121
2017-02-18 22:32:23,233 [myid:] - INFO  [main:Environment@100] - Client environment:java.vendor=Oracle Corporation
2017-02-18 22:32:23,233 [myid:] - INFO  [main:Environment@100] - Client environment:java.home=/usr/local/java/jdk1.8.0_121/jre
2017-02-18 22:32:23,233 [myid:] - INFO  [main:Environment@100] - Client environment:java.class.path=/usr/local/zookeeper/zookeeper-3.4.9/bin/../build/classes:/usr/local/zookeeper/zookeeper-3.4.9/bin/../build/lib/*.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../lib/slf4j-log4j12-1.6.1.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../lib/slf4j-api-1.6.1.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../lib/netty-3.10.5.Final.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../lib/log4j-1.2.16.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../lib/jline-0.9.94.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../zookeeper-3.4.9.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../src/java/lib/*.jar:/usr/local/zookeeper/zookeeper-3.4.9/bin/../conf:.:/usr/local/java/jdk1.8.0_121/lib:.:/usr/local/java/jdk1.8.0_121/lib:.:/usr/local/java/jdk1.8.0_121/lib:
2017-02-18 22:32:23,234 [myid:] - INFO  [main:Environment@100] - Client environment:java.library.path=/usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib
2017-02-18 22:32:23,234 [myid:] - INFO  [main:Environment@100] - Client environment:java.io.tmpdir=/tmp
2017-02-18 22:32:23,234 [myid:] - INFO  [main:Environment@100] - Client environment:java.compiler=<NA>
2017-02-18 22:32:23,235 [myid:] - INFO  [main:Environment@100] - Client environment:os.name=Linux
2017-02-18 22:32:23,235 [myid:] - INFO  [main:Environment@100] - Client environment:os.arch=amd64
2017-02-18 22:32:23,235 [myid:] - INFO  [main:Environment@100] - Client environment:os.version=4.4.0-62-generic
2017-02-18 22:32:23,235 [myid:] - INFO  [main:Environment@100] - Client environment:user.name=hadoop
2017-02-18 22:32:23,236 [myid:] - INFO  [main:Environment@100] - Client environment:user.home=/home/hadoop
2017-02-18 22:32:23,236 [myid:] - INFO  [main:Environment@100] - Client environment:user.dir=/home/hadoop
2017-02-18 22:32:23,237 [myid:] - INFO  [main:ZooKeeper@438] - Initiating client connection, connectString=Ubuntu-01:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@531d72ca
Welcome to ZooKeeper!
2017-02-18 22:32:23,268 [myid:] - INFO  [main-SendThread(Ubuntu-01:2181):ClientCnxn$SendThread@1032] - Opening socket connection to server Ubuntu-01/192.168.1.160:2181. Will not attempt to authenticate using SASL (unknown error)
JLine support is enabled
2017-02-18 22:32:23,398 [myid:] - INFO  [main-SendThread(Ubuntu-01:2181):ClientCnxn$SendThread@876] - Socket connection established to Ubuntu-01/192.168.1.160:2181, initiating session
2017-02-18 22:32:23,429 [myid:] - INFO  [main-SendThread(Ubuntu-01:2181):ClientCnxn$SendThread@1299] - Session establishment complete on server Ubuntu-01/192.168.1.160:2181, sessionid = 0x15a51a0e47d0000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: Ubuntu-01:2181(CONNECTED) 0] quit
Quitting...
2017-02-18 22:32:34,993 [myid:] - INFO  [main-EventThread:ClientCnxn$EventThread@519] - EventThread shut down for session: 0x15a51a0e47d0000
2017-02-18 22:32:34,994 [myid:] - INFO  [main:ZooKeeper@684] - Session: 0x15a51a0e47d0000 closed


hadoop@Ubuntu-01:~$ echo ruok| nc Ubuntu-01 2181
imokhadoop@Ubuntu-01:~$
```

## 安装HBase
下载地址：http://hbase.apache.org/
安装版本：hbase-1.2.4-bin.tar.gz

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir hbase
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop hbase/
hadoop@Ubuntu-01:/usr/local$ cd hbase/
hadoop@Ubuntu-01:/usr/local/hbase$ tar -zxvf hbase-1.2.4-bin.tar.gz
hadoop@Ubuntu-01:/usr/local/spark$ sudo vim /etc/profile

export HBASE_HOME=/usr/local/hbase/hbase-1.2.4
export PATH=$PATH:$HBASE_HOME/bin
export HBASE_CLASSPATH=$HBASE_HOME/lib

hadoop@Ubuntu-01:/usr/local/spark$ source /etc/profile
hadoop@Ubuntu-01:/usr/local/hbase$ cd hbase-1.2.4/conf
hadoop@Ubuntu-01:/usr/local/hbase/hbase-1.2.4/conf$ vim hbase-env.sh
```

取消JAVA_HOME和HBASE_MANAGES_ZK项的注释，并设置正确值。

```shell
export JAVA_HOME=/usr/local/java/jdk1.8.0_121
export HBASE_MANAGES_ZK=false
```

```shell
hadoop@Ubuntu-01:/usr/local/hbase/hbase-1.2.4/conf$ vim hbase-site.xml
```

```xml
<configuration>
<property>
        <name>hbase.rootdir</name>
        <value>hdfs://Ubuntu-01:9000/hbase</value>
</property>
<property>
        <name>hbase.cluster.distributed</name>
        <value>true</value>
</property>
<property>
        <name>hbase.zookeeper.quorum</name>
        <value>Ubuntu-01,Ubuntu-02,Ubuntu-03</value>
</property>
</configuration>
```

复制到另外两个节点

```shell
hadoop@Ubuntu-01:/usr/local/hbase$ scp -r hbase-1.2.4 hadoop@Ubuntu-02:/usr/local/hbase/
hadoop@Ubuntu-01:/usr/local/hbase$ scp -r hbase-1.2.4 hadoop@Ubuntu-03:/usr/local/hbase/
```
### 验证

#### 启动
除了zkServer.sh start要在所有节点执行外，其余启动命令只需要在主节点执行

```shell
hadoop@Ubuntu-01:~$ start-dfs.sh 
Starting namenodes on [Ubuntu-01]
Ubuntu-01: starting namenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-namenode-Ubuntu-01.out
Ubuntu-02: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-02.out
Ubuntu-03: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-03.out
Starting secondary namenodes [Ubuntu-01]
Ubuntu-01: starting secondarynamenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-secondarynamenode-Ubuntu-01.out
hadoop@Ubuntu-01:~$ jps
10835 Jps
10518 NameNode
4299 SecondaryNameNode
hadoop@Ubuntu-01:~$ zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
hadoop@Ubuntu-01:~$ jps
10518 NameNode
10854 QuorumPeerMain
4299 SecondaryNameNode
10879 Jps
hadoop@Ubuntu-01:~$ start-hbase.sh
starting master, logging to /usr/local/hbase/hbase-1.2.4/logs/hbase-hadoop-master-Ubuntu-01.out
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0
hadoop@Ubuntu-01:~$ jps
10518 NameNode
10854 QuorumPeerMain
11015 HMaster
11191 Jps
4299 SecondaryNameNode
hadoop@Ubuntu-01:~$ hbase shell
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hbase/hbase-1.2.4/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop/hadoop-2.7.3/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
HBase Shell; enter 'help<RETURN>' for list of supported commands.
Type "exit<RETURN>" to leave the HBase Shell
Version 1.2.4, r67592f3d062743907f8c5ae00dbbe1ae4f69e5af, Tue Oct 25 18:10:20 CDT 2016

hbase(main):001:0>
```

#### 查看hbase管理界面
http://ubuntu-01:16010/


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image071.png)




#### 关闭
除了zkServer.sh stop要在所有节点执行外，其余关闭命令只需要在主节点执行

```shell
hadoop@Ubuntu-01:~$ jps
11297 Jps
10518 NameNode
10854 QuorumPeerMain
11015 HMaster
4299 SecondaryNameNode
hadoop@Ubuntu-01:~$ stop-hbase.sh 
stopping hbase................
hadoop@Ubuntu-01:~$ jps
10518 NameNode
10854 QuorumPeerMain
4299 SecondaryNameNode
11516 Jps
hadoop@Ubuntu-01:~$ zkServer.sh stop
ZooKeeper JMX enabled by default
Using config: /usr/local/zookeeper/zookeeper-3.4.9/bin/../conf/zoo.cfg
Stopping zookeeper ... STOPPED
hadoop@Ubuntu-01:~$ jps
11537 Jps
10518 NameNode
4299 SecondaryNameNode
hadoop@Ubuntu-01:~$ stop-dfs.sh 
Stopping namenodes on [Ubuntu-01]
Ubuntu-01: stopping namenode
Ubuntu-02: stopping datanode
Ubuntu-03: stopping datanode
Stopping secondary namenodes [Ubuntu-01]
hadoop@Ubuntu-01:~$ jps
11880 Jps
```

## 安装Hive
http://hive.apache.org/

apache-hive-2.1.1-bin.tar.gz


```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir hive
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop hive/
hadoop@Ubuntu-01:/usr/local$ cd hive/
hadoop@Ubuntu-01:/usr/local/hive$ tar -zxvf apache-hive-2.1.1-bin.tar.gz


hadoop@Ubuntu-01:/usr/local/hive$ sudo vim /etc/profile



export HIVE_HOME=/usr/local/hive/apache-hive-2.1.1-bin
export PATH=$PATH:$HIVE_HOME/bin

hadoop@Ubuntu-01:/usr/local/hive$ source /etc/profile


hadoop@Ubuntu-01:/usr/local/hive$ cd apache-hive-2.1.1-bin/conf/
hadoop@Ubuntu-01:/usr/local/hive/apache-hive-2.1.1-bin/conf$ cp hive-default.xml.template hive-site.xml
hadoop@Ubuntu-01:/usr/local/hive/apache-hive-2.1.1-bin/conf$ vim hive-site.xml
```

```xml
<configuration>
<property>
   <name>javax.jdo.option.ConnectionURL</name>
   <value>jdbc:mysql://192.168.1.100:3306/hive?createDatabaseIfNotExist=true</value>
</property>
<property>
   <name>javax.jdo.option.ConnectionDriverName</name>
   <value>com.mysql.jdbc.Driver</value>
</property>
<property>
  <name>javax.jdo.option.ConnectionUserName</name>
  <value>hive</value>
  <description>username to use against metastore database</description>
</property>
<property>
   <name>javax.jdo.option.ConnectionPassword</name>
   <value>hive</value>
</property>
<property>
   <name>hive.hwi.listen.port</name>
   <value>9999</value>
   <description>This is the port the Hive Web Interface will listen on</description>
</property>
<property>
   <name>datanucleus.autoCreateSchema</name>
   <value>false</value>
</property>
<property>
   <name>datanucleus.fixedDatastore</name>
   <value>true</value>
</property>
<property>
 <name>hive.metastore.local</name>
 <value>true</value>
 <description>controls whether to connect to remove metastore server or open a new metastore server in Hive Client JVM</description>
</property>
<property>
   <name>hive.metastore.schema.verification</name>
   <value>false</value>
    <description>
    Enforce metastore schema version consistency.
    True: Verify that version information stored in metastore matches with one from Hive jars.  Also disable automatic
          schema migration attempt. Users are required to manully migrate schema after Hive upgrade which ensures
          proper metastore schema migration. (Default)
    False: Warn if the version information stored in metastore doesn't match with one from in Hive jars.
    </description>
 </property>
</configuration>
```

下载mysql连接java的驱动 并拷入hive home的lib下（mysql-connector-java-5.1.38.jar）

```shell
hadoop@Ubuntu-01:~$ schematool -initSchema -dbType mysql
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hive/apache-hive-2.1.1-bin/lib/log4j-slf4j-impl-2.4.1.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop/hadoop-2.7.3/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
Metastore connection URL:	 jdbc:mysql://192.168.1.100:3306/hive?createDatabaseIfNotExist=true
Metastore Connection Driver :	 com.mysql.jdbc.Driver
Metastore connection User:	 hive
Starting metastore schema initialization to 2.1.0
Initialization script hive-schema-2.1.0.mysql.sql
Initialization script completed
schemaTool completed
hadoop@Ubuntu-01:~$ start-dfs.sh 
Starting namenodes on [Ubuntu-01]
Ubuntu-01: starting namenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-namenode-Ubuntu-01.out
Ubuntu-02: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-02.out
Ubuntu-03: starting datanode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-datanode-Ubuntu-03.out
Starting secondary namenodes [Ubuntu-01]
Ubuntu-01: starting secondarynamenode, logging to /usr/local/hadoop/hadoop-2.7.3/logs/hadoop-hadoop-secondarynamenode-Ubuntu-01.out
hadoop@Ubuntu-01:~$ hive
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hive/apache-hive-2.1.1-bin/lib/log4j-slf4j-impl-2.4.1.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hadoop/hadoop-2.7.3/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in jar:file:/usr/local/hive/apache-hive-2.1.1-bin/lib/hive-common-2.1.1.jar!/hive-log4j2.properties Async: true
Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
hive>
```

```sql
create database hive;
-- 创建hive用户,并授权
grant all on hive.* to hive@'%' identified by 'hive';
flush privileges;
```


## 安装PIG
http://pig.apache.org/
pig-0.16.0.tar.gz

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir pig
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop pig/
hadoop@Ubuntu-01:/usr/local$ cd pig/
hadoop@Ubuntu-01:/usr/local/pig$ tar -zxvf pig-0.16.0.tar.gz

hadoop@Ubuntu-01:/usr/local/pig$ sudo vim /etc/profile

export PIG_HOME=/usr/local/pig/pig-0.16.0
export PATH=$PATH:$PIG_HOME/bin
export PIG_CLASSPATH=$HADDOP_HOME/conf


hadoop@Ubuntu-01:/usr/local/pig$ source /etc/profile
```

### 测试

```shell
hadoop@Ubuntu-01:~$ pig -x local
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hadoop/hadoop-2.7.3/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hbase/hbase-1.2.4/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
17/02/24 22:26:57 INFO pig.ExecTypeProvider: Trying ExecType : LOCAL
17/02/24 22:26:57 INFO pig.ExecTypeProvider: Picked LOCAL as the ExecType
2017-02-24 22:26:57,715 [main] INFO  org.apache.pig.Main - Apache Pig version 0.16.0 (r1746530) compiled Jun 01 2016, 23:10:49
2017-02-24 22:26:57,715 [main] INFO  org.apache.pig.Main - Logging error messages to: /home/hadoop/pig_1487946417711.log
2017-02-24 22:26:57,754 [main] INFO  org.apache.pig.impl.util.Utils - Default bootup file /home/hadoop/.pigbootup not found
2017-02-24 22:26:58,045 [main] INFO  org.apache.hadoop.conf.Configuration.deprecation - mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
2017-02-24 22:26:58,046 [main] INFO  org.apache.hadoop.conf.Configuration.deprecation - fs.default.name is deprecated. Instead, use fs.defaultFS
2017-02-24 22:26:58,048 [main] INFO  org.apache.pig.backend.hadoop.executionengine.HExecutionEngine - Connecting to hadoop file system at: file:///
2017-02-24 22:26:58,344 [main] INFO  org.apache.hadoop.conf.Configuration.deprecation - io.bytes.per.checksum is deprecated. Instead, use dfs.bytes-per-checksum
2017-02-24 22:26:58,374 [main] INFO  org.apache.pig.PigServer - Pig Script ID for the session: PIG-default-7efc5f81-68bd-4e67-aa0d-30882be88c11
2017-02-24 22:26:58,375 [main] WARN  org.apache.pig.PigServer - ATS is disabled since yarn.timeline-service.enabled set to false
grunt> quit
2017-02-24 22:30:50,757 [main] INFO  org.apache.pig.Main - Pig script completed in 3 minutes, 53 seconds and 947 milliseconds (233947 ms)
hadoop@Ubuntu-01:~$ pig
17/02/24 22:32:52 INFO pig.ExecTypeProvider: Trying ExecType : LOCAL
17/02/24 22:32:52 INFO pig.ExecTypeProvider: Trying ExecType : MAPREDUCE
17/02/24 22:32:52 INFO pig.ExecTypeProvider: Picked MAPREDUCE as the ExecType
2017-02-24 22:32:52,844 [main] INFO  org.apache.pig.Main - Apache Pig version 0.16.0 (r1746530) compiled Jun 01 2016, 23:10:49
2017-02-24 22:32:52,845 [main] INFO  org.apache.pig.Main - Logging error messages to: /home/hadoop/pig_1487946772836.log
2017-02-24 22:32:52,890 [main] INFO  org.apache.pig.impl.util.Utils - Default bootup file /home/hadoop/.pigbootup not found
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/usr/local/hadoop/hadoop-2.7.3/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/usr/local/hbase/hbase-1.2.4/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
2017-02-24 22:32:53,865 [main] INFO  org.apache.hadoop.conf.Configuration.deprecation - mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
2017-02-24 22:32:53,866 [main] INFO  org.apache.hadoop.conf.Configuration.deprecation - fs.default.name is deprecated. Instead, use fs.defaultFS
2017-02-24 22:32:53,866 [main] INFO  org.apache.pig.backend.hadoop.executionengine.HExecutionEngine - Connecting to hadoop file system at: hdfs://Ubuntu-01:9000
2017-02-24 22:32:54,752 [main] INFO  org.apache.pig.PigServer - Pig Script ID for the session: PIG-default-aeeb7102-d88a-4154-9876-d76ff0da3a8c
2017-02-24 22:32:54,752 [main] WARN  org.apache.pig.PigServer - ATS is disabled since yarn.timeline-service.enabled set to false
grunt> ls /
hdfs://Ubuntu-01:9000/hbase	<dir>
hdfs://Ubuntu-01:9000/output	<dir>
hdfs://Ubuntu-01:9000/tmp	<dir>
```

## 安装Mahout

http://mahout.apache.org/
apache-mahout-distribution-0.12.2.tar.gz

```shell
hadoop@Ubuntu-01:~$ cd /usr/local
hadoop@Ubuntu-01:/usr/local$ sudo mkdir mahout
hadoop@Ubuntu-01:/usr/local$ sudo chown hadoop:hadoop mahout/
hadoop@Ubuntu-01:/usr/local$ cd mahout/
hadoop@Ubuntu-01:/usr/local/mahout$ tar -zxvf apache-mahout-distribution-0.12.2.tar.gz


hadoop@Ubuntu-01:/usr/local/mahout$ sudo vim /etc/profile

export MAHOUT_HOME=/usr/local/mahout/apache-mahout-distribution-0.12.2
export PATH=$PATH:$MAHOUT_HOME/bin

hadoop@Ubuntu-01:/usr/local/mahout$ source /etc/profile

hadoop@Ubuntu-01:~$ cd
hadoop@Ubuntu-01:~$ start-dfs.sh
hadoop@Ubuntu-01:~$ start-yarn.sh
hadoop@Ubuntu-01:~$ mahout –help
Running on hadoop, using /usr/local/hadoop/hadoop-2.7.3/bin/hadoop and HADOOP_CONF_DIR=
MAHOUT-JOB: /usr/local/mahout/apache-mahout-distribution-0.12.2/mahout-examples-0.12.2-job.jar
Unknown program '--help' chosen.
Valid program names are:
  arff.vector: : Generate Vectors from an ARFF file or directory
  baumwelch: : Baum-Welch algorithm for unsupervised HMM training
  canopy: : Canopy clustering
  cat: : Print a file or resource as the logistic regression models would see it
  cleansvd: : Cleanup and verification of SVD output
  clusterdump: : Dump cluster output to text
  clusterpp: : Groups Clustering Output In Clusters
  cmdump: : Dump confusion matrix in HTML or text formats
  cvb: : LDA via Collapsed Variation Bayes (0th deriv. approx)
  cvb0_local: : LDA via Collapsed Variation Bayes, in memory locally.
  describe: : Describe the fields and target variable in a data set
  evaluateFactorization: : compute RMSE and MAE of a rating matrix factorization against probes
  fkmeans: : Fuzzy K-means clustering
  hmmpredict: : Generate random sequence of observations by given HMM
  itemsimilarity: : Compute the item-item-similarities for item-based collaborative filtering
  kmeans: : K-means clustering
  lucene.vector: : Generate Vectors from a Lucene index
  matrixdump: : Dump matrix in CSV format
  matrixmult: : Take the product of two matrices
  parallelALS: : ALS-WR factorization of a rating matrix
  qualcluster: : Runs clustering experiments and summarizes results in a CSV
  recommendfactorized: : Compute recommendations using the factorization of a rating matrix
  recommenditembased: : Compute recommendations using item-based collaborative filtering
  regexconverter: : Convert text files on a per line basis based on regular expressions
  resplit: : Splits a set of SequenceFiles into a number of equal splits
  rowid: : Map SequenceFile<Text,VectorWritable> to {SequenceFile<IntWritable,VectorWritable>, SequenceFile<IntWritable,Text>}
  rowsimilarity: : Compute the pairwise similarities of the rows of a matrix
  runAdaptiveLogistic: : Score new production data using a probably trained and validated AdaptivelogisticRegression model
  runlogistic: : Run a logistic regression model against CSV data
  seq2encoded: : Encoded Sparse Vector generation from Text sequence files
  seq2sparse: : Sparse Vector generation from Text sequence files
  seqdirectory: : Generate sequence files (of Text) from a directory
  seqdumper: : Generic Sequence File dumper
  seqmailarchives: : Creates SequenceFile from a directory containing gzipped mail archives
  seqwiki: : Wikipedia xml dump to sequence file
  spectralkmeans: : Spectral k-means clustering
  split: : Split Input data into test and train sets
  splitDataset: : split a rating dataset into training and probe parts
  ssvd: : Stochastic SVD
  streamingkmeans: : Streaming k-means clustering
  svd: : Lanczos Singular Value Decomposition
  testnb: : Test the Vector-based Bayes classifier
  trainAdaptiveLogistic: : Train an AdaptivelogisticRegression model
  trainlogistic: : Train a logistic regression using stochastic gradient descent
  trainnb: : Train the Vector-based Bayes classifier
  transpose: : Take the transpose of a matrix
  validateAdaptiveLogistic: : Validate an AdaptivelogisticRegression model against hold-out data set
  vecdist: : Compute the distances between a set of Vectors (or Cluster or Canopy, they must fit in memory) and a list of Vectors
  vectordump: : Dump vectors from a sequence file to text
  viterbi: : Viterbi decoding of hidden states from given output states sequence
hadoop@Ubuntu-01:~$ hadoop fs -mkdir /user
hadoop@Ubuntu-01:~$ hadoop fs -mkdir /user/Hadoop
hadoop@Ubuntu-01:~$ hadoop fs -mkdir /user/hadoop/testdata
hadoop@Ubuntu-01:~$ hadoop fs -put big-data-demo/synthetic_control.data.txt /user/hadoop/testdata
hadoop@Ubuntu-01:~$ hadoop jar /usr/local/mahout/apache-mahout-distribution-0.12.2/mahout-examples-0.12.2-job.jar org.apache.mahout.clustering.syntheticcontrol.kmeans.Job
hadoop@Ubuntu-01:~$ hadoop fs -ls -R output
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:21 output/_policy
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:21 output/clusteredPoints
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:21 output/clusteredPoints/_SUCCESS
-rw-r--r--   2 hadoop supergroup     363282 2017-03-01 22:21 output/clusteredPoints/part-m-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:16 output/clusters-0
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:16 output/clusters-0/_policy
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00000
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00001
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00002
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00003
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00004
-rw-r--r--   2 hadoop supergroup       1891 2017-03-01 22:16 output/clusters-0/part-00005
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:16 output/clusters-1
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:16 output/clusters-1/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:16 output/clusters-1/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:16 output/clusters-1/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:21 output/clusters-10-final
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:21 output/clusters-10-final/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:21 output/clusters-10-final/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:21 output/clusters-10-final/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:17 output/clusters-2
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:17 output/clusters-2/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:17 output/clusters-2/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:17 output/clusters-2/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:17 output/clusters-3
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:17 output/clusters-3/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:17 output/clusters-3/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:17 output/clusters-3/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:18 output/clusters-4
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:18 output/clusters-4/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:18 output/clusters-4/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:18 output/clusters-4/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:18 output/clusters-5
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:18 output/clusters-5/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:18 output/clusters-5/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:18 output/clusters-5/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:19 output/clusters-6
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:19 output/clusters-6/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:19 output/clusters-6/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:19 output/clusters-6/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:19 output/clusters-7
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:19 output/clusters-7/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:19 output/clusters-7/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:19 output/clusters-7/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:20 output/clusters-8
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:20 output/clusters-8/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:20 output/clusters-8/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:20 output/clusters-8/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:20 output/clusters-9
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:20 output/clusters-9/_SUCCESS
-rw-r--r--   2 hadoop supergroup        194 2017-03-01 22:20 output/clusters-9/_policy
-rw-r--r--   2 hadoop supergroup       7581 2017-03-01 22:20 output/clusters-9/part-r-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:16 output/data
-rw-r--r--   2 hadoop supergroup          0 2017-03-01 22:16 output/data/_SUCCESS
-rw-r--r--   2 hadoop supergroup     335470 2017-03-01 22:16 output/data/part-m-00000
drwxr-xr-x   - hadoop supergroup          0 2017-03-01 22:16 output/random-seeds
-rw-r--r--   2 hadoop supergroup       7723 2017-03-01 22:16 output/random-seeds/part-randomSeed
```

## 使用Ambari安装Hadoop集群

ubuntu-16.04.1-04 ubuntu-16.04.1-05 ubuntu-16.04.1-06三台虚拟机已经拆除，如果需要再次尝试Ambari需要重新创建虚拟机。

### 基础环境搭建
配置主机名，安装JDK，配置SSH互登陆等参考前文所述方法，配置SSH互登陆过程中要使用root用户，在配置过程中，如果scp命令不允许使用root用户远程访问，参考下面的方法解决：

```shell
root@Ubuntu-04:~# vi /etc/ssh/sshd_config

# Authentication:
LoginGraceTime 120
PermitRootLogin yes
#PermitRootLogin prohibit-password
StrictModes yes
```

重启 ssh  服务

```shell
root@Ubuntu-04:~# service ssh restart
```

另外由于Ambari最新版本的安装需要Maven，所以在某个节点上使用下面方式安装Maven：

```shell
root@Ubuntu-04:~# mkdir /usr/local/maven
root@Ubuntu-04:~# cd /usr/local/maven/
root@Ubuntu-04:/usr/local/maven# ls
apache-maven-3.5.0-bin.tar.gz
root@Ubuntu-04:/usr/local/maven# tar -zxvf apache-maven-3.5.0-bin.tar.gz


root@Ubuntu-04:/usr/local/maven# sudo vim /etc/profile

export M2_HOME=/usr/local/maven/apache-maven-3.5.0
export PATH=$PATH:$M2_HOME/bin


root@Ubuntu-04:/usr/local/maven# source /etc/profile
```

### 安装Ambari
主要参考官方文档：https://cwiki.apache.org/confluence/display/AMBARI/Installation+Guide+for+Ambari+2.5.1

在其中一个节点（安装maven的节点）下载ambari的源码包，并打包成deb包，拷贝到所有其它节点进行安装。

```shell
root@Ubuntu-04:~# mkdir /usr/local/ambary
root@Ubuntu-04:~# cd /usr/local/ambari/
root@Ubuntu-04:/usr/local/ambari# wget http://www.apache.org/dist/ambari/ambari-2.5.1/apache-ambari-2.5.1-src.tar.gz
root@Ubuntu-04:/usr/local/ambari# tar xfvz apache-ambari-2.5.1-src.tar.gz
root@Ubuntu-04:/usr/local/ambari# cd apache-ambari-2.5.1-src
root@Ubuntu-04:/usr/local/ambari/apache-ambari-2.5.1-src# mvn versions:set -DnewVersion=2.5.1.0.0
root@Ubuntu-04:/usr/local/ambari/apache-ambari-2.5.1-src# pushd ambari-metrics
/usr/local/ambari/apache-ambari-2.5.1-src/ambari-metrics /usr/local/ambari/apache-ambari-2.5.1-src
root@Ubuntu-04:/usr/local/ambari/apache-ambari-2.5.1-src/ambari-metrics# mvn versions:set -DnewVersion=2.5.1.0.0
root@Ubuntu-04:/usr/local/ambari/apache-ambari-2.5.1-src/ambari-metrics# popd
/usr/local/ambari/apache-ambari-2.5.1-src
root@Ubuntu-04:/usr/local/ambari/apache-ambari-2.5.1-src# mvn -B clean install package jdeb:jdeb -DnewVersion=2.5.1.0.0 -DskipTests -Dpython.ver="python >= 2.6"
# 如果遇到某些包因为墙的原因无法下载，则直接在网上下载对应的包放到日志指定的目录。
# 如果报错：ENOGIT git is not installed or not in the PATH，则安装git：apt-get install git。
# 如果遇到类似于下面的错误，则在对应项目的pom.xml中增加
```

```xml
<plugin>
         <groupId>org.vafer</groupId>
         <artifactId>jdeb</artifactId>
         <version>1.0.1</version>
         <executions>
           <execution>
             <!--Stub execution on direct plugin call - workaround for ambari deb build process-->
             <id>stub-execution</id>
             <phase>none</phase>
             <goals>
               <goal>jdeb</goal>
             </goals>
           </execution>
         </executions>
         <configuration>
           <skip>true</skip>
           <attach>false</attach>
           <submodules>false</submodules>
           <controlDir>${project.basedir}/../src/main/package/deb/control</controlDir>
         </configuration>
       </plugin>\
```

```log
[ERROR] Failed to execute goal org.vafer:jdeb:1.0.1:jdeb (default-cli) on project ambari-logsearch: Failed to create debian package /home/kylin/apache-ambari-2.4.2-src/ambari-logsearch/target/ambari-logsearch_2.4.2.0.0_all.deb: “/home/kylin/apache-ambari-2.4.2-src/ambari-logsearch/src/main/package/deb/control” is not a valid ‘control’ directory) -> [Help 1]

# 如果遇到类似下面的错误，将对应项目的pom.xml中的storm版本改为1.1.0

<properties>
    <storm.version>1.1.0 </storm.version>
  </properties>
# 如果遇到如下报错，执行sudo apt-get install python-dev

     [exec] creating build/temp.linux-x86_64-2.7/psutil
     [exec] x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -fno-strict-aliasing -Wdate-time -D_FORTIFY_SOURCE=2 -g -fstack-protector-strong -Wformat -Werror=format-security -fPIC -I/usr/include/python2.7 -c psutil/_psutil_linux.c -o build/temp.linux-x86_64-2.7/psutil/_psutil_linux.o
     [exec] psutil/_psutil_linux.c:12:20: fatal error: Python.h: 没有那个文件或目录
     [exec] compilation terminated.
     [exec] error: command 'x86_64-linux-gnu-gcc' failed with exit status 1

# 如果报如下错误，参考https://cwiki.apache.org//confluence/display/MAVEN/OutOfMemoryError

[ERROR] Java heap space -> [Help 1]
[ERROR] 
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR] 
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/OutOfMemoryError
```

## 大数据平台-kerberos安装部署文档

### 环境准备

#### 操作系统
本次安装部署要求在操作系统为CentOS release 6.5 (Final)的版本下进行部署，所以在安装部署kerberos之前请先确保操作系统为以上版本，并且集群中各机器已做时钟同步。
本次安装部署以csdm-hadoop-04作为主kdc服务器，以csdm-hadoop-05作为从kdc服务器，以csdm-hadoop-03作为客户端。一般不建议在服务器上再安装其他应用程序，比如hadoop。但为了节省资源本次安装在这三台机器均已安装hadoop相关软件。
#### 创建操作用户
创建操作系统hdfs、yarn、mapred用户，并使其归属于hadoop用户组:
adduser hdfs -g Hadoop
adduser yarn -g Hadoop
adduser mapred -g Hadoop
#### 配置hosts文件
为各台机器修改/etc/hosts文件，将真实ip与主机名对应配置，服务端与客户端均需配置，形如：（不能存在127.0.0.1的配置，否则hadoop进行kerberos验证时将会出错）
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image072.png)
 
#### 关闭防火墙
执行以下命令关闭防火墙：
service iptables stop
出现以下界面表示关闭成功
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image073.png)
 
#### 注册服务与端口的对应
在/etc/service文件最后增加以下信息，以便后续使用：
	krb5_prop 754/tcp   # Kerberos slave propagation

### 安装配置Kerberos
#### 安装rpm包
	以root用户登录并创建目录存放安装包：
mkdir /var/kerberos
	上传安装包文件到创建的目录，包括krb5-libs-1.10.3-10.el6_4.6.x86_64.rpm、krb5-server-1.10.3-10.el6_4.6.x86_64.rpm（客户端可不安装）、krb5-workstation-1.10.3-10.el6_4.6.x86_64.rpm
	执行安装命令：
rpm -ivh krb5-libs-1.10.3-10.el6_4.6.x86_64.rpm
rpm -ivh krb5-server-1.10.3-10.el6_4.6.x86_64.rpm【客户端可不安装】
rpm -ivh krb5-workstation-1.10.3-10.el6_4.6.x86_64.rpm
	查看上述包是否已安装成功：
rpm –qa krb5*
                 若出现以下情况则代表安装成功。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image074.jpg)

#### 配置主KDC服务器
##### 设置全局环境变量
需要以root身份登录系统在/etc/profile末尾增加配置文件的全局环境变量：
export KRB5_CONFIG=/etc/krb5.conf
export KRB5_KDC_PROFILE=/var/kerberos/krb5kdc/kdc.conf

保存后并 执行source /etc/profile 使之生效。

##### 配置krb5.conf
执行vi编辑/etc/krb5.conf，内容如下：

[libdefaults]
 default_realm = ERICSSON.COM
 dns_lookup_realm = false
 dns_lookup_kdc = false
 ticket_lifetime = 24h
 renew_lifetime = 7d
 forwardable = true

[realms]
  ERICSSON.COM = {
  kdc = csdm-hadoop-04
kdc = csdm-hadoop-05 
  admin_server =csdm-hadoop-04
 }

[domain_realm]
 .ericsson.com = ERICSSON.COM
 ericsson.com = ERICSSON.COM


##### 配置kdc.conf 
执行vi编辑/var/kerberos/krb5kdc/kdc.conf，内容如下：
	[kdcdefaults]
Kdc_ports=750,88  

[realms]
      ERICSSON.COM ={  
			kadmind_port = 749
            max_life=10h 0m 0s  
            max_renewable_life=7d 0h 0m 0s  
            database_name= /var/kerberos/krb5kdc/principal  
            admin_keytab=/var/kerberos /krb5kdc/kadm5.keytab  
            acl_file=/var/kerberos /krb5kdc/kadm5.acl  
            key_stash_file=/var/kerberos /krb5kdc/.k5.ERICSSON.COM 
      }  
[logging]
 default = FILE:/var/log/krb5libs.log
 kdc = FILE:/var/log/krb5kdc.log
 admin_server = FILE:/var/log/kadmind.log

集群机器如果开启selinux，请在机器上执行restorecon -R -v /etc/krb5.conf
##### 生成数据库
在主KDC服务器上执行以下命令创建数据库，在执行的过程中会提示输入密码和确认密码，两次输入相同的密码即可：
kdb5_util create -r ericsson.com –s

等待片刻后在提示输入密码界面输入密码后会出现以下界面：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image075.png)

##### 创建管理用户
运行管理入口命令：
kadmin.local 
在提示符下执行以下命令
addprinc kadmin/admin@ERICSSON.COM
addprinc kadmin/changepw@ERICSSON.COM
会提示输入密码，输入两次一样的密码后会提示成功创建。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image076.png)
将主体添加至密钥文件中
 ktadd -k /var/kerberos/krb5kdc/kadm5.keytab kadmin/admin 
ktadd -k /var/kerberos/krb5kdc/kadm5.keytab kadmin/changepw 

##### 启动krb5kdc 和kadmind服务
执行以下命令启动krb5kdc和kadmind服务：
krb5kdc start
kadmind 
出现以下界面表示启动成功
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image077.png)

#### 配置从KDC服务器
##### 为从kdc服务器创建创建授权票证
每一个kdc服务器都需要一个host票证，用于在迁移数据库数据市在各kdc服务器之间进行交互验证。注意，创建host票据需要在主kdc服务器上执行而不是在从kdc服务器。在csdm-hadoop-04上执行以下命令创建票证：

kadmin
addprinc –randkey host/csdm-hadoop-04@ERICSSON.COM
addprinc –randkey host/csdm-hadoop-05@ERICSSON.COM
ktadd host/csdm-hadoop-05@ERICSSON.COM

##### 设置从kdc服务器的配置文件
将主kdc服务器中的配置文件（kdc.conf、 krb5.conf、 .k5.ERICSSON.COM、 kadm5.acl）复制到从kdc服务器上相应的目录中；在从kdc服务器的/var/Kerberos/krb5kdc的目录下创建kpropd.acl文件并增加以下信息：

host/csdm-hadoop-04@ERICSSON.COM
host/csdm-hadoop-05@ERICSSON.COM

#### 复制数据库数据到KDC从服务器
	在主服务器上创建数据库的dump文件
kdb5_util dump /var/kerberos/krb5kdc/slave_datatrans
	在从服务器上执行数据迁移
kprop -f  /var/Kerberos/krb5kdc/slave_datatrans csdm-hadoop-05

定时将主KDC服务器上的数据库数据，更新到从KDC服务器上
由于KDC不提供数据库数据的同步服务功能，因此需要使用脚本或者手工将主KDC服务器上的数据同步到从KDC服务器上，可以参考以下脚本，并配置到定时器中
#!/bin/sh   
	kdclist = "kerberos2.example.com kerberos3.example.com"   
	kdb5_util dump /var/kerberos/krb5kdc/slave_datatrans   
	for kdc in $kdclist do      
		   kprop -f /var/kerberos/krb5kdc/slave_datatrans $kdc 

#### 启动从服务器的krb5kdc程序
在从服务器上启动命令执行启动：
	krb5kdc
#### 配置自启动
在/etc/inittab中增加以下信息可使进程随系统自启动：
/etc/init.d/krb5kdc start
Kadmind

#### 客户端配置
下面以csdm-hadoop-03这台机器作为客户端说明相关配置
1、在csdm-hadoop-03上安装客户端软件
rpm -ivh krb5-libs-1.10.3-10.el6_4.6.x86_64.rpm
rpm -ivh krb5-workstation-1.10.3-10.el6_4.6.x86_64.rpm
2、在主KDC服务器csdm-hadoop-04上，把/etc/krb5.conf复制到csdm-hadoop-03本地对应目录
3、在客户端csdm-hadoop-03上启动命令执行启动：
	krb5kdc
此时即可在客户端csdm-hadoop-03上连接KDC服务器

4、生成可访问csdm-hadoop-03机器应用程序的验证
在主KDC服务器csdm-hadoop-04,生成csdm-hadoop-03的principals和keytab，
为客户端csdm-hadoop-03添加principals（可以为host或者所要进行验证的机器用户）
addprinc –randkey host/csdm-hadoop-03@ERICSSON.COM
    为客户端csdm-hadoop-03生成keytab
Ktadd –k /var/kerberos/krb5kdc/keytab/host.keytab host/csdm-hadoop-03@ERICSSON.COM
把csdm-hadoop-04上生成的keytab复制到csdm-hadoop-03机器上


### 测试服务器
#### 服务器端测试客户端连接
 运行kinit admin/admin，显示提示输入密码则代表配置成功： 
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image078.png)
#### 远程客户机连接测试
    在客户机运行kinit admin/admin 连接服务端，显示提示输入密码则代表配置成功：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image079.png)

### Hadoop集成kerberos配置
#### 4.1  kerberos配置
Hadoop官方网站建议的操作系统用户及权限如下，下面我们按照这三个用户的权限进行配置，要求使用下面三种用户分别具有各自启动相应进程的权限。
User:Group	Daemons
hdfs:hadoop	NameNode, Secondary NameNode, JournalNode, DataNode
yarn:hadoop	ResourceManager, NodeManager
mapred:hadoop	MapReduce，JobHistory Server

##### 4.1.1 为所有机器的用户生成principal
从主KDC服务器csdm-hadoop-04上，把/etc/krb5.conf复制到csdm-hadoop-03本地对应目录，
在主KDC服务器上为hadoop集群中每台机器的用户创建principal，下面以csdm-hadoop-03这台机器为例，运行管理入口命令：
kadmin.local
在提示符下执行以下命令：
addprinc -randkey hdfs/csdm-hadoop-03@ERICSSON.COM
addprinc -randkey host/csdm-hadoop-03@ERICSSON.COM

addprinc -randkey yarn/csdm-hadoop-03@ERICSSON.COM
addprinc -randkey host/csdm-hadoop-03@ERICSSON.COM

addprinc -randkey mapred/csdm-hadoop-03@ERICSSON.COM
addprinc -randkey host/csdm-hadoop-03@ERICSSON.COM

注：
	集群中的每台机器所用到的用户都需执行上面的命令生成principal
	每个用户必须执行addprinc -randkey host/XX@XX的命令，这个命令生成的是基于 Kerberos 的应用程序（例如 klist 和 kprop）和服务（例如 ftp 和 telnet）使用的主体。此主体称为 host 主体或服务主体。

##### 4.1.2 生成keytab文件
完成5.1.1后在主KDC服务器上为所有principal生成keytab文件，运行管理入口命令：
kadmin.local 
在提示符下执行以下命令：
xst -norandkey -k /var/kerberos/krb5kdc/keytab/hdfs.keytab 
hdfs/csdm-hadoop-03@ERICSSON.COM  host/csdm-hadoop-03@ERICSSON.COM
xst -norandkey -k /var/kerberos/krb5kdc/keytab/mapred.keytab 
mapred/csdm-hadoop-03@ ERICSSON.COM  host/csdm-hadoop-03@ERICSSON.COM
xst -norandkey -k /var/kerberos/krb5kdc/keytab/yarn.keytab 
yarn/csdm-hadoop-03@ERICSSON.COM  host/csdm-hadoop-03@ERICSSON.COM

生成授权文件后，使用以下命令检查生成的keytab是否可用：
kinit -k -t 
/var/kerberos/krb5kdc/keytab/hdfs.keytab hdfs/csdm-hadoop-03@ERICSSON.COM
kinit -k -t 
/var/kerberos/krb5kdc/keytab/mapred.keytab  mapred/csdm-hadoop-03@ERICSSON.COM
kinit -k -t 
/var/kerberos/krb5kdc/keytab/yarn.keytab  yarn/csdm-hadoop-03@ERICSSON.COM

检查没问题后，把生成的keytab文件分发到整个集群中的所有机器。

#### 修改HADOOP配置文件
##### 4.2.1 Jsvc安装配置
Datanode的安全机制需要以root用户身份用jsvc来启动，因此首先需要检查是否安装是jsvc如果没有，按以下步骤进行安装：
1、	下载commons-daemon-1.0.15-src.tar.gz 包并上传至自定义的目录（本操作目录为/home/hadoop）
2、	解压缩后
以root用户登录进入目录/home/Hadoop 执行:
tar –xvf commons-daemon-1.0.15-bin.tar.gz
解压完成后进入
/home/Hadoop /commons-daemon-1.0.15-src/src/native/unix
执行命令：configure
执行命令：make
编译完成后，会在/home/hadoop/commons-daemon-1.0.15-src/src/native/unix目录下生成jsvc可执行文件，如下图

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image080.png)

在该目录下执行file jsvc如果出现下图所示，则jsvc安装成功
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image081.png)

   这里，我们把该执行文件复制到$HADOOP_HOME/bin以便后续的配置
执行命令：cp  /home/hadoop/commons-daemon-1.0.15-src/src/native/unix/jsvc 
/home/hadoop/hadoop/bin
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image082.png)

##### 4.2.2 hadoop-env.sh配置
找到以下两项配置，并修改
export HADOOP_SECURE_DN_USER=hdfs（配置为要执行datanode的用户，这里为hdfs）
export JSVC_HOME=/home/hadoop/hadoop/bin(配置为jsvc所在的目录)
##### 4.2.3 core-site.xml
在集群中所有节点的core-site.xml文件中添加下面的配置

```xml
  <!-- kerberos config --> 
<property>
        <name>hadoop.security.authorization</name>
        <value>true</value>
    </property>
    <property>
        <name>hadoop.security.authentication</name>
        <value>kerberos</value>
    </property>
    <property>
        <name>hadoop.rpc.protection</name>
        <value>authentication</value>    
 </property><!—默认使用authentication，可使用integrity ，privacy -->
    <property>
        <name> hadoop.security.auth_to_local</name>
        <value> DEFAULT</value>
    </property><!—此选项对应krb5.conf中【realms】的auth_to_local，用于将操作系统用户与principal 的映射关系-->
```

##### 4.2.4 hdfs-site.xml
在集群中所有节点的hdfs-site.xml文件中添加下面的配置，下面配置以节点csdm-hadoop-04为例： 
<!-- General HDFS security config -->
   <property>
     <name>dfs.block.access.token.enable</name>
     <value>true</value>
   </property>
   <!-- NameNode security config -->
<property>
        <name>dfs.encrypt.data.transfer</name>
        <value>true</value>
   </property>
   <property>
     <name>dfs.https.address</name>
     <value>csdm-hadoop-04:50470</value>
   </property>
   <property>
     <name>dfs.https.port</name>
     <value>50470</value>
   </property>
   <property>
     <name>dfs.namenode.keytab.file</name>
     <value>/var/kerberos/krb5kdc/keytab/hdfs.keytab</value> <!-- path to the HDFS keytab -->

   </property>
   <property>
     <name>dfs.namenode.kerberos.principal</name>
     <value>hdfs/_HOST@ERICSSON.COM</value>
   </property>
   <property>
     <name>dfs.namenode.kerberos.https.principal</name>
     <value>host/_HOST@ERICSSON.COM</value>
   </property>
   
   <!-- Secondary NameNode security config -->
   <property>
     <name>dfs.secondary.https.address</name>
     <value>csdm-hadoop-04:50495</value>
   </property>
   <property>
     <name>dfs.secondary.https.port</name>
     <value>50495</value>
   </property>
   <property>
     <name>dfs.secondary.namenode.keytab.file</name>
     <value>/var/kerberos/krb5kdc/keytab/hdfs.keytab</value> <!-- path to the HDFS keytab -->
   </property>
   <property>
     <name>dfs.secondary.namenode.kerberos.principal</name>
     <value>hdfs/_HOST@ERICSSON.COM</value>
   </property>
   <property>
     <name>dfs.secondary.namenode.kerberos.https.principal</name>
     <value>host/_HOST@ERICSSON.COM</value>
   </property>
   
   <!-- DataNode security config -->
   <property>
     <name>dfs.datanode.data.dir.perm</name>
     <value>700</value>
   </property>
   <property>
     <name>dfs.datanode.address</name>
     <value>0.0.0.0:1004</value>
   </property>
   <property>
     <name>dfs.datanode.http.address</name>
     <value>0.0.0.0:1006</value>
   </property>
   <property>
     <name>dfs.datanode.keytab.file</name>
     <value>/var/kerberos/krb5kdc/keytab/hdfs.keytab</value> <!-- path to the HDFS keytab -->
   </property>
   <property>
     <name>dfs.datanode.kerberos.principal</name>
     <value>hdfs/_HOST@ERICSSON.COM</value>
   </property>
   <property>
     <name>dfs.datanode.kerberos.https.principal</name>
     <value>host/_HOST@ERICSSON.COM</value>
   </property>
   
<!--web config-->
<property>  
        <name>dfs.web.authentication.kerberos.principal</name>  
        <value>hdfs/_HOST@ERICSSON.COM</value>  
</property>  
<property>  
      <name>dfs.web.authentication.kerberos.keytab</name>  
      <value>/var/kerberos/krb5kdc/keytab/hdfs.keytab</value>  
      <description>  
          The Kerberos keytab file with the credentials for the  
          HTTP Kerberos principal used by Hadoop-Auth in the HTTP endpoint.  
      </description>  
</property>       

配置中有几点要注意的
	. dfs.datanode.address表示data transceiver RPC server所绑定的hostname或IP地址，如果开启security，端口号必须小于1024(privileged port)，否则的话启动datanode时候会报“Cannot start secure cluster without privileged resources”错误
	. principal中的instance部分可以使用'_HOST'标记，系统会自动替换它为全称域名
	. 如果开启了security, hadoop会对hdfs block data做permission check，方式用户的代码不是调用hdfs api而是直接本地读block data，这样就绕过了kerberos和文件权限验证，管理员可以通过设置dfs.datanode.data.dir.perm来修改datanode文件权限，这里我们设置为700


配置完成后，修改hdfs.keytab所有者为hdfs
chown -R hdfs:hadoop /var/kerberos/krb5kdc/keytab/hdfs.keytab
chmod 700  /var/kerberos/krb5kdc/keytab/hdfs.keytab

同时保证以下表格中各个目录的对于hdfs用户的权限

Filesystem	Path	User:Group	Permissions
local	dfs.namenode.name.dir	hdfs:hadoop	drwx------
local	dfs.datanode.data.dir	hdfs:hadoop	drwx------
local	$HADOOP_LOG_DIR	hdfs:hadoop	drwxrwxr-x
Hdfs	/	hdfs:hadoop	drwxr-xr-x
Hdfs	/tmp	hdfs:hadoop	drwxrwxrwxt
Hdfs	/user	hdfs:hadoop	drwxr-xr-x

###### 1、测试namenode进程启动是否正常
切换到hdfs用户，首先执行klist命令，查看当前是否获取了ticket，经测试，如果已经获取了ticket那么启动namenode进程的时候会报以下错误 
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image083.png)
使用kdestroy销毁获取的ticket
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image084.png)

切换到hdfs用户，启动namenode进程（已经执行过HDFS格式化的操作）
执行命令：hadoop namenode
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image085.png)
如果配置正常，应该会看到以下的日志信息输出
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image086.png)

验证namenode是否启动正常
	可打开网页
http://XX:50070/dfshealth.html#tab-overview验证
	hadoop fs -ls /
注：如果在你的凭据缓存中没有有效的kerberos ticket，执行hadoop fs –ls /将会失败。
可以使用klist来查看是否有有有效的ticket。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image087.png)
如果为空，使用kinit来获取ticket.命令如下
kinit -k -t /var/kerberos/krb5kdc/keytab/hdfs.keytab hdfs/csdm-hadoop-03@ERICSSON.COM

###### 2、测试datanode启动是否正常
切换到root用户，
执行命令：hadoop-daemon.sh start datanode
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image088.png)
如果启动正常，能在日志文件看到以下日志内容
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image089.png)
在日志目录，启动datanode进程会有以下几个日志文件，其中jsvc.err记录了jsvc的错误信息
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image090.png)

启动datanode进程，只能使用root用户，如果使用其他用户启动，只会报以下错误
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image091.png)
##### 4.2.5 mapred-site.xml
在mapred-site.xml中添加
<!-- JobTracker security configs -->
  <property>
    <name>mapreduce.jobtracker.kerberos.principal</name>
    <value>mapred/_HOST@ERICSSON.COM</value>
  </property>
  <property>
    <name>mapreduce.jobtracker.kerberos.https.principal</name>
    <value>host/_HOST@ERICSSON.COM</value>
  </property>
  <property>
    <name>mapreduce.jobtracker.keytab.file</name>
    <value>/var/kerberos/krb5kdc/keytab/mapred.keytab</value> <!-- path to the MapReduce keytab -->
  </property>
  
  <!-- TaskTracker security configs -->
  <property>
    <name>mapreduce.tasktracker.kerberos.principal</name>
    <value>mapred/_HOST@ERICSSON.COM</value>
  </property>
  <property>
    <name>mapreduce.tasktracker.kerberos.https.principal</name>
    <value>host/_HOST@ERICSSON.COM</value>
  </property>
  <property>
    <name>mapreduce.tasktracker.keytab.file</name>
    <value>/var/kerberos/krb5kdc/keytab/mapred.keytab</value> <!-- path to the MapReduce keytab -->
  </property>
  
  <!-- jobhistory server security -->

<property>
     <name  mapreduce.jobhistory.address</name>
     <value>10020 </value>      <!—如果不设置，则默认使用10020端口-->
  </property>

  <property>
     <name>mapreduce.jobhistory.keytab</name>
     <value>/var/kerberos/krb5kdc/keytab/mapred.keytab</value>
  </property>
  <property>
      <name>mapreduce.jobhistory.principal</name>
      <value>mapred/_HOST@ERICSSON.COM</value>
  </property>

将mapred.keytab文件赋权给mapred用户 ，执行以下命令：
chown -R mapred:hadoop /var/kerberos/krb5kdc/keytab/mapred.keytab
chmod  700  /var/kerberos/krb5kdc/keytab/mapred.keytab
确保以下表格中各个路径的执行权限
Filesystem	Path	User:Group	Permissions
hdfs	mapreduce.jobhistory.intermediate-done-dir	mapred:hadoop	drwxrwxrwxt
hdfs	mapreduce.jobhistory.done-dir	mapred:hadoop	drwxr-x---

测试historyserver 进程
执行命令：mr-jobhistory-daemon.sh start historyserver
配置正常，则会看到以下日志内容
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image092.png)

##### 4.2.6 yarn-site.xml
在yarn-site.xml追加以下内容：
<!-- yarn security -->
	    <property>
               <name>yarn.resourcemanager.keytab</name>
                <value>/var/kerberos/krb5kdc/keytab/yarn.keytab</value>
        </property>
        <property>
                <name>yarn.resourcemanager.principal</name>
                <value>yarn/_HOST@ERICSSON.COM</value>
        </property>
           <!—以上为ResourceManager设置-->
        <property>
                <name>yarn.nodemanager.keytab</name>
                <value>/var/kerberos/krb5kdc/keytab/yarn.keytab</value>
        </property>
        <property>
                <name>yarn.nodemanager.principal</name>
                <value>yarn/_HOST@ERICSSON.COM</value>
        </property>
        <property>
                <name>yarn.nodemanager.container-executor.class</name>
         <value>org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor</value>
        </property>
        <property>
                <name>yarn.nodemanager.linux-container-executor.group</name>
                <value>hadoop</value>
        </property>
       
 <property>
                <name>yarn.nodemanager.linux-container-executor.path</name>
                <value>/home/hadoop/hadoop/bin/container-executor</value> <!—你存放container-executor的绝对路径，下文有交代-->
        </property>
        <!—以上为NodeManager配置-->

YARN提供了两种Container启动实现，DefaultContainerExecutor以及LinuxContainerExecutor，在上面的yarn-site.xml里配置了yarn.nodemanager.container-executor.class的启动方式为LinuxContainerExecutor，那么就需要编译安装LinuxContainerExecutor，按如下操作执行：在hadoop的home目录（这里是/home/Hadoop/hadoop）的 /etc/hadoop/目录下创建 container-executor.cfg 文件，内容如下：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image093.png)

 设置该文件权限：
$ chown root:hadoop container-executor.cfg
$ chmod 400 container-executor.cfg
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image094.png)
注意：
•	container-executor.cfg 文件读写权限需设置为 400，所有者为 root:hadoop。
并且该文件所在的父目录所有者必须为root用户，并对该文件所在的各个父目录赋以下权限，例如：chmod 750 /home/hadoop/
•	yarn.nodemanager.linux-container-executor.group 要同时配置在 yarn-site.xml 和 container-executor.cfg，且其值需要为运行 NodeManager 的用户所在的组，这里为 hadoop。
•	banned.users 不能为空，默认值为 hfds,yarn,mapred,bin
•	min.user.id 默认值为 1000，在centos系统中，需要设置为小于500的值 
•	确保 yarn.nodemanager.local-dirs 和 yarn.nodemanager.log-dirs 对应的目录权限为 755 。
设置 $HADOOP_HOME/bin/container-executor 读写权限为 6050 如下：
$ chown root:hadoop $HADOOP_HOME/bin/container-executor
$ chmod 6050 $HADOOP_HOME/bin/container-executor

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image095.png)
测试是否配置正确：
$ /home/hadoop/hadoop/bin/container-executor –checksetup
出现以下信息，则表示配置正确，如果出错，请检查各个目录的权限及container-executor.cfg文件是否配置正确
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image096.png)

修改yarn.keytab权限
chown -R yarn:hadoop /var/kerberos/krb5kdc/keytab/ yarn.keytab
chmod 700  /var/kerberos/krb5kdc/keytab/yarn.keytab

确保以下表格各目录的权限
Filesystem	Path	User:Group	Permissions
hdfs	yarn.nodemanager.remote-app-log-dir	yarn:hadoop	drwxrwxrwxt
local	$YARN_LOG_DIR	yarn:hadoop	drwxrwxr-x
local	yarn.nodemanager.local-dirs	yarn:hadoop	drwxr-xr-x
local	yarn.nodemanager.log-dirs	yarn:hadoop	drwxr-xr-x
local	container-executor	root:hadoop	--Sr-s---
local	conf/container-executor.cfg	root:hadoop	r--------


	测试 nodemanager 进程
执行命令：yarn nodemanager
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image097.png)
如果配置正常，会输出以下日志
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image098.png)


	测试resourcemanager进程
执行命令：yarn resourcemanager
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image099.png)
如果配置正常，会输出以下日志
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image100.png)

### 说明
注：本部署文档部署环境默认机器未配置DNS，如果配置有DNS的机器上创建实体则格式为：用户名/hostname.DNS@领域名。例如：hdfs/csdm-hadoop-04.ericsson.com@ERICSSON.COM



火狐配置使用SPNNEGO
1、	在地址栏输入about:config打开配置界面
2、	network.negotiate-auth.delegation-uris
network.negotiate-auth.trusted-uris
找到以上两个选项，把你要访问的页面地址加进去

LINUX下配置
1、	在/etc/hosts下加入要访问的地址对应关系（包括客户端和服务器）
2、	在KDC服务器上生成浏览器所在客户端的principal：格式如下：HTTP/hd2@ERICSSON.COM，并把该principal生成到keytab中，在KEYTAB中应该可以看到如下的信息
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image101.png)
