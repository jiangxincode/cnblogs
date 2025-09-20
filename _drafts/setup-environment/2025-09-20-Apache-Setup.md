## 安装Apache

安装Apache作为HTTP文件下载服务器

```bash
ubuntu@ubuntu:~$ sudo apt-get install apache2
```

尝试启动Apache2服务

```bash
ubuntu@ubuntu:~$ /etc/init.d/apache2 start
Starting apache2 (via systemctl): apache2.service==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to start 'apache2.service'.
Authenticating as: qcloud (ubuntu)
Password:
==== AUTHENTICATION COMPLETE ===
.
```

直接访问<http://124.222.145.48:80/>，既可看到对应的Apache2默认页面。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2025-07-26_12-25-59.png)

存放的目录为`/var/www/html/`，想要下载的文件直接放到这个目录下，然后直接访问既可。

<http://124.222.145.48/download/>

```bash

命令汇总

```bash
# 启动Apache2服务
/etc/init.d/apache2 start

# 查看Apache2服务状态
/etc/init.d/apache2 status

# 停止Apache2服务
/etc/init.d/apache2 stop

# 重启Apache2服务
/etc/init.d/apache2 restart
```