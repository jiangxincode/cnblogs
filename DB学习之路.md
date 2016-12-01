# DB学习之路 [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

# 通用：

* http://db-engines.com
* Tech On The Net: http://www.techonthenet.com/index.php
* SQL Pretty Printer formatter: http://www.dpriver.com/index.php
* ApexSQL: http://www.apexsql.com/
* RazorSQL: http://www.razorsql.com/
* AquaFold: http://www.aquafold.com/
* Withdata: http://www.withdata.com/index.html
* 红宝书：http://www.redbook.io/
* erwin: http://erwin.com/
* DBeaver: http://dbeaver.jkiss.org/
* Navicat: http://www.navicat.com.cn/
* 0xDBE: https://www.jetbrains.com/dbe/
* 数据库比较工具DBCompareTool 0.3.0 preview 发布：http://www.blogjava.net/allenny/archive/2011/09/30/359028.html
* DB Compare(SQL Server): http://dbcompare.codeplex.com/
* DBComparer(SQL Server): http://dbcomparer.com/
* NoSQL数据库笔谈: http://old.sebug.net/paper/databases/nosql/Nosql.html


# MySQL

* MySQL: http://www.mysql.com/
* MySQL参考：http://dev.mysql.com/doc/#manual
* windows下忘记mysql超级管理员root密码的解决办法：http://superman7020.blog.163.com/blog/static/1374465920085210119253/
* 5款常用mysql slow log分析工具的比较：http://blog.chinaunix.net/uid-8504518-id-2030594.html
* Autocomplete in MySQL under Windows: http://stackoverflow.com/questions/269653/autocomplete-in-mysql-under-windows
* 安装mysql，在./configure时出现错误：error: No curses/termcap library found的解决办法: http://www.cnblogs.com/luojianqun/p/4087423.html
* MYSQL常见错误及其解决方式: http://www.cnblogs.com/jiangxinnju/p/5894225.html
* 如何提高MySql的安全性？: http://blog.163.com/longsu2010@yeah/blog/static/17361234820116223593175/
* 如何写出高质量、高性能的MySQL查询: http://blog.sina.com.cn/s/blog_a8cf6bb20101a33v.html
* 解决mysql字符集乱码问题: http://www.cnblogs.com/dayday-study/archive/2012/05/18/2507276.html
* MySQL默认数据库: http://www.cnblogs.com/jiangxinnju/p/5901845.html
* MySQL的安装、使用及权限管理: http://www.cnblogs.com/sunada2005/articles/2647435.html


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
* MS SQL专用管理员连接DAC: http://www.cnblogs.com/kerrycode/p/3344085.html
* 用于数据库管理员的诊断连接: https://msdn.microsoft.com/zh-cn/library/ms189595.aspx
* 解决sqlserver 2008 sqlcmd无法登陆: http://www.cnblogs.com/skynothing/archive/2010/08/26/1809125.html
* 关于SQLSERVER的全文目录跟全文索引的区别: http://www.cnblogs.com/lyhabc/archive/2012/08/05/2623795.html
* 在SQL Server中如何获得刚插入一条新记录的自动ID号: http://blog.csdn.net/wangji163163/article/details/2424191
* SQL Server中如何取得刚插入的标识值: http://www.blogjava.net/DreamAngel/archive/2012/05/11/377920.html
* Join操作基本：外连接、自然连接、内连接: http://www.cnblogs.com/huangfr/archive/2012/06/20/2555530.html
* SQL 中 where 1=1 和 1=0的 作用: http://blog.csdn.net/wanghai__/article/details/4813909
* left join on 和where条件的放置: http://blog.csdn.net/muxiaoshan/article/details/7617533



## 全文索引和普通索引的区别

两种索引的功能和结构都是不同的，普通索引的结构主要以B+树和哈希索引为主，用于实现对字段中数据的精确查找，比如查找某个字段值等于给定值的记录，A=10这种查询，因此适合数值型字段和短文本字段。全文索引是用于检索字段中是否包含或不包含指定的关键字，有点像搜索引擎的功能，因此全文索引内部采用的是与搜索引擎相同的倒排索引结构，其原理是对字段中的文本进行分词，然后为每一个出现的单词记录一个索引项，这个索引项中保存了所有出现过该单词的记录的信息，也就是说在索引中找到这个单词后，就知道哪些记录的字段中包含这个单词了。因此适合用大文本字段的查找。大字段之所以不适合做普通索引，最主要的原因是普通索引对检索条件只能进行精确匹配，而大字段中的文本内容很多，通常也不会在这种字段上执行精确的文本匹配查询，而更多的是基于关键字的全文检索查询，例如你查一篇文章信息，你会只输入一些关键字，而不是把整篇文章输入查询（如果有整篇文章也就不用查询了）。而全文索引正是适合这种查询需求。

## 提示找不到存储过程(SQLServer)

在sql server 里新建了几个存储过程，每次都是建了之后，存储过程是可以看见的，但用exec语句的时候，却一直有红色波浪线提示找不到存储过程，但是直接执行，却又是可以执行成功的，每次都需要重新打开ssms，红色的波浪线提示才会取消。
原因是这样的.你的SQL Server 客户端，在连接到 SQL Server 数据库以后。会自动读取数据库的数据字典信息。也就是当前数据库，有哪些表/字段/视图/存储过程等基础信息。保存在客户端的内存里面。这样。当你在客户端输入 SQL 语句的时候，输入表名字.会自动弹出这个表的字段列表让你选择。但是当你新建了一个对象的时候，例如表或者上面那个例子，新建存储过程abc这个时候，数据库那里已经有存储过程abc 了。但是客户端的缓存里面并没有存储过程 abc 的信息。因为内存里面的信息没有更新。因此在客户端那里。输入EXEC abc，abc下有红线。将客户端关闭后，重新打开，由于客户端重新加载了数据库的基础信息。知道了当前数据库里面，有一个名字叫 abc 的存储过程，因此就不出红线了。



# Oracle Database

* Oracle Database DownLoad: http://www.oracle.com/technetwork/cn/database/enterprise-edition/downloads/index.html
* Documents: http://docs.oracle.com/en/database/
* Database Reference: http://docs.oracle.com/cd/B28359_01/server.111/b28320/index.htm
* Database SQL Language Reference: http://docs.oracle.com/cd/B28359_01/server.111/b28286/index.htm
* Listener Control Utility (LSNRCTL): http://docs.oracle.com/cd/A87861_01/NT817EE/network.817/a76933/controlu.htm#433891
* Database Concepts: http://docs.oracle.com/database/121/CNCPT/toc.htm
* The differences of "on delete cascade" and "on delete set null": http://docs.oracle.com/cd/B28359_01/server.111/b28286/clauses002.htm (search "on delete")
* Database Error Messages: http://docs.oracle.com/cd/B28359_01/server.111/b28278/toc.htm
* 3 Starting Up and Shutting Down: http://docs.oracle.com/database/121/ADMIN/start.htm
* 5 Introduction to LOBs: http://docs.oracle.com/cd/B10500_01/appdev.920/a96583/cci05lob.htm
* E Managing Oracle Database Port Numbers: http://docs.oracle.com/cd/B19306_01/install.102/b15667/app_port.htm
* Configuring the Operating System Environment Variables: http://docs.oracle.com/database/121/ADMQS/GUID-EC18C4A6-3BA5-4C14-9D76-B0DD62FEFFF2.htm#ADMQS12369
* 1 Administering Oracle Database: http://docs.oracle.com/database/121/UNXAR/admin_ora.htm#UNXAR001
* 9 Managing Diagnostic Data: http://docs.oracle.com/database/121/ADMIN/diag.htm#ADMIN11007
* 12 Managing Archived Redo Log Files: http://docs.oracle.com/database/121/ADMIN/archredo.htm#ADMIN008
* 3 Setting Up a Globalization Support Environment: http://docs.oracle.com/database/121/NLSPG/ch3globenv.htm#NLSPG003
* 12 Logical Storage Structures: http://docs.oracle.com/database/121/CNCPT/logical.htm#CNCPT004

* Oracle SQL Developer: http://www.oracle.com/technetwork/developer-tools/sql-developer/overview/index.html
* Instant Client Downloads for Microsoft Windows (32-bit): http://www.oracle.com/technetwork/topics/winsoft-085727.html

* Oracle SQL Handler：http://www.heartblue.cn/
* SI Object Browser：http://www.presoft.com.cn/ob/

* ToadWorld: http://www.toadworld.com/

* Oracle 11g安装图文攻略: http://jingyan.baidu.com/article/9f7e7ec04c14c76f29155465.html
* oracle 11g如何完全卸载: http://jingyan.baidu.com/article/922554468d4e6b851648f4e3.html
* win7_oracle11g_64位连接32位PLSQL_Developer: http://jingyan.baidu.com/article/fb48e8be4c7c206e622e1491.html
* Oracle 11g 如何创建数据库：http://jingyan.baidu.com/article/cbcede07cf42ef02f40b4dc2.html
* 数据库使用详解：[3]SQL Developer如何配置：http://jingyan.baidu.com/article/e4511cf33f289e2b845eafb6.html
* oracle的各版本发行时间及特点: http://blog.csdn.net/dream19881003/article/details/7178357
* oracle客户端软件的说明：http://blog.csdn.net/haiross/article/details/17917637
* 怎么判断oracle客户端、服务器端的位数：http://blog.csdn.net/linghe301/article/details/8471945
* oracle数据导入与导出: http://blog.csdn.net/loadrunn/article/details/7283441
* EXECUTE IMMEDIATE 常见使用方法: http://blog.itpub.net/27042095/viewspace-739404/
* Oracle11g自带的SQL developer无法打开解决方案(百度文库)： http://wenku.baidu.com/link?url=scHbokjqF7nK8kca00Pxrm8uaUmm7HNkgXLGaq0tNU-9T2zOrc08oZ7YJkXagD-QbQUmQl7c1wiZNigvIZ9YNVwMU9qIgxBI34HfkM8kWdO
* 【Foreign Key】Oracle外键约束三种删除行为 : http://blog.itpub.net/519536/viewspace-630034/
* Oracle导入JAR包并调用Java: http://www.jianshu.com/p/4280ac298ded
* Reclaiming Unused LOB Space: http://www.idevelopment.info/data/Oracle/DBA_tips/LOBs/LOBS_85.shtml
* sqlplus 汉字乱码问题的解决: http://blog.csdn.net/tianlesoftware/article/details/5224448
* Oracle 10g: Issue with startup mount command (ORA-24324, ORA-01041): http://stackoverflow.com/questions/12470893/oracle-10g-issue-with-startup-mount-command-ora-24324-ora-01041
* 你所不知道的OERR: http://blog.163.com/jet_it_life/blog/static/2050970832012320146595/
* 第9 章 HWM 与数据库性能的探讨: Oracle 数据库性能优化
* Oracle数据库shutdown immediate被hang住的几个原因: http://www.cnblogs.com/kerrycode/p/3506430.html
* Oracle JDBC 连接卡死后 Connection Reset: http://www.cnblogs.com/lailailai/p/4055670.html


## PL/SQL Developer

* http://www.allroundautomations.com/registered/plsqldev.html
* 配置：localhost:1521/orcl

## navicat 连接Oracle 报错：Cannot load OCI DLL, 126

windows Server 2008 服务器上安装了Oracle 11g R2，在用Navicat去连接Oracle时，提示以下错误：

    Cannot load OCI DLL, 126: Instant Client package is required for Baic and TNS connection ，For more information: http://wiki.navicat.com/wiki/index.php/Instant_client_required

查看上述链接页面提示，Navicat only support 32-bit instant client， 因此，尽管我们安装了64位的Oracle，但由于Navicat仅支持32位的，因此我们还需下载一个32位的客户端， 下载地址：

    http://www.oracle.com/technetwork/topics/winsoft-085727.html。

以下为完整的解决方法：

* 在上述地址中下载文件：instantclient-basic-nt-12.1.0.2.0.zip,
* 解压此安装包至：D:/app/administrator/product/instantclient_2_2_x32
* 打开Navicat，选择工具→选项→其他→OCI，然后设置OCI library为：D:app/administrator/product/instantclient_12_2_x32/oci.dll，设置SQL  plus为：D:/app/administrator/product/11.2.0/dbhome_1/BIN/sqlplus.exe。确定。
* 测试成功。



## Oracle 11g 默认用户名和密码

安装ORACLE时，若没有为下列用户重设密码，则其默认密码如下：

用户名/密码                登录身份                说明

sys/change_on_install      SYSDBA 或 SYSOPER       不能以 NORMAL 登录，可作为默认的系统管理员

system/manager             SYSDBA 或 NORMAL        不能以 SYSOPER 登录，可作为默认的系统管理员

sysman/oem_temp            sysman                  为 oms 的用户名

scott/tiger                NORMAL                  普通用户

aqadm/aqadm               SYSDBA 或 NORMAL        高级队列管理员

Dbsnmp/dbsnmp              SYSDBA 或 NORMAL        复制管理员


登录身份：指登录时的Role指定，oracle11g中分SYSDBA和default两种。在安装Oracle 10g的时候，提示创建数据库，在创建的同时提示你输入口令，若此时你输入了密码，在登录数据库的时候用户名sys 对应的密码就应该是你创建数据库时候输入的口令。而非默认的change_on_install.



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


## 使sqlplus中方向键可用

使Unix下的sqlplus/rman也像windows下sqlplus/rman命令一样，可以通过左右箭头修改命令，通过上下箭头查看命令历史。The rlwrap (readline wrapper) utility provides a command history and editing of keyboard input for any other command. This is a really handy addition to SQL*Plus and RMAN on Linux. 而rlwrap会用到readline包，首先要安装readline，然后安装rlwrap。

### 下载

* readline下载：http://directory.fsf.org/project/readline/
* rlwrap下载：http://utopia.knoware.nl/~hlub/uck/rlwrap/

### 安装（使用root登陆，平台是Solaris，其它类似）
```
    # install readline：
    gunzip readline-5.0.tar.gz
    tar xvf readline-5.0.tar
    cd readline-5.0
    ./configure
    make
    make install

    # install rlwrap：
    gunzip rlwrap-0.30.tar.gz
    tar xvf rlwrap-0.30.tar
    cd rlwrap-0.30
    ./configure
    make
    make check
    make install
```

### 使用

# rlwrap sqlplus user/pwd@testdb

可以设别名放到.bash_porfile里，然后直接使用别名即可。

    alias rlsqlplus='rlwrap sqlplus'
    source ~/.bash_porfile

## Oracle安装错误ora-00922（缺少或无效选项）

安装Oracle 11g R2的过程中，在新建数据库实例时出现了该错误，如果选择"忽略"就会出现ora-28000错误。经网络查询验证，这是属于在前面配置管理员密码的时候，采用了数字开头的密码，Oracle貌似对此不支持，但当时不提示出错，晕倒！据说包含其他非法特殊字符也可能产生此问题。

ORA-00922: 选项缺失或无效

错误原因：一般是语句的语法有问题。比如命名不对，关键字写错等等。对于非标准的命名，一般采用双引号来创建。

标识符命名规则:

* 必须以字母开始。
* 长度不能超过30个单字节字符。
* 只能包括A-Z，a-z，0-9，_，$和#。
* 不能在相同用户下建立两个同名的对象。
* 不能使用保留字和关键字

ORA-28000: 账户锁定

* 使用PL/SQL，登录名为system,数据库名称不变，选择类型的时候把Normal修改为Sysdba;
* 选择myjob,查看users;
* 选择system,右击点击“编辑”；
* 修改密码，把“帐户被锁住”的勾去掉；
* 点击“应用”再点击“关闭”；
* 重新登录就可以通过验证了

## oracle emca常用命令

```
    $emctl stop dbconsole
    $emca -r 修复完毕，dbconsole 可以正常使用了

    创建一个EM资料库
    emca -repos create

    重建一个EM资料库
    emca -repos recreate
    删除一个EM资料库
    emca -repos drop
    配置数据库的 Database Control
    emca -config dbcontrol db
    删除数据库的 Database Control配置
    emca -deconfig dbcontrol db
    重新配置db control的端口，默认端口在1158
    emca -reconfig ports
    emca -reconfig ports -dbcontrol_http_port 1160
    emca -reconfig ports -agent_port 3940
    先设置ORACLE_SID环境变量后,启动EM console服务
    emctl start dbconsole
    emctl stop dbconsole
    emctl status dbconsole
    重新配置dbconsole的步骤
    emca -repos drop 删除DBConsole
    emca -repos create 重建
    emca -config dbcontrol db 配置
    emctl start dbconsole 启动
```


```sql
    -- Windows下以管理员身份启动数据库
    net start oracleserviceorcl -- 后面的orcl是你安装的数据库实例名
    net start oracleoradb11g_home1tnslistener --非必须

    -- linux下以sysdba用户登录，然后启动数据库
    sqlplus / as sysdba
    startup

    -- sqlplus登陆方式
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


    desc v$database; --查询v$database数据库的表结构



    --在sqlplus中执行sql脚本，下面两种方式都可以
    START file_name
    @file_name


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

    --ORACLE 判断序列是否存在,如果存在就删除

    declare
     V_NUM number;

    BEGIN
      ----多次删除时，每次都将v_num设置成为0
        V_NUM := 0;
        ----判断序列 seq_name_1 是否存在（区分大小写）
        select count(0) into V_NUM from user_sequences where sequence_name = 'SEQ_BUSINESS_PROCESS_INDEX_ID';
        ----如果存在立即删除
        if V_NUM > 0 then
        execute immediate 'DROP SEQUENCE  SEQ_BUSINESS_PROCESS_INDEX_ID';
        end if;
    END;


    -- 设置sqlplus模式显示总行数
    show pagesize; --查看当前的pagesize
    set pagesize 300;

    -- 设置sqlplus模式显示行宽度
    show linesize; --查看当前的linesize
    set linesize 300;

    -- 修改安装目录glogin.sql文件才能保证之前的设置永久生效
    set pagesize 300;
    set linesize 300;


   

    -- 删除表对象
    select 'drop table '||segment_name from dba_segments where owner='VPMUSER' and segment_type='TABLE';
    -- 创建表对象
    select
    'create table '||segment_name || ' as select * from '||segment_name ||'@DBLINK'
    from dba_segments where owner='VPMUSER' and segment_type='TABLE';

    -- 检查表是否完整导入
    select segment_name from dba_segments@aaa where owner='VPMUSER' and segment_type='TABLE'
    and (segment_name not like 'BIN$%'
    and segment_name not like '%201%')
    minus
    select segment_name from dba_segments where owner='VPMUSER' and segment_type='TABLE'  and segment_name not like 'BIN$%'


    --查询用户所有表的语句1
    select t.table_name,t.comments from user_tab_comments t

    --查询用户所有表的语句2:
    select r1, r2, r3, r5
    from (select a.table_name r1, a.column_name r2, a.comments r3
              from user_col_comments a),
           (select t.table_name r4, t.comments r5 from user_tab_comments t)
    where r4 = r1


    -- 查找表的所有索引（包括索引名，类型，构成列）：
    select t.*,i.index_type from user_ind_columns t,user_indexes i where t.index_name = i.index_name and t.table_name = i.table_name and t.table_name = 要查询的表
    -- 查找表的主键（包括名称，构成列）：
    select cu.* from user_cons_columns cu, user_constraints au where cu.constraint_name = au.constraint_name and au.constraint_type = 'P' and au.table_name = 要查询的表

    -- 查找表的唯一性约束（包括名称，构成列）：
    select column_name from user_cons_columns cu, user_constraints au where cu.constraint_name = au.constraint_name and au.constraint_type = 'U' and au.table_name = 要查询的表

    -- 查找表的外键（包括名称，引用表的表名和对应的键名，下面是分成多步查询）：
    select * from user_constraints c where c.constraint_type = 'R' and c.table_name = 要查询的表

    -- 查询外键约束的列名：
    select * from user_cons_columns cl where cl.constraint_name = 外键名称

    -- 查询引用表的键的列名：
    select * from user_cons_columns cl where cl.constraint_name = 外键引用表的键名

    -- 查询表的所有列及其属性
    select t.*,c.COMMENTS from user_tab_columns t,user_col_comments c where t.table_name = c.table_name and t.column_name = c.column_name and t.table_name = 要查询的表
    
	
	--备份表数据
	create table emp as select * from scott.emp

	--还原表数据
	insert into emp select * from scott.emp
	
	--查看已经执行过的sql这些是存在共享池中的，用户名需要大写，必须具有DBA 的权限
	select * from v$sqlarea t where t.PARSING_SCHEMA_NAME in ('用户名') order by t.LAST_ACTIVE_TIME desc
	
	
	--ORACLE11G 字符集更改（这里更改为AL32UTF8）
	sqlplus sys as sysdba

	--执行下面命令，有可能造成数据库中已有数据混乱的情况，所以在进行操作前，要进行数据库的备份操作
    shutdown immediate;
    STARTUP MOUNT;
    ALTER SESSION SET SQL_TRACE=TRUE;
    ALTER SYSTEM ENABLE RESTRICTED SESSION;
    ALTER SYSTEM SET JOB_QUEUE_PROCESSES=0;
    ALTER SYSTEM SET AQ_TM_PROCESSES=0;
    ALTER DATABASE OPEN;
    ALTER DATABASE character set INTERNAL_USE AL32UTF8;
    ALTER SESSION SET SQL_TRACE=FALSE;
    shutdown immediate;
    startup;

	--察看 NLS_LANG 信息：
    SELECT parameter, value FROM v$nls_parameters WHERE parameter LIKE '%CHARACTERSET';

```

## linux/unix平台Oracle sqlplus 中Backspace无法删除字符

Oracle sqlplus在打错字符时我们可以使用ctrl+backspace组合键实现删除功能。但是你一定要使用Backspace键删除的话，会出现^H，无法删除。这是因为linux中对tty设备的字符转换没有配置好，可通过stty命令修改终端配置来实现Backspace删除功能。具体修改办法如下：

```shell
    [oracle@www.yeserver.com ~]$ id
    uid=800(oracle) gid=803(oinstall) groups=800(dba),801(oper),803(oinstall)
    [oracle@www.yeserver.com ~]$ stty erase ^h
```

若要恢复Ctrl+Backspace组合键删除功能，可执行以下命令:

```shell
    [oracle@www.yeserver.com ~]$ id
    uid=800(oracle) gid=803(oinstall) groups=800(dba),801(oper),803(oinstall)
    [oracle@www.yeserver.com ~]$ stty erase ^?
```

同时可通过stty -a查看所有的终端设置

```shell
    [oracle@www.yeserver.com ~]$ id
    uid=800(oracle) gid=803(oinstall) groups=800(dba),801(oper),803(oinstall)
    [oracle@www.yeserver.com ~]$ stty -a
    speed 38400 baud; rows 37; columns 122; line = 0;
    intr = ^C; quit = ^\; erase = ^?; kill = ^U; eof = ^D; eol = ; eol2 = ; swtch = ; start = ^Q;
    stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O; min = 1; time = 0;
    -parenb -parodd cs8 -hupcl -cstopb cread -clocal -crtscts -cdtrdsr
    -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany -imaxbel -iutf8
    opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
    isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke
```


## oracle 的修改SID

1、检查原来的数据库实例名（sid）

    oracle@oracle[/home/oracle]> echo $ORACLE_SID
    orcl
    oracle@oracle[/home/oracle]> sqlplus / as sysdba
    SQL*Plus: Release 10.2.0.1.0 - Production on Sun Dec 20 11:14:49 2009
    Copyright (c) 1982, 2005, Oracle. All rights reserved.
    Connected to:
    Oracle Database 10g Enterprise Edition Release 10.2.0.1.0 - Production
    With the Partitioning, OLAP and Data Mining options
    sys@ORCL> select instance from v$thread;
    INSTANCE
    --------------------------------------------------------------------------------
    orcl

2、关闭数据库

注意不能用shutdown abort，只能是shutdown immediate或shutdown normal

    sys@ORCL> shutdown immediate
    Database closed.
    Database dismounted.
    ORACLE instance shut down.
    sys@ORCL> exit
    Disconnected from Oracle Database 10g Enterprise Edition Release 10.2.0.1.0 - Production
    With the Partitioning, OLAP and Data Mining options

3、修改oracle用户的ORACLE_SID环境变量，如由orcl修改为ybbe

4、修改/etc/oratab文件，将sid名由旧的修改为新的，如从orcl修改为ybbe

5、进入到$ORACLE_HOME/dbs目录，将所有文件名中包含原来的sid的修改为对应的新sid的。如我对如下文件修改为其后对应的文件

    hc_orcl.dat->hc_ybbe.dat
    lkORCL->lkYBBE
    orapworcl->orapwybbe
    snapcf_orcl.f->snapcf_cnhtm.f
    spfileorcl.ora->spfilecnhtm.ora
    cd $ORACLE_HOME/dbs
    orapwd file=orapwybbe password='ybbe' entries=5 force=y

可以用命令进行对上面的文件进行自动生成

6、使新修改的ORACLE_SID环境变量生效

    oracle@oracle[/oracle/app/10.1/dbs]> . ~/.bash_profile
    oracle@oracle[/oracle/app/10.1/dbs]> echo $ORACLE_SID
    cnhtm

7、重建口令文件

因为口令文件改名后不能在新实例中使用，所以重建

    oracle@oracle[/oracle/app/10.1/dbs]> orapwd file=$ORACLE_HOME/dbs/orapw$ORACLE_SID password=oracle entries=5 force=y
    oracle@oracle[/oracle/app/10.1/dbs]> ls -lrt orapw*
    -rw-r----- 1 oracle oinstall 2048 Dec 20 11:27 orapwybbe

8、启动数据库

    oracle@oracle[/oracle/app/10.1/dbs]> sqlplus / as sysdba
    SQL*Plus: Release 10.2.0.1.0 - Production on Sun Dec 20 11:29:53 2009
    Copyright (c) 1982, 2005, Oracle. All rights reserved.
    Connected to an idle instance.
    idle> startup
    ORACLE instance started.
    Total System Global Area 167772160 bytes
    Fixed Size 1218292 bytes
    Variable Size 62916876 bytes
    Database Buffers 96468992 bytes
    Redo Buffers 7168000 bytes
    Database mounted.
    Database opened.

9、检查数据库实例名。通过如下语句检查数据库实例名，发现实例名已经由orcl变成ybbe

    select instance from v$thread;
    INSTANCE

## ESCAPE关键字用法

　　定义：escape关键字经常用于使某些特殊字符，如通配符：'%','_'转义为它们原来的字符的意义，被定义的转义字符通常使用'\',但是也可以使用其他的符号。实例：

    SQL> select * from t11 where name like '%_%';
    SQL> select * from t11 where name like '%\_%' escape '\';

注意：如果是 '/' 作为检索字符， 必须 用 '/' 作为转义符， 正斜扛也一样。

    select * from wan_test where psid like '%//%' escape '/'

1.使用 ESCAPE 关键字定义转义符。在模式中，当转义符置于通配符之前时，该通配符就解释为普通字符。
2.ESCAPE 'escape_character' 允许在字符串中搜索通配符而不是将其作为通配符使用。escape_character 是放在通配符前表示此特殊用途的字符。


## Oracle中session和processes的设置

* PROCESSES: http://docs.oracle.com/cd/B28359_01/server.111/b28320/initparams188.htm#sthref560
* SESSIONS: http://docs.oracle.com/cd/B28359_01/server.111/b28320/initparams220.htm#sthref647
* TRANSACTIONS: http://docs.oracle.com/cd/B28359_01/server.111/b28320/initparams248.htm

* Oracle 11gR2之前：sessions=(1.1*processes) + 5
* Oracle 11gR2之后：sessions=(1.5*porcesses) + 22

当Oracle需要启动新的process而又已经达到processes参数时，就会报错：

```shell
    00020, 00000, "maximum number of processes (%s) exceeded"
    // *Cause: All process state objects are in use.
    // *Action: Increase the value of the PROCESSES initialization parameter.
```

当数据库连接的并发用户已经达到sessions这个值时，又有新session连进来，就会报错

```shell
    00018, 00000, "maximum number of sessions exceeded"
    // *Cause: All session state objects are in use.
    // *Action: Increase the value of the SESSIONS initialization parameter.
```

如何使用sqlplus查看、修改processes呢？使用sys，以sysdba权限登录：

```shell
    show parameter processes; --显示：processes integer 150
	show parameter sessions; --显示：sessions integer 165
	select count(*) from v$process; --显示当前processes数目
	select  count(*) from v$session; --显示当前sessions数目
    alter system set processes=400 scope = spfile; --显示系统已更改
    show parameter processes; --显示：processes integer 150
    create pfile from spfile; --显示：文件已创建。

    --重启数据库
    shutdown immediate;
    startup
    
    --重启监听
    lsnrctl stop/start/status

    show parameter processes; --显示：processes integer 400
    show parameter session; --显示：sessions integer 445
```

## 忘记oracle的sys用户密码怎么修改

### 忘记除SYS、SYSTEM用户之外的用户的登录密码

    CONN SYS/PASS_WORD AS SYSDBA; --用SYS (或SYSTEM)用户登录
    ALTER USER user_name IDENTIFIED BY "newpassword"; --修改用户的密码，密码不能是数字开头，否则会出现：ORA-00988: 口令缺失或无效

### 忘记SYS用户，或者是SYSTEM用户的密码

    CONN SYS/PASS_WORD AS SYSDBA; --如果是忘记SYSTEM用户的密码，可以用SYS用户登录。
    ALTER USER SYSTEM IDENTIFIED BY "newpassword";

    CONN SYSTEM/PASS_WORD AS SYSDBA; --如果是忘记SYS用户的密码，可以用SYSTEM用户登录。
    ALTER USER SYS IDENTIFIED BY "newpassword";

### SYS,SYSTEM用户的密码都忘记

Oracle提供了两种验证方式，一种是OS验证，另一种密码文件验证方式，如果是第一种方式用以下方法修改密码：

```sql
　　sqlplus /nolog;
　　connect / as sysdba
　　alter user sys identified by newpassword;
　　alter user system identified by newpassword;
```

如果是第二种方法可以使用ORAPWD.EXE 工具修改密码。打开命令提示符窗口，输入如下命令：

    orapwd file=D:\oracle10g\database\pwdctcsys.ora password=newpassword

这个命令重新生成了数据库的密码文件。密码文件的位置在ORACLE_HOME目录下的\database目录下。这个密码是修改sys用户的密码。除sys其他用户的密码不会改变。也可以下方法修改密码，设定完后，重新启动服务，再次登陆就可以了。

    orapwd file=pwdxxx.ora password=newpassword entries=10


# DB2

* 官网：http://www-01.ibm.com/software/data/db2/
* DB2China：http://www.db2china.net/


# Oracle Berkeley DB

* Oracle Berkeley DB：http://www.oracle.com/technetwork/database/database-technologies/berkeleydb/overview/index.html


# SQLite

* http://www.sqlite.org/
* DB Browser for SQLite: http://sqlitebrowser.org/
* SQLite Expert: http://www.sqliteexpert.com/index.html


# mongodb

* https://www.mongodb.org/
* https://docs.mongodb.org/manual/
* http://api.mongodb.org/java/
* MonjaDB (MongoDB GUI client tool) : http://www.jumperz.net/index.php?i=2&a=0&b=9
* mongolab: https://mongolab.com/
* Spring Data MongoDB hello world example: http://www.mkyong.com/mongodb/spring-data-mongodb-hello-world-example/
* MongoDB设置访问权限、设置用户: http://www.cnblogs.com/zengen/archive/2011/04/23/2025722.html
* 三招解决MongoDB的磁盘IO问题: http://blog.nosqlfan.com/html/3925.html


# MONGOVUE

* http://www.mongovue.com/


# Morphia

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

* GBase: http://www.gbase.cn/
* Vertica: https://www.vertica.com/
* Teradata Aster: http://developer.teradata.com/aster
* actian: http://www.actian.com/
* Apache Derby: http://db.apache.org/derby/

# 数据模型

## PowerDesigner两张表主键如何设成一致的

设置方法：Tools--->Model Options->Model Settings。在Data Item组框中定义数据项的唯一性代码选项(Unique Code)与重用选项（Allow Reuse）。把allow reuse选上，去掉unique code选项。
