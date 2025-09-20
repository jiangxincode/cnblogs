## 安装TeraData(SUSE LINUX Enterprise Server 11)

### 下载、安装VMware-workstation：
VMware-workstation-full-12.5.5-5234757.exe

### 下载、安装TDExpress
TDExpress14.10.03_Sles11_40GB.7z
http://downloads.teradata.com/download/database/teradata-express-for-vmware-player

安装可以参考：
http://downloads.teradata.com/database/articles/teradata-express-14-0-for-vmware-user-guide

### 网络设置

编辑-虚拟网络编辑器

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image107.png)

SUSE静态配置IP成功上网: http://blog.csdn.net/seulww/article/details/17136555
按照上面链接设置之后，发现虚拟机无法ping通网关，经查询是DNS配置没有生效。按照下述步骤处理：

修改ip地址（建议通过GUI配置）
即时生效: ifconfig eth0 192.168.1.155 netmask 255.255.255.0
启动生效:修改/etc/sysconfig/network/ifcfg-eth0
修改default gateway（建议通过GUI配置）
即时生效:route add default gw 192.168.1.1
启动生效:修改/etc/sysconfig/network/ifcfg-eth0
修改dns（不知为何通过GUI配置没有生效）
修改/etc/resolv.conf
修改后可即时生效，启动同样有效（一下为修改的内容）

search localdomain
nameserver 114.114.114.114
nameserver 8.8.8.8

修改host name（建议通过GUI配置）
即时生效:hostname TDExpress
启动生效:修改/etc/HOSTNAME

### 启动报错解决
启动之后可以查看/var/log/boot.msg获取此次开机的报错日志。

问题1：
Error：cannot mount filesystem：Protocol error
Mounting HGFS shares:    FAILED

解决：

在VM->Setting中的Option页面，设置Shared Folders，使之enable 就可以了，这个功能能把host上的目录mount到Guest上的/mnt/hgfs目录，实现共享访问。

问题2：

<notice -- Apr 16 00:58:00.139375000> ipmi start
Starting ipmi drivers: failed
<notice -- Apr 16 00:58:00.379049000> 'ipmi start' exits with status 1

解决：
不影响功能，暂未解决。

### 使用DBeaver进行连接

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image108.png)
