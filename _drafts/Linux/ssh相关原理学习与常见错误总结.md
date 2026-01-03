
## SSH基本原理与运用

* SSH原理与运用（一）: 远程登录: http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html
* SSH原理与运用（二）: 远程操作与端口转发: http://www.ruanyifeng.com/blog/2011/12/ssh_port_forwarding.html

## connect to host localhost port 22: Connection refused

参考：http://blog.csdn.net/jszhangyili/article/details/8881807

## Agent admitted failure to sign using the key

ssh-keygen 产生出 id_rsa, id_rsa.pub, 已经都放到正确位置(.ssh), 但是联机时却出现下述讯息:`Agent admitted failure to sign using the key`。解决方法是在自己的机器上, 执行 ssh-add, 会出现: `Identity added: /home/user/.ssh/id_rsa (/home/user/.ssh/id_rsa)`

## ssh长时间误操作断开

```sh
# 修改/etc/ssh/sshd_config（注意是sshd_config，不是ssh_config）

ClientAliveInterval 60 # 指定服务器向客户端请求消息的时间间隔，默认是0表示不发送；可以改为60表示每分钟发送一次
ClientAliveCountMax 86400 # 表示服务器发出请求后客户端没有响应的次数达到一定值, 就自动断开
```

ubuntu@ubuntu:~$ sudo service ssh restart

* 如果使用MobaXterm，需要开启keepalive功能：Settings -> Configuration -> SSH -> SSH keepalive
* 同时注意电脑的电源管理设置，避免进入睡眠模式。

## root用户通过ssh登录

```sh
# 修改/etc/ssh/sshd_config（注意是sshd_config，不是ssh_config）
PermitRootLogin yes # 允许root用户登录
```

ubuntu@ubuntu:~$ sudo service ssh restart

## sftp子系统申请已拒绝 请确保ssh连接的sftp子系统设置有效

```shell
vi /etc/ssh/sshd_config

# 取消下面这一行的注释
Subsystem       sftp /usr/libexec/openssh/sftp-server

/etc/init.d/sshd reload
```

## too many authentication failures for root

使用xshell提示此问题，但可以通过Putty登录系统。
打开文件 /etc/ssh/sshd_config
修改 MaxAuthTries 这个参数的值，不建议修改太大。

## Xshell利用登录脚本从服务器登录到另外一个服务器

通过脚本设置，可以实现从这个服务器登录到另外一个服务器。打开Xshell 4的会话属性（【文件】->【属性】），左边的类别下选择【登录脚本】，在右边底下你可以看到有个【连接会话时运行脚本】的复选框。

登录脚本的格式如下：

```VBS
Sub Main
    xsh.Screen.Send "ssh 用户名@服务器地址"
    xsh.Screen.Send VbCr
    xsh.Screen.WaitForString "password: "
    xsh.Screen.Send "登录密码"
    xsh.Screen.Send VbCr
End Sub
```

将上面内容保存成一个vbs后缀的文件（最好保存到Xshell安装文件下面），准备好脚本文件后在Xshell中打开

会话属性，勾选【连接会话时运行脚本】这个复选框，选择刚才保存的那个vbs后缀的文件就可以了。

如果想进一步了解Xshell支持的脚本API，可以查看Xshell的帮助文档。
