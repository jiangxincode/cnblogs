```sql
-- 全量导出
exp system/manager@TEST file=d:\daochu.dmp full=y

-- 将数据库中system用户与sys用户的表导出
exp system/manager@TEST file=d:\daochu.dmp owner=(system,sys)

-- 将数据库中的表table1中的字段filed1以"00"打头的数据导出
exp system/manager@TEST file=d:\daochu.dmp tables=(table1) query=\" where filed1 like '00%'\"

-- 将数据库中的表table1/table2导出
exp system/manager@TEST file=d:\daochu.dmp tables=(table1,table2)


-- 将d:\daochu.dmp中的表table1/table2导入
-- 如果在Linux下导入导出，需要使用 tables="(table1,table2)"，否则报错"syntax error near unexpected token("
imp system/manager@TEST file=d:\daochu.dmp tables=(table1,table2)
```