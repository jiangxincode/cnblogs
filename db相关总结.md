# 通用：

* http://db-engines.com/en/ranking
* Tech On The Net: http://www.techonthenet.com/index.php
* SQL Pretty Printer formatter: http://www.dpriver.com/index.php
* ApexSQL: http://www.apexsql.com/
* Withdata: http://www.withdata.com/index.html

    Founded in 2002, Withdata Software is a technology company producing high-quality software for database administrators and developers.
    We do our best to design and develop products that remove complexity, and compress time frames. We are glad to realize that our products take usual chores upon themselves, so that our customers could have more time left for their creative work.


# Oracle MySQL

* MySQL: http://www.mysql.com/
* MySQL参考：http://dev.mysql.com/doc/#manual
* windows下忘记mysql超级管理员root密码的解决办法：http://superman7020.blog.163.com/blog/static/1374465920085210119253/
* 5款常用mysql slow log分析工具的比较：http://blog.chinaunix.net/uid-8504518-id-2030594.html
* Autocomplete in MySQL under Windows: http://stackoverflow.com/questions/269653/autocomplete-in-mysql-under-windows


# SQL Server

* SQL Server: https://msdn.microsoft.com/library/bb545450.aspx
* Transact-SQL 参考: https://msdn.microsoft.com/zh-cn/library/bb510741(v=sql.105).aspx
* TSQLT：http://tsqlt.org/
* sqlcmd 实用工具：http://msdn.microsoft.com/zh-cn/library/ms162773.aspx
* SQL SERVER 2005中的Schema（架构）概念详解：http://blog.sina.com.cn/s/blog_5b2c0dcc0100alj9.html
* Sql Server 2005中的架构(Schema)、用户(User)、角色(Role)和登录(Login)(一)：http://www.cnblogs.com/end/archive/2009/08/07/1541373.html
* Sql Server 2005中的架构(Schema)、用户(User)、角色(Role)和登录(Login)(二)：http://www.cnblogs.com/end/archive/2009/08/07/1541374.html
* Sql Server 2005中的架构(Schema)、用户(User)、角色(Role)和登录(Login)(三)：http://www.cnblogs.com/end/archive/2009/08/07/1541377.html
* 谓词和运算符：http://www.cnblogs.com/cuiyh/archive/2010/12/18/1910090.html
* Tempdb数据库详细介绍：http://www.cnblogs.com/qanholas/archive/2012/01/05/2313006.html


# Oracle Database

* Oracle Database DownLoad: http://www.oracle.com/technetwork/cn/database/enterprise-edition/downloads/index.html
* Documents: http://docs.oracle.com/en/database/
* Database Reference: http://docs.oracle.com/cd/B28359_01/server.111/b28320/index.htm
* Database SQL Language Reference: http://docs.oracle.com/cd/B28359_01/server.111/b28286/index.htm
* Listener Control Utility (LSNRCTL): http://docs.oracle.com/cd/A87861_01/NT817EE/network.817/a76933/controlu.htm#433891
* Database Concepts: http://docs.oracle.com/database/121/CNCPT/toc.htm

* Oracle SQL Developer: http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html
* Instant Client Downloads for Microsoft Windows (32-bit): http://www.oracle.com/technetwork/topics/winsoft-085727.html

* Oracle SQL Handler：http://www.heartblue.cn/
* SI Object Browser：http://www.presoft.com.cn/ob/

* Navicat: http://www.navicat.com.cn/
* Navicat Premium: http://www.navicat.com.cn/products/navicat-premium

    Navicat Premium 是一套数据库管理工具，让你以单一程序同時连接到 MySQL、MariaDB、SQL Server、SQLite、Oracle 和 PostgreSQL 数据库。

* PL/SQL Developer(可以美化sql脚本): http://www.allroundautomations.com/registered/plsqldev.html
* ToadWorld: http://www.toadworld.com/

* Oracle 11g安装图文攻略: http://jingyan.baidu.com/article/9f7e7ec04c14c76f29155465.html
* oracle 11g如何完全卸载: http://jingyan.baidu.com/article/922554468d4e6b851648f4e3.html
* win7_oracle11g_64位连接32位PLSQL_Developer: http://jingyan.baidu.com/article/fb48e8be4c7c206e622e1491.html
* Oracle 11g 如何创建数据库：http://jingyan.baidu.com/article/cbcede07cf42ef02f40b4dc2.html
* 数据库使用详解：[3]SQL Developer如何配置：http://jingyan.baidu.com/article/e4511cf33f289e2b845eafb6.html
* oracle的各版本发行时间及特点: http://blog.csdn.net/dream19881003/article/details/7178357
* oracle客户端软件的说明：http://blog.csdn.net/haiross/article/details/17917637
* 怎么判断oracle客户端、服务器端的位数：http://blog.csdn.net/linghe301/article/details/8471945


## 常用命令

### 杂项

```sql
    desc v$database; --查询v$database数据库的表结构

    show parameter name; -- 查看一些数据库的名字信息

    select global_name from global_name; -- 查看oracle的全局数据库名

    select name,dbid from v$database; -- 查看数据库名
    show parameter db_name;

    select instance_name from v$instance; --查询实例名
    show parameter instance_name;

    select value from v$parameter where name='db_domin'; --查询数据库域名
    show parameter domain;

    --查询数据库服务名，数据库如果有域，则数据库服务名就是全局数据库名；如果没有，则数据库服务名就是数据库名。
    select value from v$parameter where name='service_name';
    show parameter service_name
    show parameter service;
    show parameter names;

```

注：数据库实例名对应着SID，查询SID还可以使用下面的方式：

* linux下查询sid 

在配置oracle环境变量的情况可以使用 echo $ORACLE_SID,如果没有可以使用ps -ef |grep oracle 来查询，结果中的xxxx就是对应的SID。
oracle    2548     1  0 Aug17 ?        00:00:00 ora_pmon_xxxx 

* windows下查询sid

在windows环境下,oracle是以后台服务的方式被管理的,所以看"控制面板->管理工具->服务 里面的名称:"OracleServiceORCL",则ORCL就是sid; 


### 启动数据库

Windows下以管理员身份运行：

    net start oracleserviceorcl (后面的orcl是你安装的数据库实例名)
    net start oracleoradb11g_home1tnslistener (非必须)

linux下以oracle用户登录

    sqlplus / as sysdba
    startup


### sqlplus登陆方式

```sql
    sqlplus / as sysdba --以操作系统权限认证的oracle sys管理员登陆

    sqlplus /nolog
    conn / as sysdba --以操作系统权限认证的oracle sys管理员登陆


    sqlplus sys/password@orcl as sysdba --以sys用户登陆必须使用as sysdba

    sqlplus /nolog --不在cmd或者teminal当中暴露密码的登陆方式
    conn sys/password as sysdba


    sqlplus --不显露密码的方式登陆
    Enter user-name：sys
    Enter password：password as sysdba --以sys用户登陆的话 必须要加上as sysdba子句

    sqlplus scott/tiger@orcl --非管理员用户登陆
    
```

### 设置sqlplus显示格式

```sql
    -- 设置sqlplus模式显示总行数
    show pagesize; --查看当前的pagesize
    set pagesize 300;

    -- 设置sqlplus模式显示行宽度
    show linesize; --查看当前的linesize
    set linesize 300;

    -- 修改安装目录glogin.sql文件才能保证之前的设置永久生效
    set pagesize 300;
    set linesize 300;
```

### oracle创建表之前判断表是否存在，如果存在则删除已有表

在sqlserver中，有if exit()这样的语句，但是在oracle中却没有。如果直接使用drop table那么如果表不存在会报错，导致后续语句无法运行。因此可以通过一个存储过来来进行判断。主要是查询all_tables表的TABLE_NAME和OWNER，如果表存在，则执行execute immediate 'drop table TABLE_NAME'; 

```sql
    --判断表是否存在，如果存在则删除
    declare 
          num   number; 
    begin 
          select count(1) into num from all_tables where TABLE_NAME = 'EMP' and OWNER='SCOTT'; 
          if   num=1   then 
              execute immediate 'drop table EMP'; 
          end   if; 
    end; 
    / 
    --创建表
    CREATE TABLE EMP
           (EMPNO NUMBER(4) NOT NULL,
            ENAME VARCHAR2(10),
            JOB VARCHAR2(9),
            MGR NUMBER(4),
            HIREDATE DATE,
            SAL NUMBER(7, 2),
            COMM NUMBER(7, 2),
            DEPTNO NUMBER(2));
    可以将上述存储过程加载到每一个create table前面。
```

## Oracle 11g 默认用户名和密码

安装ORACLE时，若没有为下列用户重设密码，则其默认密码如下：
 
用户名/密码                登录身份                说明

sys/change_on_install      SYSDBA 或 SYSOPER       不能以 NORMAL 登录，可作为默认的系统管理员

system/manager             SYSDBA 或 NORMAL        不能以 SYSOPER 登录，可作为默认的系统管理员

sysman/oem_temp            sysman                  为 oms 的用户名

scott/tiger                NORMAL                  普通用户

aqadm /aqadm               SYSDBA 或 NORMAL        高级队列管理员

Dbsnmp/dbsnmp              SYSDBA 或 NORMAL        复制管理员
 
 
登录身份：指登录时的Role指定，oracle11g中分SYSDBA和default两种。在安装Oracle 10g的时候，提示创建数据库，在创建的同时提示你输入口令，若此时你输入了密码，在登录数据库的时候用户名sys 对应的密码就应该是你创建数据库时候输入的口令。而非默认的change_on_install.

如果在安装Oracle 11g时忘了设置口令，之后登陆不上去，可以进行如下操作：

```sql
    sqlplus /nolog
    connect /as sysdba
    alter user sys identified by change_on_install
```


## SID和service_name的区别

sid是数据库实例的名字，每个实例各不相同。

service_name参数是由oracle8i引进的。在8i以前，使用SID来表示标识数据库的一个实例，但是在Oracle的并行环境中，一个数据库对应多个实例，这样就需要多个网络服务名，设置繁琐。为了方便并行环境中的设置，引进了service_name参数，该参数对应一个数据库，而不是一个实例，而且该参数有许多其它的好处。该参数的缺省值为Db_name.Db_domain，即等于Global_name。一个数据库可以对应多个service_name，以便实现更灵活的配置。该参数与SID没有直接关系，即不必service name 必须与SID一样 

Java JDBC Thin Driver 连接 Oracle有三种方法，如下：

格式一: Oracle JDBC Thin using a ServiceName: 

jdbc:oracle:thin:@//<host>:<port>/<service_name> 

Example: jdbc:oracle:thin:@//192.168.2.1:1521/XE 

注意这里的格式，@后面有//, 这是与使用SID的主要区别。 这种格式是Oracle 推荐的格式，因为对于集群来说，每个节点的SID 是不一样的，但是SERVICE_NAME 确可以包含所有节点。 

格式二: Oracle JDBC Thin using an SID:

jdbc:oracle:thin:@<host>:<port>:<SID> 

Example: jdbc:oracle:thin:@192.168.2.1:1521:X01A 

Note: Support for SID is being phased out. Oracle recommends that users switch over to usingservice names. 

格式三：Oracle JDBC Thin using a TNSName: 

jdbc:oracle:thin:@<TNSName> 

Example: jdbc:oracle:thin:@GL 

Note:Support for TNSNames was added in the driver release 10.2.0.1 


## Oracle的thin与oci连接方式比较

应用与oracle的连接分为thin和oci两种模式：

                Oracle oci                Oracle thin

实现方式        用Java调用本机Oracle客户端达到访问数据库目的       用Java完成访问数据库

Oracle客户端    需要安装配置             不用安装

性能            理论上略好               理论上略差

移植性          略差                     略好

推荐使用THIN DRIVER，移植性好，相对规范些，问题也少。具体连接上的写法的差异：

```
    jdbc:oracle:thin:@youroraclehost:1521:yoursid
    jdbc:oracle:thin:@(description=(address=(host=youroraclehost)(protocol=tcp)(port=1521))(connect_data=(SERVICE_NAME=yourservicename)))
    jdbc:oracle:oci:@youroracle-tns-name
    jdbc:oracle:oci:@(description=(address=(host=youroraclehost)(protocol=tcp)(port=1521))(connect_data=(SERVICE_NAME=yourservicename)))
```

## 与 oracle 有关的几个端口：1158、1521、5500、5560 

* 1521端口：响应sqlplus
* 1158端口：http://RemoteIP:1158/em，即通过网页方式访问em
* 5560端口：http://RemoteIP:5560/isqlplus，即通过网页方式访问sqlplus

## Oracle 11g服务详细介绍及哪些服务是必须开启的？

成功安装Oracle 11g后，共有7个服务，这七个服务的含义分别为：

* Oracle ORCL VSS Writer Service：Oracle卷映射拷贝写入服务，VSS（Volume Shadow Copy Service）能够让存储基础设备（比如磁盘，阵列等）创建高保真的时间点映像，即映射拷贝（shadow copy）。它可以在多卷或者单个卷上创建映射拷贝，同时不会影响到系统的性能。（非必须启动）
* OracleDBConsoleorcl：Oracle数据库控制台服务，orcl是Oracle的实例标识，默认的实例为orcl。在运行Enterprise Manager（企业管理器OEM）的时候，需要启动这个服务。（非必须启动）
* OracleJobSchedulerORCL：Oracle作业调度（定时器）服务，ORCL是Oracle实例标识。（非必须启动）
* OracleMTSRecoveryService：服务端控制。该服务允许数据库充当一个微软事务服务器MTS、COM/COM+对象和分布式环境下的事务的资源管理器。（非必须启动）
* OracleOraDb11g_home1ClrAgent：Oracle数据库.NET扩展服务的一部分。 （非必须启动）
* OracleOraDb11g_home1TNSListener：监听器服务，服务只有在数据库需要远程访问的时候才需要。（非必须启动，下面会有详解）。
* OracleServiceORCL：数据库服务(数据库实例)，是Oracle核心服务该服务，是数据库启动的基础， 只有该服务启动，Oracle数据库才能正常启动。(必须启动)

那么在开发的时候到底需要启动哪些服务呢？对新手来说，要是只用Oracle自带的sql*plus的话，只要启动OracleServiceORCL即可，要是使用PL/SQL Developer等第三方工具的话，OracleOraDb11g_home1TNSListener服务也要开启。OracleDBConsoleorcl是进入基于web的EM必须开启的，其余服务很少用。

注：ORCL是数据库实例名，默认的数据库是ORCL，你可以创建其他的，即OracleService+数据库名。


# DB2

* 官网：http://www-01.ibm.com/software/data/db2/
* DB2China：http://www.db2china.net/


# Oracle Berkeley DB

* Oracle Berkeley DB：http://www.oracle.com/technetwork/database/database-technologies/berkeleydb/overview/index.html


# nosql

* NoSQL数据库笔谈: http://old.sebug.net/paper/databases/nosql/Nosql.html


# mongodb

* https://www.mongodb.org/
* https://docs.mongodb.org/manual/
* http://api.mongodb.org/java/
* MonjaDB (MongoDB GUI client tool) : http://www.jumperz.net/index.php?i=2&a=0&b=9
* mongolab: https://mongolab.com/
* Spring Data MongoDB hello world example: http://www.mkyong.com/mongodb/spring-data-mongodb-hello-world-example/
* MongoDB设置访问权限、设置用户: http://www.cnblogs.com/zengen/archive/2011/04/23/2025722.html


## MONGOVUE

* http://www.mongovue.com/


## Morphia

    The Java Object Document Mapper for MongoDB

* http://mongodb.github.io/morphia/
* NoSQL 之 Morphia 操作 MongoDB: http://www.cnblogs.com/hoojo/archive/2012/02/17/2355384.html


# hbase

* http://hbase.apache.org/
* HBase 官方文档(中文)：http://yankaycom-wordpress.stor.sinaapp.com/hbase/book.html?q=/wp-content/hbase/book.html


# Hive

* http://hive.apache.org/
* https://cwiki.apache.org/confluence/display/Hive/Home

# Others

GBase: http://www.gbase.cn/
Vertica: https://www.vertica.com/
Teradata Aster: http://developer.teradata.com/aster
actian: http://www.actian.com/

