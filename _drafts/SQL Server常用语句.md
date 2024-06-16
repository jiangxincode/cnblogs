欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

```SQL
-- 身份证验证(SQLServer)
-- 主要验证SQL数据库中已输入的15位 及18位 身份证号码的位数、出生年月日是否正确，可以过滤出大部分的输入错误。
select 身份证号
from 身份表
where (len(身份证号)<>15 and len(身份证号)<>18)
or (len(身份证号)=18 and (Substring(身份证号,7,2)<'19' or Substring(身份证号,7,2)>'20'
or (Substring(身份证号,11,2)>12)
or (Substring(身份证号,11,2) in (01,03,05,07,08,10,12) and Substring(身份证号,13,2)>31)
or (Substring(身份证号,11,2) in (04,06,09,11) and Substring(身份证号,13,2)>30)
or (Substring(身份证号,11,2)=02 and Substring(身份证号,13,2)>29)))
---------------------- 下面是针对 15位 及18位 身份证号码性别的验证语句 -------------------- Access 不支持 Substring 查询，可以替换为 mid 查询。
select 序号,姓名,身份证号,性别
from 身份表
where (((len(身份证号)=15) and (Substring(身份证号,15,1) in (1,3,5,7,9)) and 性别<>'男')
or ((len(身份证号)=15) and (Substring(身份证号,15,1) in (2,4,6,8,0)) and 性别<>'女'))
or (((len(身份证号)=18) and (Substring(身份证号,17,1) in (1,3,5,7,9)) and 性别<>'男')
or ((len(身份证号)=18) and (Substring(身份证号,17,1) in (2,4,6,8,0)) and 性别<>'女'))
----------------- 下面是针对 15位 及18位 身份证号码位数与出生年月日的验证 ------------- Access 不支持 Substring 查询，可以替换为 mid 查询
select 序号,姓名,身份证号,性别
from 身份表
where (len(身份证号)<>15 and len(身份证号)<>18)
or (len(身份证号)=15 and ((Substring(身份证号,9,2)>12)
or (Substring(身份证号,11,2) > 31)
or (Substring(身份证号,9,2) in (01,03,05,07,08,10,12) and Substring(身份证号,11,2)>31)
or (Substring(身份证号,9,2) in (04,06,09,11) and Substring(身份证号,11,2)>30)
or (Substring(身份证号,9,2)=02 and Substring(身份证号,11,2)>29)))




-- 更改列名：
exec sp_rename '表名.原列名','新列名','column';
exec sp_rename 'student.Ssex','Sex','column';



-- 成绩统计语句(SQLServer)
CREATE TABLE stuscore
(
	id int NOT NULL PRIMARY KEY identity(0000,1),
	name varchar(20),
	subject varchar(20),
	score int,
	stuid varchar(10)
  )  

insert into stuscore(name,subject,score,stuid)
select '张三', '数学', 89, '1' UNION ALL
select '张三', '语文', 80, '1' UNION ALL
select '张三', '英语', 70, '1' UNION ALL
select '李四', '数学', 90, '2' UNION ALL
select '李四', '语文', 70, '2' UNION ALL
select '李四', '英语', 80, '2' UNION ALL
select '王五', '数学', 49, '3' UNION ALL
select '王五', '语文', 87, '3' UNION ALL
select '王五', '英语', 90, '3'

--计算每个人的总成绩并排名 
select name,sum(score) as allscore
from stuscore 
group by name 
order by allscore desc

--计算每个人的总成绩并排名 
select distinct t1.name,t1.stuid,t2.allscore
from stuscore t1,(select stuid,sum(score) as allscore from stuscore group by stuid) t2
where t1.stuid=t2.stuid
order by t2.allscore desc

--计算每个人单科的最高成绩 
select t1.stuid,t1.name,t1.subject,t1.score 
from stuscore t1,(select stuid,max(score) as maxscore from stuscore group by stuid) t2
where t1.stuid=t2.stuid and t1.score=t2.maxscore 

--计算每个人的平均成绩 
select distinct t1.stuid,t1.name,t2.avgscore
from stuscore t1,(select stuid,avg(score) as avgscore
from stuscore
group by stuid) t2
where t1.stuid=t2.stuid 

--列出各门课程成绩最好的学生 
select t1.stuid,t1.name,t1.subject,t2.maxscore
from stuscore t1,(select subject,max(score) as maxscore from stuscore group by subject) t2
where t1.subject=t2.subject and t1.score=t2.maxscore

--列出各门课程成绩最好的两位学生 
select distinct t1.* 
from stuscore t1 
where t1.id in (select top 2 stuscore.id from stuscore where subject = t1.subject order by score desc) 
order by t1.subject

--学号 姓名 语文 数学 英语 总分 平均分 
select
	stuid as 学号,
	name as 姓名,
	sum(case when subject='语文' then score else 0 end) as 语文,
	sum(case when subject='数学' then score else 0 end) as 数学,
	sum(case when subject='英语' then score else 0 end) as 英语,
	sum(score) as 总分,
	(sum(score)/count(*)) as 平均分
from stuscore
group by stuid,name 
order by 总分 desc 

--列出各门课程的平均成绩 
select subject,avg(score) as avgscore 
from stuscore
group by subject 

--声明变量以便后续调用
declare @tmp table(pm int,name varchar(50),score int,stuid int)
declare @id int

--列出数学成绩的排名
insert into @tmp
select null,name,score,stuid
from stuscore
where subject='数学'
order by score desc
set @id=0
update @tmp set @id=@id+1,pm=@id
select * from @tmp
select DENSE_RANK () OVER(order by score desc) as row,name,subject,score,stuid
from stuscore
where subject='数学'
order by score desc

--列出数学成绩在2-3名的学生 
select t3.*
from
(
	select top 2 t2.* from(select top 3 name,subject,score,stuid from stuscore where subject='数学'order by score desc) t2
	order by t2.score
) t3
order by t3.score desc 

--求出李四的数学成绩的排名
insert into @tmp
select null,name,score,stuid
from stuscore where subject='数学'
order by score desc
set @id=0
update @tmp
set @id=@id+1,pm=@id
select * from @tmp where name='李四'

--课程 不及格（-59） 良（-80） 优（-100） 
select subject,
	(select count(*) from stuscore where score<60 and subject=t1.subject) as 不及格,
	(select count(*) from stuscore where score between 60 and 80 and subject=t1.subject) as 良,
	(select count(*) from stuscore where score >80 and subject=t1.subject) as 优
from stuscore t1
group by subject 

--数学:张三(50分),李四(90分),王五(90分),赵六(76分) 
declare @s varchar(1000)
set @s=''
select @s =@s+','+name+'('+convert(varchar(10),score)+'分)'
from stuscore
where subject='数学'
set @s=stuff(@s,1,1,'')
print '数学:'+@s




-- 怎样删除外键约束(SQLServer)
--测试环境
--主表
create table test1(id int primary key not null,value int)
insert test1 select 1,2
go
--从表
create table test2(id int references test1(id),value int)
go

--第一步:找出test2表上的外键约束名字
--Microsoft SQLServer 2000（及以上）
exec sp_helpconstraint 'test2'
--Microsoft SQLServer 2005（及以上）
select name
from  sys.foreign_key_columns f join sys.objects o 
on f.constraint_object_id=o.object_id 
where f.parent_object_id=object_id('test2')

--第二步：删除外键约束
alter table test2 
drop constraint FK__test2__id__08EA5793




```