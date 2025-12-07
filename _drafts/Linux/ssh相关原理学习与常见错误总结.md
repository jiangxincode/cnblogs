
## SSH基本原理与运用

* SSH原理与运用（一）: 远程登录: http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html
* SSH原理与运用（二）: 远程操作与端口转发: http://www.ruanyifeng.com/blog/2011/12/ssh_port_forwarding.html

## connect to host localhost port 22: Connection refused

参考：http://blog.csdn.net/jszhangyili/article/details/8881807

## Agent admitted failure to sign using the key

ssh-keygen 产生出 id_rsa, id_rsa.pub, 已经都放到正确位置(.ssh), 但是联机时却出现下述讯息:`Agent admitted failure to sign using the key`。解决方法是在自己的机器上, 执行 ssh-add, 会出现: `Identity added: /home/user/.ssh/id_rsa (/home/user/.ssh/id_rsa)`

## sshd相关配置优化

```sh
# 修改/etc/ssh/sshd_config（注意是sshd_config，不是ssh_config）

ClientAliveInterval 60 # 指定服务器向客户端请求消息的时间间隔，默认是0表示不发送；可以改为60表示每分钟发送一次
ClientAliveCountMax 86400 # 表示服务器发出请求后客户端没有响应的次数达到一定值, 就自动断开

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