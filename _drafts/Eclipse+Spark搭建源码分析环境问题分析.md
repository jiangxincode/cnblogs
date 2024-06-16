欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju


# Scala IDE complains about ‘... is cross-compiled with an incompatible version of Scala ...’

* http://scala-ide.org/docs/current-user-doc/faq/index.html


# "Cannot run program "bash" ...: CreateProcess error=2"

[ERROR] Failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.8:run (default) on project spark-core_2.11: An Ant BuildException has occured: Execute failed: java.io.IOException: Cannot run program "bash" (in directory "D:\temp\Scala\spark\core"): CreateProcess error=2, 系统找不到指定的文件。

* http://blog.csdn.net/xubo245/article/details/52073805


# "Failed to execute goal org.apache.maven.plugins:maven-clean-plugin:3.0.0:clean..."

[ERROR] Failed to execute goal org.apache.maven.plugins:maven-clean-plugin:3.0.0:clean (default-clean) on project spark-parent_2.10: Failed to clean project: Failed to delete /usr/spark/spark-2.1.0/target/tmp -> [Help 1]

* http://www.cnblogs.com/o-din/p/6292153.html


# "Could not transfer artifact ... from/to central ...: GET request of: ... from central failed: Tag mismatch!"

[ERROR] Failed to execute goal on project spark-sql_2.11: Could not resolve dependencies for project org.apache.spark:spark-sql_2.11:jar:2.2.0-SNAPSHOT: Could not transfer artifact it.unimi.dsi:fastutil:jar:6.5.7 from/to central (https://repo1.maven.org/maven2): GET request of: it/unimi/dsi/fastutil/6.5.7/fastutil-6.5.7.jar from central failed: Tag mismatch! -> [Help 1]

删除fastutil-6.5.7.jar重新下载