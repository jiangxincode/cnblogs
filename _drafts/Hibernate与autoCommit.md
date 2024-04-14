# JDBC 的`autoCommit`属性

对于每一个 JDBC connection，都有一个autoCommit属性，只有执行commit后，该connection中的操作（statement操作）才会在数据库中真正执行。所以若是 JDBC connection的autoCommit属性是false，且sql语句中没有显示commit，则sql语句即使被发送到数据库中，但因为没有commit，实际上也没有真正执行。若是connection的autoCommit为true，那么每一条发送到数据中的sql，会自动commit，即会自动执行。也就是说：commit才会真正的导致sql语句执行。数据库默认是自动提交的，即数据库默认的的autoCommit属性是true。

# Hibernate 的`hibernate.connection.autocommit`属性

Hibernate中hibernate.connection.autocommit属性用来设置获取到的 JDBC connection的autoCommit属性。hibernate.cfg.xml中默认是false。session.connection().getAutoCommit()方法可以获取session对应的connection的autoCommit属性。

# Hibernate 的`session.beginTransaction()`方法

session.beginTransaction()方法会将session对应的connection的autoCommit属性设为false，autoCommit=false（相当于connection 的start transaction）就是指开启jdbc的事务。所以session.beginTransaction()后一定要有：transaction.commit()，不然刷到数据库中的所有sql执行语句都没有commit，也就不会执行。

# Hibernate 的`session.flush()`方法

清理session缓存；先由save()等代码中指定的操作生成对应的sql语句，可能有多条sql语句，再将session中的sql语句发送到数据库执行。若是在生成sql语句时抛错，即使生成其它sql语句时正确，也不会生成任何sql语句，也即不会有任何的sql发送到数据库中去执行。transaction.commit()和session.close()操作都已经有flush()的操作，所以commit或close后就不用flush。


# 参考文章

* https://forum.hibernate.org/viewtopic.php?f=1&t=944848