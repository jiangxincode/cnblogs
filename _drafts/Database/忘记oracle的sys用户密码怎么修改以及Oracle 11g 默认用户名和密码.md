
## 忘记除SYS、SYSTEM用户之外的用户的登录密码

    CONN SYS/PASS_WORD AS SYSDBA; --用SYS (或SYSTEM)用户登录
    ALTER USER user_name IDENTIFIED BY "newpassword"; --修改用户的密码，密码不能是数字开头，否则会出现：ORA-00988: 口令缺失或无效

## 忘记SYS用户，或者是SYSTEM用户的密码

    CONN SYS/PASS_WORD AS SYSDBA; --如果是忘记SYSTEM用户的密码，可以用SYS用户登录。
    ALTER USER SYSTEM IDENTIFIED BY "newpassword";

    CONN SYSTEM/PASS_WORD AS SYSDBA; --如果是忘记SYS用户的密码，可以用SYSTEM用户登录。
    ALTER USER SYS IDENTIFIED BY "newpassword";

## SYS,SYSTEM用户的密码都忘记

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