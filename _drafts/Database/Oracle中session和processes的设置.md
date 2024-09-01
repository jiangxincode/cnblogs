欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju


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