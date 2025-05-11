
## oracle 临时表空间和数据表空间

Oracle临时表空间主要用来做查询和存放一些缓冲区数据。临时表空间消耗的主要原因是需要对查询的中间结果进行排序。重启数据库可以释放临时表空间，如果不能重启实例，而一直保持问题sql语句的执行，temp表空间会一直增长。直到耗尽硬盘空间。网上有人猜测在磁盘空间的分配上，oracle使用的是贪心算法，如果上次磁盘空间消耗达到1GB，那么临时表空间就是1GB。也就是说当前临时表空间文件的大小是历史上使用临时表空间最大的大小。临时表空间的主要作用：

* 索引create或rebuild
* Order by 或 group by
* Distinct 操作
* Union 或 intersect 或 minus
* Sort-merge joins
* analyze

数据表空间：表空间的作用能帮助DBA用户完成以下工作:

* 决定数据库实体的空间分配;
* 设置数据库用户的空间份额;
* 控制数据库部分数据的可用性;
* 分布数据于不同的设备之间以改善性能;
* 备份和恢复数据。

用户创建其数据库实体时其必须于给定的表空间中具有相应的权力,所以对一个用户来说,其要操纵一个ORACLE数据库中的数据,应该:

* 被授予关于一个或多个表空间中的RESOURCE特权;
* 被指定缺省表空间;
* 被分配指定表空间的存储空间使用份额;
* 被指定缺省临时段表空间。

表空间的维护是由ORACLE数据库系统管理员DBA通过SQL*PLUS语句实现的,其中表空间创建与修改中的文件名是不能带路径的,因此DBA必须在ORACLE/DBS目录中操作。


```
-- 表空间相关问题

--创建永久表空间
create tablespace tablespace_name
datafile 'PATH_OF_NEW_DATAFILE'
size 50M
AUTOEXTEND ON NEXT 50M;

--删除表空间
DROP TABLESPACE TABLESPACE_NAME;

-- 表空间不足的一般报错信息为：
-- sqlexception:ora-01654: unable to extend index index_name by 1024 in tablespace tablespace_name

-- 表空间是逻辑概念，数据文件和临时数据文件都是物理感念。
-- 一个表空间可以有多个数据文件或者临时数据文件。
SELECT * FROM dba_tablespaces;
SELECT * FROM dba_data_files;

-- 该表中只有数据文件的使用率，不包含临时数据文件
SELECT * FROM dba_free_space;

-- dba_data_files表中同一个tablespace_name可能会有多个数据文件
-- 使用sum聚集函数，并且添加group by子句可以统计相同的tablesapce_name的多个数据文件的总大小
select t.tablespace_name, round(sum(d.bytes/(1024*1024)),0) "tablespace_size(M)"
from dba_tablespaces t, dba_data_files d
where t.tablespace_name = d.tablespace_name
group by t.tablespace_name;

select sum(bytes)/(1024*1024) as free_space,tablespace_name 
from dba_free_space
group by tablespace_name;

-- 查询数据文件实际使用情况（不包含临时数据文件，执行速度比较慢）
select file_name, sum(e.bytes)/1024/1024 as mb   
from dba_extents e join dba_data_files f on e.file_id=f.file_id   
group by file_name;


-- 为某个表空间添加数据文件，文件路径格式参考dba_data_files表中的格式
alter tablespace tablespace_name add datafile 'PATH_OF_NEW_DATAFILE' size 10m 
autoextend ON next 5m maxsize 100m;

-- 修改已有的数据文件自动增长
alter database datafile 'PATH_OF_OLD_DATAFILE'
autoextend on next 5m maxsize 100m;

-- 重新设置已有的数据文件大小，如果是缩小的话不能小于数据文件的实际使用情况
alter database datafile 'PATH_OF_OLD_DATAFILE'
resize 100m;


-- 如何解决临时表空间不足

SELECT * FROM dba_temp_files;

-- 查询临时表空间的使用情况，D.TABLESPACE_NAME = F.TABLESPACE_NAME(+)代表左联接
SELECT D.TABLESPACE_NAME,SPACE "SUM_SPACE(M)",BLOCKS SUM_BLOCKS, 
USED_SPACE "USED_SPACE(M)",ROUND(NVL(USED_SPACE,0)/SPACE*100,2) "USED_RATE(%)",
NVL(FREE_SPACE,0) "FREE_SPACE(M)"
FROM 
(SELECT TABLESPACE_NAME,ROUND(SUM(BYTES)/(1024*1024),2) SPACE,SUM(BLOCKS) BLOCKS
FROM DBA_TEMP_FILES
GROUP BY TABLESPACE_NAME) D,
(SELECT TABLESPACE_NAME,ROUND(SUM(BYTES_USED)/(1024*1024),2) USED_SPACE,
ROUND(SUM(BYTES_FREE)/(1024*1024),2) FREE_SPACE
FROM V$TEMP_SPACE_HEADER
GROUP BY TABLESPACE_NAME) F
WHERE  D.TABLESPACE_NAME = F.TABLESPACE_NAME(+);

-- 建立一个中转临时表空间：
create temporary tablespace temp2
tempfile 'PATH_OF_NEW_TEMPFILE' size 512M
reuse autoextend on next 100M maxsize 2048M;
alter database default temporary tablespace temp2;
drop tablespace temp including contents and datafiles;

create temporary tablespace temp
tempfile 'PATH_OF_NEW_TEMPFILE' size 512M
reuse autoextend on next 100M maxsize 1024M;
alter database default temporary tablespace temp;
drop tablespace temp2 including contents and datafiles;


-- 查看分配给某个表的空间，不管实际是否使用
SELECT TABLESPACE_NAME,TO_CHAR(SUM(BYTES)/(1024*1024),'999G999D999') CNT_MB   
FROM DBA_EXTENTS
WHERE OWNER='SCOTT' AND SEGMENT_NAME='BONUS' AND SEGMENT_TYPE LIKE '%TABLE%'   
GROUP BY TABLESPACE_NAME;

-- 实际使用的空间
analyze table SCOTT.BONUS compute statistics;
select num_rows * avg_row_len 
from dba_tables 
where owner = 'SCOTT' and table_name = 'BONUS';


-- 数据文件，表空间与状态对应关系
SELECT FILE_NAME, TABLESPACE_NAME, ONLINE_STATUS FROM DBA_DATA_FILES;

-- 用户与表空间对应关系
SELECT USERNAME, DEFAULT_TABLESPACE FROM DBA_USERS;

```