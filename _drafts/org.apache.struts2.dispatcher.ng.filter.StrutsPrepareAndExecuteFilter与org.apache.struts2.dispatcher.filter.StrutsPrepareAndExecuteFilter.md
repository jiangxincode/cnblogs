欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

使用Eclipse启动Maven+Struts项目报错，报错日志如下：

```
2016-08-31 22:00:47  INFO ContextLoader:325 - Root WebApplicationContext: initialization completed in 2675 ms
八月 31, 2016 10:00:47 下午 org.apache.catalina.core.StandardContext filterStart
严重: Exception starting filter struts2
java.lang.ClassNotFoundException: org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1295)
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1147)
	at org.apache.catalina.core.DefaultInstanceManager.loadClass(DefaultInstanceManager.java:520)
	at org.apache.catalina.core.DefaultInstanceManager.loadClassMaybePrivileged(DefaultInstanceManager.java:501)
	at org.apache.catalina.core.DefaultInstanceManager.newInstance(DefaultInstanceManager.java:120)
	at org.apache.catalina.core.ApplicationFilterConfig.getFilter(ApplicationFilterConfig.java:258)
	at org.apache.catalina.core.ApplicationFilterConfig.<init>(ApplicationFilterConfig.java:105)
	at org.apache.catalina.core.StandardContext.filterStart(StandardContext.java:4615)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5222)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1409)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1399)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
```

很明显是类没有找到，找到web.xml中的配置如下：

```
<filter>
    <filter-name>struts2</filter-name>
    <filter-class>
        org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter
    </filter-class>
</filter>
<filter-mapping>
    <filter-name>struts2</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

使用`Ctrl+Shift+T`发现，存在该类，但是包路径不对，实际包路径为：`org.apache.struts2.dispatcher.filter`。于是猜测是Struts2版本升级之后包路径换了，查看pom.xml，配置如下：

```xml
<!-- https://mvnrepository.com/artifact/org.apache.struts/struts2-core -->
<dependency>
    <groupId>org.apache.struts</groupId>
    <artifactId>struts2-core</artifactId>
    <version>2.5.1</version>
</dependency>
```

通过struts官网，可以看到从2.3到2.5部分包路径确实发生了改变。在web.xml中配置成新的包路径，重新启动，问题解决。官网说明：http://struts.apache.org/docs/version-notes-25.html。