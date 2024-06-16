转自（原文图片已丢失，本文修复图片，重新排版，并更正部分原文错误）：http://www.superwu.cn/2013/12/26/913

欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

Hadoop2的学习资料很少，只有官网的少数文档。如果想更深入的研究hadoop2，除了仅看官网的文档外，还要学习如何看源码，通过不断的调试跟踪源码，学习hadoop的运行机制。

# 1.安装CentOS

我使用的是CentOS 6.5，下载地址是: http://mirror.neu.edu.cn/centos/6.5/isos/x86_64/, 选择`CentOS-6.5-x86_64-bin-DVD1.iso`下载，注意是64位的，大小是4GB，需要下载一段时间的。其实6.x的版本都可以，不一定是6.5。

我使用的是VMWare虚拟机，分配了2GB内存，20GB磁盘空间。内存太小，会比较慢；磁盘太小，编译时可能会出现空间不足的情况。上述不是最低配置，根据自己的机器配置修改吧。还有，一定要保持linux联网状态。

以下是安装各种软件，我把软件下载后全部复制到/usr/local目录下，以下命令执行的路径是在/usr/local目录下。请读者在阅读时，一定要注意路径。

# 2.安装JDK

hadoop是java写的，编译hadoop必须安装jdk。

从Oracle官网下载jdk，下载地址是: http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html, 选择`jdk-7u45-linux-x64.tar.gz`下载。

执行以下命令解压缩jdk
```shell
　　tar -zxvf  jdk-7u45-linux-x64.tar.gz
```
会生成一个文件夹`jdk1.7.0_45`，然后设置在环境变量中。

执行命令 `vi /etc/profile`，增加以下内容到配置文件中，结果显示如下

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114325681-1557853764.png)


保存退出文件后，执行以下命令
```shell
　　source  /etc/profile
　　java -version
```
如果看到下面的显示信息，证明配置正确了。

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114408525-1777603873.png)
 

# 3.安装maven

hadoop源码是使用maven组织管理的，必须下载maven。从maven官网下载，下载地址是: http://maven.apache.org/download.cgi, 选择`apache-maven-3.0.5-bin.tar.gz`下载，不要选择3.1下载。

执行以下命令解压缩jdk
```shell
    tar -zxvf  apache-maven-3.0.5-bin.tar.gz
```
会生成一个文件夹`apache-maven-3.0.5`，然后设置环境变量中。

执行命令`vi /etc/profile`，编辑结果如下图所示

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114451978-786211996.png)


保存退出文件后，执行以下命令
```shell
　　source  /etc/profile
　　mvn -version
```
如果看到下面的显示信息，证明配置正确了。

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114517322-447120661.png)

# 4.安装findbugs（可选步骤）

findbugs是用于生成文档的。如果不需要编译生成文档，可以不执行该步骤。从findbugs官网下载findbugs，下载地址是: http://sourceforge.jp/projects/sfnet_findbugs/releases/, 选择`findbugs-3.0.0-dev-20131204-e3cbbd5.tar.gz`下载。

执行以下命令解压缩jdk
```shell
    tar -zxvf  findbugs-3.0.0-dev-20131204-e3cbbd5.tar.gz
```
会生成一个文件夹`findbugs-3.0.0-dev-20131204-e3cbbd5`，然后设置环境变量中。

执行命令`vi /etc/profile`，编辑结果如下图所示

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114554275-1273084212.png)
 

保存退出文件后，执行以下命令
```shell
　　source  /etc/profile
　　findbugs -version
```
　　如果看到下面的显示信息，证明配置正确了。

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114643775-783496920.png)

# 5.安装protoc

hadoop使用protocol buffer通信，从protoc官网下载protoc，下载地址是: https://code.google.com/p/protobuf/downloads/list, 选择`protobuf-2.5.0.tar.gz`下载。

为了编译安装protoc，需要下载几个工具，顺序执行以下命令
```shell
　　yum install gcc
　　yum intall gcc-c++
　　yum install make
```
如果操作系统是CentOS6.5那么gcc和make已经安装了。其他版本不一定。在命令运行时，需要用户经常输入“y”。

然后执行以下命令解压缩protobuf
```shell
　　tar -zxvf  protobuf-2.5.0.tar.gz
```
会生成一个文件夹`protobuf-2.5.0`，执行以下命令编译protobuf。
```shell
　　cd protobuf-2.5.0
　　./configure --prefix=/usr/local/protoc/
　　make && make install
```
只要不出错就可以了。

执行完毕后，编译后的文件位于`/usr/local/protoc/`目录下，我们设置一下环境变量

执行命令`vi /etc/profile`，编辑结果如下图所示

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114754760-1359143830.png)

保存退出文件后，执行以下命令
```shell
　　source  /etc/profile
　　protoc --version
```
如果看到下面的显示信息，证明配置正确了。

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114820244-1651571624.png)
 

# 6.安装其他依赖

顺序执行以下命令
```shell
　　yum install cmake
　　yum install openssl-devel
　　yum install ncurses-devel
```
　　安装完毕即可。

# 7.编译Hadoop2.2源码

从hadoop官网下载2.2稳定版，下载地址是: http://apache.fayea.com/apache-mirror/hadoop/common/stable2/, 下载`hadoop-2.2.0-src.tar.gz`下载。

执行以下命令解压缩jdk
```shell
　　tar -zxvf hadoop-2.2.0-src.tar.gz
```
会生成一个文件夹 `hadoop-2.2.0-src`。源代码中有个bug，这里需要修改一下，编辑目录`/usr/local/hadoop-2.2.0-src/hadoop-common-project/hadoop-auth`中的文件pom.xml，执行以下命令
```shell
　　gedit pom.xml
```
在第55行下增加以下内容
```xml
     <dependency>
         <groupId>org.mortbay.jetty</groupId>
         <artifactId>jetty-util</artifactId>
         <scope>test</scope>
    </dependency>
```
保存退出即可。

上述bug详见: https://issues.apache.org/jira/browse/HADOOP-10110, 在hadoop3中修复了，离我们太遥远了。

好了，现在进入到目录`/usr/local/hadoop-2.2.0-src`中，执行命令
```shell
　　mvn package -DskipTests -Pdist,native,docs
```
如果没有执行第4步，把上面命令中的docs去掉即可，就不必生成文档了。

该命令会从外网下载依赖的jar，编译hadoop源码，需要花费很长时间，你可以吃饭了。

在等待n久之后，可以看到如下的结果：
```shell
[INFO] Apache Hadoop Main ................................ SUCCESS [6.936s]
[INFO] Apache Hadoop Project POM ......................... SUCCESS [4.928s]
[INFO] Apache Hadoop Annotations ......................... SUCCESS [9.399s]
[INFO] Apache Hadoop Assemblies .......................... SUCCESS [0.871s]
[INFO] Apache Hadoop Project Dist POM .................... SUCCESS [7.981s]
[INFO] Apache Hadoop Maven Plugins ....................... SUCCESS [8.965s]
[INFO] Apache Hadoop Auth ................................ SUCCESS [39.748s]
[INFO] Apache Hadoop Auth Examples ....................... SUCCESS [11.081s]
[INFO] Apache Hadoop Common .............................. SUCCESS [10:41.466s]
[INFO] Apache Hadoop NFS ................................. SUCCESS [26.346s]
[INFO] Apache Hadoop Common Project ...................... SUCCESS [0.061s]
[INFO] Apache Hadoop HDFS ................................ SUCCESS [12:49.368s]
[INFO] Apache Hadoop HttpFS .............................. SUCCESS [41.896s]
[INFO] Apache Hadoop HDFS BookKeeper Journal ............. SUCCESS [41.043s]
[INFO] Apache Hadoop HDFS-NFS ............................ SUCCESS [9.650s]
[INFO] Apache Hadoop HDFS Project ........................ SUCCESS [0.051s]
[INFO] hadoop-yarn ....................................... SUCCESS [1:22.693s]
[INFO] hadoop-yarn-api ................................... SUCCESS [1:20.262s]
[INFO] hadoop-yarn-common ................................ SUCCESS [1:30.530s]
[INFO] hadoop-yarn-server ................................ SUCCESS [0.177s]
[INFO] hadoop-yarn-server-common ......................... SUCCESS [15.781s]
[INFO] hadoop-yarn-server-nodemanager .................... SUCCESS [40.800s]
[INFO] hadoop-yarn-server-web-proxy ...................... SUCCESS [6.099s]
[INFO] hadoop-yarn-server-resourcemanager ................ SUCCESS [37.639s]
[INFO] hadoop-yarn-server-tests .......................... SUCCESS [4.516s]
[INFO] hadoop-yarn-client ................................ SUCCESS [25.594s]
[INFO] hadoop-yarn-applications .......................... SUCCESS [0.286s]
[INFO] hadoop-yarn-applications-distributedshell ......... SUCCESS [10.143s]
[INFO] hadoop-mapreduce-client ........................... SUCCESS [0.119s]
[INFO] hadoop-mapreduce-client-core ...................... SUCCESS [55.812s]
[INFO] hadoop-yarn-applications-unmanaged-am-launcher .... SUCCESS [8.749s]
[INFO] hadoop-yarn-site .................................. SUCCESS [0.524s]
[INFO] hadoop-yarn-project ............................... SUCCESS [16.641s]
[INFO] hadoop-mapreduce-client-common .................... SUCCESS [40.796s]
[INFO] hadoop-mapreduce-client-shuffle ................... SUCCESS [7.628s]
[INFO] hadoop-mapreduce-client-app ....................... SUCCESS [24.066s]
[INFO] hadoop-mapreduce-client-hs ........................ SUCCESS [13.243s]
[INFO] hadoop-mapreduce-client-jobclient ................. SUCCESS [16.670s]
[INFO] hadoop-mapreduce-client-hs-plugins ................ SUCCESS [3.787s]
[INFO] Apache Hadoop MapReduce Examples .................. SUCCESS [17.012s]
[INFO] hadoop-mapreduce .................................. SUCCESS [6.459s]
[INFO] Apache Hadoop MapReduce Streaming ................. SUCCESS [12.149s]
[INFO] Apache Hadoop Distributed Copy .................... SUCCESS [15.968s]
[INFO] Apache Hadoop Archives ............................ SUCCESS [5.851s]
[INFO] Apache Hadoop Rumen ............................... SUCCESS [18.364s]
[INFO] Apache Hadoop Gridmix ............................. SUCCESS [14.943s]
[INFO] Apache Hadoop Data Join ........................... SUCCESS [9.648s]
[INFO] Apache Hadoop Extras .............................. SUCCESS [5.763s]
[INFO] Apache Hadoop Pipes ............................... SUCCESS [16.289s]
[INFO] Apache Hadoop Tools Dist .......................... SUCCESS [3.261s]
[INFO] Apache Hadoop Tools ............................... SUCCESS [0.043s]
[INFO] Apache Hadoop Distribution ........................ SUCCESS [56.188s]
[INFO] Apache Hadoop Client .............................. SUCCESS [10.910s]
[INFO] Apache Hadoop Mini-Cluster ........................ SUCCESS [0.321s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 40:00.444s
[INFO] Finished at: Thu Dec 26 12:42:24 CST 2013
[INFO] Final Memory: 109M/362M
[INFO] ------------------------------------------------------------------------
```
好了，编译完成了。

编译后的代码在`/usr/local/hadoop-2.2.0-src/hadoop-dist/target`下面，如下图。

![](http://images2015.cnblogs.com/blog/611264/201701/611264-20170115114914494-1703630439.png)

如果有的同学操作失败，可以直接下载我已经安装好的镜像文件，链接: http://pan.baidu.com/share/link?shareid=956286972&uk=2032187724, 密码：n0kf