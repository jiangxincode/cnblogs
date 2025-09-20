## Ubuntu 22.04安装Samba

### 下载/安装Samba服务器:
sudo apt-get install samba samba-common

### 配置Samba服务器
首先将默认的配置文件进行备份
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

sudo vim /etc/samba/smb.conf

[jiangxin]
path = /home/jiangxin 
available = yes
browseable = yes
public = yes
writable = yes 
valid users = jiangxin

### 设置密码并重启服务器

sudo smbpasswd -a jiangxin //设置访问的密码
sudo service smbd restart //重启smb服务器

### 访问

在Windows资源管理器导航栏输入`\\ip_adress`，然后输入账号和密码就可以访问了。为了后续方便快速访问Linux侧目录，将远程目录映射为网络驱动器：
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image197.png)


![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image198.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image199.png)

### 其它问题

如果Windows无法访问samba服务器，尝试通过以下方式确认问题所在：

控制面板-系统和安全-Windows Defender 防火墙，关闭防火墙

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image200.png)
控制面板-程序-启用或关闭Windows功能，勾选SMB 1.0/CIFS文件共享支持

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image201.png)
Win+R，输入gpedit.msc，计算器配置-管理模板-网络-Lanman工作站，选中"不安全的来宾登陆"，在新的对话框中选中"已启用"

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image202.png)
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/aloys_build_manual/image203.png)