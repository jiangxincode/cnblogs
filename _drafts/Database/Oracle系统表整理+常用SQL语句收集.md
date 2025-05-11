
```
-- DBA/ALL/USER/V_$/GV_$/SESSION/INDEX开头的绝大部分都是视图
-- DBA_TABLES意为DBA拥有的或可以访问的所有的关系表。
-- ALL_TABLES意为某一用户拥有的或可以访问的所有的关系表。
-- USER_TABLES意为某一用户所拥有的所有的关系表。
-- 当某一用户本身就为数据库DBA时，DBA_TABLES与ALL_TABLES等价。
-- DBA_TABLES >= ALL_TABLES >= USER_TABLES
-- 需要注意的是在ORACLE数据库中大小写是敏感的，而此三表中数据默认都是大写的，所以在进行查询的时候注意小写的数据可能会造成数据无法查到。

SELECT * FROM dba_views WHERE view_name LIKE 'DBA%';
SELECT * FROM dba_views WHERE view_name LIKE 'ALL%';
SELECT * FROM dba_views WHERE view_name LIKE 'USER%';
SELECT * FROM dba_views WHERE view_name LIKE 'V_$%'; -- 针对某个实例的视图
SELECT * FROM dba_views WHERE view_name LIKE 'GV_$%'; -- 全局视图，针对多个实例环境
SELECT * FROM dba_views WHERE view_name LIKE 'SESSION%';
SELECT * FROM dba_views WHERE view_name LIKE 'INDEX%';

SELECT count(1) FROM dba_tables;
SELECT count(1) FROM all_tables;
SELECT count(1) FROM user_tables;

-- V$/GV$开头的绝大部分都是V_$/GV_$表的别名
SELECT * FROM dba_synonyms WHERE synonym_name LIKE 'V$%';
SELECT * FROM dba_synonyms WHERE synonym_name LIKE 'GV$%';

-- X$没有对应的X_$
SELECT * FROM dba_synonyms WHERE synonym_name LIKE 'X$%';


-- 比较常用的DBA开头的视图有
select * from dba_users; --数据库用户信息
select * from dba_roles; --角色信息
select * from dba_segments; --表段信息
select * from dba_extents; --数据区信息
select * from dba_objects; --数据库对象信息
select * from dba_lobs; --lob数据信息
select * from dba_tablespaces; --数据库表空间信息
select * from dba_data_files; --数据文件设置信息
select * from dba_temp_files; --临时数据文件信息
select * from dba_rollback_segs; --回滚段信息
select * from dba_ts_quotas; --用户表空间配额信息
select * from dba_free_space; --数据库空闲空间信息
select * from dba_profiles; --数据库用户资源限制信息
select * from dba_sys_privs; --用户的系统权限信息
select * from dba_tab_privs; --用户具有的对象权限信息
select * from dba_col_privs; --用户具有的列对象权限信息
select * from dba_role_privs; --用户具有的角色信息
select * from dba_audit_trail; --审计跟踪记录信息
select * from dba_stmt_audit_opts; --审计设置信息
select * from dba_audit_object; --对象审计结果信息
select * from dba_audit_session; --会话审计结果信息
select * from dba_indexes; --用户模式的索引信息


-- 比较常用的ALL开头的视图有
select * from all_users; --数据库所有用户的信息
select * from all_objects; --数据库所有的对象的信息
select * from all_def_audit_opts; --所有默认的审计设置信息
select * from all_tables; --所有的表对象信息
select * from all_indexes; --所有的数据库对象索引的信息
select * from all_tab_comments; --查询所有用户的表,视图等
select * from all_col_comments; --查询所有用户的表的列名和注释.
select * from all_tab_columns; --查询所有用户的表的列名等信息(详细但是没有备注)


-- 比较常用的ALL开头的视图有
select * from user_objects; --用户对象信息
select * from user_source; --数据库用户的所有资源对象信息
select * from user_segments; --用户的表段信息
select * from user_tables; --用户的表对象信息
select * from user_tab_columns; --用户的表列信息
select * from user_constraints; --用户的对象约束信息
select * from user_sys_privs; --当前用户的系统权限信息
select * from user_tab_privs; --当前用户的对象权限信息
select * from user_col_privs; --当前用户的表列权限信息
select * from user_col_comments; -- 查询本用户的表的列名和注释
select * from user_role_privs; --当前用户的角色权限信息
select * from user_indexes; --用户的索引信息
select * from user_ind_columns; --用户的索引对应的表列信息
select * from user_cons_columns; --用户的约束对应的表列信息
select * from user_clusters; --用户的所有簇信息
select * from user_clu_columns; --用户的簇所包含的内容信息
select * from user_cluster_hash_expressions; --散列簇的信息


-- 比较常用的V$开头的别名有
select * from v$database; --数据库信息
select * from v$datafile; --数据文件信息
select * from v$controlfile; --控制文件信息
select * from v$logfile; --重做日志信息
select * from v$instance; --数据库实例信息
select * from v$log; --日志组信息
select * from v$loghist; --日志历史信息
select * from v$sga; --数据库SGA信息
select * from v$parameter; --初始化参数信息
select * from v$process; --数据库服务器进程信息
select * from v$bgprocess; --数据库后台进程信息
select * from v$controlfile_record_section; --控制文件记载的各部分信息
select * from v$thread; --线程信息
select * from v$datafile_header; --数据文件头所记载的信息
select * from v$archived_log; --归档日志信息
select * from v$archive_dest; --归档日志的设置信息
select * from v$logmnr_contents; --归档日志分析的DML DDL结果信息
select * from v$logmnr_dictionary; --日志分析的字典文件信息
select * from v$logmnr_logs; --日志分析的日志列表信息
select * from v$tablespace; --表空间信息
select * from v$tempfile; --临时文件信息
select * from v$filestat; --数据文件的I/O统计信息
select * from v$undostat; --Undo数据信息
select * from v$rollname; --在线回滚段信息
select * from v$session; --会话信息
select * from v$transaction; --事务信息
select * from v$rollstat; --回滚段统计信息
select * from v$pwfile_users; --特权用户信息
select * from v$sqlarea; --当前查询过的sql语句访问过的资源及相关的信息
select * from v$sql; --与v$sqlarea基本相同的相关信息
select * from v$sysstat; --数据库系统状态信息

-- 比较常用的SESSION开头的视图有
select * from session_roles; --会话的角色信息
select * from session_privs; --会话的权限信息

-- 比较常用的INDEX开头的视图有
select * from index_stats; --索引的设置和存储信息

-- 伪表，参考oracle 中 dual 详解：http://blog.csdn.net/ozhouhui/article/details/7935196
select * from dual; --系统伪列表信息
select sysdate from dual; --可将Sysdate视为一个其结果为当前日期和时间的函数，在任何可以使用Oracle函数的地方都可以使用Sysdate。也可以将它视为每个表的一个隐藏的列或伪列。
select current_date from dual; --报告会话的时区中的系统日期。注：可以设置自己的时区，以区别于数据库的时区。
select SYSTIMESTAMP from dual; --报告TIMESTAMP数据类型格式的系统日期。


-- 系统权限
-- GRANTEE 接受该权限的用户名 
-- OWNER 对象的拥有者 
-- GRANTOR 赋予权限的用户
SELECT * FROM dba_sys_privs WHERE grantee = 'SYS';
SELECT * FROM dba_sys_privs WHERE grantee = 'CONNECT';
SELECT * FROM dba_sys_privs WHERE grantee = 'RESOURCE';

-- 角色权限
-- 查看某个用户有哪些角色
select * from dba_role_privs where grantee='SYS';
-- 查看某个角色被赋予了哪些用户
SELECT * FROM dba_role_privs WHERE granted_role = 'DBA';

-- 对象权限
SELECT * FROM dba_tab_privs;

-- 授予某个用户某些角色
GRANT connect,resource TO 'USER';
GRANT dba to 'USER'; --给普通用户授予dba角色时，要重新连接才能生效
REVOKE dba to 'USER';
-- 直接授予某个用户某些权限
GRANT CREATE VIEW TO 'USER';

-- 查看某个系统用户是否有SYSDBA或者SYSOPER权限
-- oracle:DBA,SYSDBA,SYSOPER三者的区别：http://blog.chinaunix.net/uid-22457844-id-3045741.html
select * from V$PWFILE_USERS;

-- 锁定、解锁用户
SELECT * FROM dba_users WHERE username = 'SCOTT';
ALTER USER SCOTT account LOCK; --锁定用户
ALTER USER SCOTT account UNLOCK; --解锁用户
COMMIT;

-- oracle10g 修改用户密码: http://blog.163.com/benbenfafa_88/blog/static/64930162200972594612972/
-- User Default Password Check in Oracle 11g: http://www.dbform.com/html/2009/673.html
SELECT password FROM dba_users WHERE username = 'SCOTT';
alter user SCOTT identified by new_password; --修改用户密码


-- SERVICE_NAMES: http://docs.oracle.com/database/121/REFRN/GUID-AC956707-D568-4F8A-BF2E-99BA41E0A64F.htm#REFRN10194
SELECT * FROM global_name; -- 查看oracle的全局数据库名
SELECT * FROM v$database; -- 查看数据库名 show parameter db_name;

-- 数据库实例名对应着SID
-- SID: http://docs.oracle.com/database/121/LADBI/glossary.htm#LADBI8021
-- linux下在配置oracle环境变量的情况可以使用 echo $ORACLE_SID,如果没有可以使用ps -ef |grep oracle 来查询，结果中的xxxx就是对应的SID。
-- oracle    2548     1  0 Aug17 ?        00:00:00 ora_pmon_xxxx
-- 在windows环境下,oracle是以后台服务的方式被管理的,所以看"控制面板->管理工具->服务 里面的名称:"OracleServiceORCL",则ORCL就是sid;
SELECT * FROM v$instance; --查看数据库实例名 show parameter instance_name;
select instance from v$thread;

-- show parameter是oracle的命令，不是标准SQL语句
-- 可以在sqlplus或者pl/sql dev的命令窗口执行
-- show parameter aaaa;等价于SELECT * FROM v$parameter WHERE name like '%aaaa%';
SELECT * FROM v$parameter WHERE name like '%name%'; --等价于show parameter name;
select * from v$parameter where name like '%db_domain%'; --查询数据库域名


select username from all_users where username like '%SCOTT%';
drop user SCOTT cascade;
commit;

-- ERROR at line 1:
-- ORA-01940: cannot drop a user that is currently connected

select 'ALTER SYSTEM KILL SESSION '||''''||SID||','||SERIAL#||''''||';' as KILLER from v$session where username='SCOTT';
-- KILLER
-- ALTER SYSTEM KILL SESSION '363,35';
-- ALTER SYSTEM KILL SESSION '364,51';
commit;

select * from dba_roles where role like '%CONNECT%';
drop role CONNECT;
commit;

select * from dba_tablespaces where tablespace_name like 'EXAMPLE';
drop tablespace EXAMPLE including contents and datafiles cascade constraints ;
-- including contents 删除表空间中的内容，如果删除表空间之前表空间中有内容，而未加此参数，表空间删不掉，所以习惯性的加此参数。
-- including datafiles 删除表空间中的数据文件。
-- cascade constraints 同时删除 tablespace 中表的外键参照。


-- 如何创建dblink和视图
-- http://docs.oracle.com/database/121/SQLRF/statements_5006.htm#i2061505
-- 如果需要创建全局 DBLink，则需要先确定用户有创建 dblink 的权限：
select * from user_sys_privs where privilege like upper('%DATABASE LINK%');

-- 如果没有，则需要使用 sysdba 角色给用户赋权：
grant create public database link to dbusername;

-- 如果创建全局 dblink，必须使用 systm 或 sys 用户，在 database 前加 public。
create /* public */ database link dblink1
connect to dbusername identified by dbpassword
using '(DESCRIPTION =(ADDRESS_LIST =(ADDRESS =(PROTOCOL = TCP)(HOST = 192.168.0.1)(PORT = 1521)))(CONNECT_DATA =(SERVICE_NAME = orcl)))';

-- 创建dblink后，就可以直接在dblink上创建视图
create or replace view cptp as (select SJDH from dbusername.cptp@dblink1); drop view cptp;


-- 锁表查询SQL
SELECT object_name, machine, s.sid, s.serial#
FROM gv$locked_object l, dba_objects o, gv$session s
WHERE l.object_id　= o.object_id
AND l.session_id = s.sid;

-- 解除锁表
alter system kill session 'sid, serial#';


-- 备份某个表
create table new_table as select * from old_table;


-- 查看数据库是否在rac环境的集群中的
show parameter cluster_database;
select * from v$parameter where name = 'cluster_database';


-- 列操作
-- 增加和修改列不需要加关键字COLUMN
-- 删除单列的话，一定要加COLUMN，删除多列的时候，不能加COLUMN关键字

-- 增加一列
alter table emp4 add test varchar2(10);
-- 修改一列
alter table emp4 modify test varchar2(20);
-- 删除一列
alter table emp4 drop column test;
-- 增加多列
alter table emp4 add (test varchar2(10),test2 number);
-- 修改多列
alter table emp4 modify (test varchar2(20),test2 varchar2(20));
-- 删除多列
alter table emp4 drop (test,test2);


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


UPDATE STAFF
SET MODIFY_TIME = TO_DATE('2016/04/22 00:01:00', 'yyyy/MM/dd hh24:mi:ss')
WHERE MODIFY_TIME < TO_DATE('2016/04/22 00:01:00', 'yyyy/MM/dd hh24:mi:ss');

UPDATE STAFF
SET MODIFY_TIME = TO_TIMESTAMP('19-03-2008 02:36:00.360000', 'dd-MM-yyyy hh24:mi:ss.ff')
WHERE STAFF_ID = '01';

```