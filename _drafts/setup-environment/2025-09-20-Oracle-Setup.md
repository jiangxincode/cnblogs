## 安装Oracle
Database Application Development Hands On Labs: http://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html

### 配置网络
[root@vbgeneric ~]# ifconfig

enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.105  netmask 255.255.255.0  broadcast 192.168.1.255
        ether 08:00:27:0c:40:7f  txqueuelen 1000  (Ethernet)
        RX packets 2677  bytes 2476158 (2.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2645  bytes 323609 (316.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 0  (Local Loopback)
        RX packets 473  bytes 111334 (108.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 473  bytes 111334 (108.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:fc:2d:7f  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@vbgeneric ~]# hostname
vbgeneric


[root@vbgeneric ~]# vim /etc/sysconfig/network-scripts/ifcfg-enp0s3

TYPE="Ethernet"
BOOTPROTO="static"
NAME="enp0s3"
UUID="05c05f77-20d5-4842-808d-366b3dc466d4"
DEVICE="enp0s3"
ONBOOT="yes"
IPADDR=192.168.1.145
NETMASK=255.255.255.0

[root@vbgeneric ~]# vim /etc/sysconfig/network

NETWORKING=yes
HOSTNAME=vbgeneric.localdomain
GATEWAY=192.168.1.1

[root@vbgeneric ~]# vim /etc/resolv.conf

nameserver 114.114.114.114
nameserver 8.8.8.8


[root@vbgeneric ~]# service network restart
Restarting network (via systemctl):                        [  OK  ]

### 账号信息
root/oracle



[root@vbgeneric ~]# cat /etc/oracle-release 
Oracle Linux Server release 7.3
[root@vbgeneric ~]# su - oracle
Last login: Sat Sep  2 08:30:31 EDT 2017 on pts/1
[oracle@vbgeneric ~]$ sqlplus / as sysdba

SQL*Plus: Release 12.2.0.1.0 Production on Sat Sep 2 08:39:20 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

ERROR:
ORA-01017: invalid username/password; logon denied


Enter user-name: sys as sysdba
Enter password: 

Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

SQL>

## Windows 10 安装 Oracle Database 11.2g
win64_11gR2_database_1of2.zip、win64_11gR2_database_2of2.zip两个解压到同一个目录
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image109.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image110.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image111.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image112.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image113.png)

Oracle基目录：$ORACLE_BASE
软件位置：$ORACLE_HOME
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image114.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image115.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image116.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image117.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image118.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image119.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image120.png)
## Windows 10 安装 Oracle12c

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image121.jpg)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image122.jpg)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image123.jpg)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image124.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image125.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image126.jpg)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image127.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image128.jpg)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image129.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image130.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image131.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image132.jpg)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image133.jpg)

## 如何利用Oracle VM Templates 在几分钟内部署Oracle Real Application Clusters (RAC) 

### 阅读前准备
阅读本教程前首先需要访问如下地址：
http://www.oracle.com/technetwork/server-storage/vm/downloads/hol-oraclevm-2368799.html

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image134.png)
下载红框标识的ovmm10471.oow.local.ova和ovs10471.oow.local.ova文件，并仔细阅读绿框标识的教程（OOW2015_HOL10471_RAC_20151116，以下简称OOW2015_HOL10471_RAC），本文是针对该教程的补充说明。

另外阅读OOW2015_HOL10471_RAC和本文需要对Oracle VM VirtualBox和Oracle VM有基本的了解，可以访问如下地址：
Oracle VM VirtualBox:
http://www.oracle.com/technetwork/server-storage/virtualbox/overview/index.html
Oracle VM:
http://www.oracle.com/technetwork/server-storage/vm/overview/index.html

### 1 INTRODUCTION
#### 1.1	LAB OBJECTIVE
#### 1.2	PREPARATION (HAS BEEN DONE BEFORE THE LAB)
要想满足和OOW2015_HOL10471_RAC中所述的前提条件，只需要在满足硬件要求的笔记本或者台式机（内存16G以上，CPU 4核以上）中下载安装VirtualBox，进行VirtualBox网络配置，导入之前下载的虚拟机即可。VirtualBox下载地址为：
http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html
下载符合宿主机操作系统的VirtualBox并按照提示进行安装。
安装后需要进行基础网络设置，之所以需要基础网络配置是因为如果想在宿主机中访问Oracle VM Manager虚拟机、Oracle VM Server虚拟机以及Oracle VM Server中Oracle RAC虚拟机，需要让宿主机和虚拟机处于一个网段之中，在OOW2015_HOL10471_RAC的1.3章节中可以知道虚拟机的网段是192.168.56.X，所以需要在Virtualbox中添加一个IP地址为192.168.56.1的网卡。添加网卡的步骤如下：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image135.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image136.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image137.png)

设置之后在【控制面板\网络和 Internet\网络连接】中可以看到配置的网卡
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image138.png)

在cmd或者powershell中执行ipconfig命令，可以发现多了一块网卡：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image139.png)


增加网卡之后需要导入Oracle VM Manager+Oracle VM Server模板。首先导入Oracle VM Manager
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image140.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image141.png)

然后导入Oracle VM Server
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image142.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image143.png)

启动虚拟机，如果出现类似于下面的提示：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image144.png)

则重新进行网络设置：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image145.png)

禁用掉OVS的USB控制器
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image146.png)



启动虚拟机，直到看到如下界面：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image147.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image148.png)

此时在宿主机中ping两台虚拟机的IP地址，应该都是可以ping通的。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image149.png)


#### 1.3	GLOBAL PICTURE
### 2	DETAILED INSTRUCTIONS
#### 2.1	START BOTH SERVERS (VIRTUAL BOX VMS)
#### 2.2	CONNECT TO THE ORACLE VM MANAGER CONSOLE
如果使用最新的Firefox版本（本文写作时的最新版本是Firefox 56），访问https://192.168.56.30:7002/ovm/console时会提示“建立安全连接失败”：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image150.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image151.png)

此时可以使用老版本的Firefox进行访问，47.0版本的Firefox安装包可以从百度网盘进行下载：http://pan.baidu.com/s/1dEBT5df

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image152.png)

安装之后首先设置禁止检查更新，防止后台再次更新升级到最新版本。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image153.png)

继续访问https://192.168.56.30:7002/ovm/console
出现如下图提示时单击“添加例外”

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image154.png)

点击“确认安全例外”
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image155.png)



此时可以看到VM Manager的登陆界面。

#### 2.3	CREATE A STORAGE REPOSITORY
#### 2.4	CLONE 3 VMS FROM DB/RAC ORACLE VM TEMPLATE
#### 2.5 CREATING SHARED DISK FOR ASM CONFIGURATION
在使用ssh连接Oracle VM Manager时如果使用的是Xshell的话，不支持OOW2015_HOL10471_RAC中所提到的ssh命令：
ssh admin@192.168.56.30 -p 10000
需要在图形配置页中进行配置，如下：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image156.png)
### 3	START INSTALLATION USING DEPLOYCLUSTER
#### 3.1	CREATE A NETCONFIG.INI FILE FOR DEPLOYMENT
#### 3.2 RUNNING DEPLOYCLUSTER.PY
在执行deploycluster.py命令时如果出现下图错误说明之前分配给三个虚拟机的资源过少：


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image157.png)

此时在浏览器中修改对应的内存值即可：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image158.png)

安装成功的标志是buildcluster.log中出现如下内容：



![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image159.png)


### 如何关闭、启动系统
OOW2015_HOL10471_RAC中未提及如何关系和启动系统，这里做简要说明。
关闭系统时首先通过浏览器关闭三台VM： 
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image160.png)

待节点状态都是Stopped之后关闭Virtualbox 虚拟机
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image161.png)


启动系统时反过来，先运行Virtualbox虚拟机：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image162.png)

看到如下画面代表Oracle VM Server启动成功：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image163_01.png)

看到如下画面代表Oracle VM Manager启动成功：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image163.png)

然后使用Firefox浏览器打开OVMM控制台：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image164.png)

待所有节点的状态都为Running时，用SSH登陆到racnode0.1节点，执行crsstat -t。当出现如下结果时说明RAC已经启动成功。
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image165.png)


### 常用Oracle RAC相关的命令

```shell
[oracle@racnode01h ~]$ crsctl check css
CRS-4529: Cluster Synchronization Services is online
[oracle@racnode01h ~]$ ps -ef|grep cssd
root      1548     1  0 16:48 ?        00:00:17 /u01/app/12.1.0/grid/bin/cssdmonitor
root      1565     1  0 16:48 ?        00:00:16 /u01/app/12.1.0/grid/bin/cssdagent
oracle    1576     1  1 16:48 ?        00:01:02 /u01/app/12.1.0/grid/bin/ocssd.bin 
oracle    4905  2855  0 18:04 pts/0    00:00:00 grep cssd
[oracle@racnode01h ~]$ crsctl check has
CRS-4638: Oracle High Availability Services is online
[oracle@racnode01h ~]$ ps -ef|grep ohasd.bin
root      1195     1  1 16:47 ?        00:01:06 /u01/app/12.1.0/grid/bin/ohasd.bin reboot
oracle    4932  2855  0 18:05 pts/0    00:00:00 grep ohasd.bin
[oracle@racnode01h ~]$ crs_stat -t
Name           Type           Target    State     Host        
------------------------------------------------------------
ora....SM.lsnr ora....er.type ONLINE    ONLINE    racnode01h  
ora.DATA.dg    ora....up.type ONLINE    ONLINE    racnode01h  
ora....ER.lsnr ora....er.type ONLINE    ONLINE    racnode01h  
ora....AF.lsnr ora....er.type OFFLINE   OFFLINE               
ora....N1.lsnr ora....er.type ONLINE    ONLINE    racnode01h  
ora.asm        ora.asm.type   ONLINE    ONLINE    racnode01h  
ora.cvu        ora.cvu.type   OFFLINE   OFFLINE               
ora.gns        ora.gns.type   ONLINE    ONLINE    racnode01h  
ora.gns.vip    ora....ip.type ONLINE    ONLINE    racnode01h  
ora....network ora....rk.type ONLINE    ONLINE    racnode01h  
ora.oc4j       ora.oc4j.type  OFFLINE   OFFLINE               
ora.ons        ora.ons.type   ONLINE    ONLINE    racnode01h  
ora.oow.db     ora....se.type ONLINE    ONLINE    racnode01h  
ora....1H.lsnr application    ONLINE    ONLINE    racnode01h  
ora....01h.ons application    ONLINE    ONLINE    racnode01h  
ora....01h.vip ora....t1.type ONLINE    ONLINE    racnode01h  
ora....2H.lsnr application    ONLINE    ONLINE    racnode02h  
ora....02h.ons application    ONLINE    ONLINE    racnode02h  
ora....02h.vip ora....t1.type ONLINE    ONLINE    racnode02h  
ora.scan1.vip  ora....ip.type ONLINE    ONLINE    racnode01h  
[oracle@racnode01h ~]$ crsctl status resource -t
--------------------------------------------------------------------------------
Name           Target  State        Server                   State details       
--------------------------------------------------------------------------------
Local Resources
--------------------------------------------------------------------------------
ora.ASMNET1LSNR_ASM.lsnr
               ONLINE  ONLINE       racnode01h               STABLE
               ONLINE  ONLINE       racnode02h               STABLE
ora.DATA.dg
               ONLINE  ONLINE       racnode01h               STABLE
               ONLINE  ONLINE       racnode02h               STABLE
ora.LISTENER.lsnr
               ONLINE  ONLINE       racnode01h               STABLE
               ONLINE  ONLINE       racnode02h               STABLE
ora.LISTENER_LEAF.lsnr
               OFFLINE OFFLINE      racnode03h               STABLE
ora.net1.network
               ONLINE  ONLINE       racnode01h               STABLE
               ONLINE  ONLINE       racnode02h               STABLE
ora.ons
               ONLINE  ONLINE       racnode01h               STABLE
               ONLINE  ONLINE       racnode02h               STABLE
--------------------------------------------------------------------------------
Cluster Resources
--------------------------------------------------------------------------------
ora.LISTENER_SCAN1.lsnr
      1        ONLINE  ONLINE       racnode01h               STABLE
ora.asm
      1        ONLINE  ONLINE       racnode01h               Started,STABLE
      2        ONLINE  ONLINE       racnode02h               Started,STABLE
      3        OFFLINE OFFLINE                               STABLE
ora.cvu
      1        OFFLINE OFFLINE                               STABLE
ora.gns
      1        ONLINE  ONLINE       racnode01h               STABLE
ora.gns.vip
      1        ONLINE  ONLINE       racnode01h               STABLE
ora.oc4j
      1        OFFLINE OFFLINE                               STABLE
ora.oow.db
      1        ONLINE  ONLINE       racnode01h               Open,STABLE
      2        ONLINE  ONLINE       racnode02h               Open,STABLE
ora.racnode01h.vip
      1        ONLINE  ONLINE       racnode01h               STABLE
ora.racnode02h.vip
      1        ONLINE  ONLINE       racnode02h               STABLE
ora.scan1.vip
      1        ONLINE  ONLINE       racnode01h               STABLE
--------------------------------------------------------------------------------
[oracle@racnode01h ~]$ sqlplus / as sysdba

SQL*Plus: Release 12.1.0.2.0 Production on Fri Nov 10 18:14:09 2017

Copyright (c) 1982, 2014, Oracle.  All rights reserved.


Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, Real Application Clusters, Automatic Storage Management, OLAP,
Advanced Analytics and Real Application Testing options

SQL> set linesize 200;
SQL> select * from gv$instance;

   INST_ID INSTANCE_NUMBER INSTANCE_NAME    HOST_NAME							     VERSION	       STARTUP_T STATUS       PAR    THREAD# ARCHIVE LOG_SWITCH_WAIT LOGINS
---------- --------------- ---------------- ---------------------------------------------------------------- ----------------- --------- ------------ --- ---------- ------- --------------- ----------
SHU DATABASE_STATUS   INSTANCE_ROLE	 ACTIVE_ST BLO	   CON_ID INSTANCE_MO EDITION FAMILY
--- ----------------- ------------------ --------- --- ---------- ----------- ------- --------------------------------------------------------------------------------
	 1		 1 OOW1 	    racnode01h							     12.1.0.2.0        10-NOV-17 OPEN	      YES	   1 STOPPED		     ALLOWED
NO  ACTIVE	      PRIMARY_INSTANCE	 NORMAL    NO		0 REGULAR     EE

	 2		 2 OOW2 	    racnode02h							     12.1.0.2.0        10-NOV-17 OPEN	      YES	   2 STOPPED		     ALLOWED
NO  ACTIVE	      PRIMARY_INSTANCE	 NORMAL    NO		0 REGULAR     EE


SQL>
```

## 安装PLSQL Developer 11.0.6

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image166.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image167.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image168.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image169.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image170.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image171.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image172.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image173.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image174.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image175.jpg)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image176.jpg)