使用Android Studio经常会在Event Log窗口遇到如下报错：
```
21:42	Android Studio is using the following JDK location when running Gradle:
			C:\Program Files\Android\Android Studio\jre
			Using different JDK locations on different processes might cause Gradle to
			spawn multiple daemons, for example, by executing Gradle tasks from a terminal
			while using Android Studio.
			More info...
			Select a JDK from the File System
			Do not show this warning again
```
可以通过如下指引了解详细信息：

<https://docs.gradle.org/current/userguide/gradle_daemon.html#sec:why_is_there_more_than_one_daemon_process_on_my_machine>

简单解释下就是如果后台有一个常驻的gradle守护进程，可以提高我们构建效率。因为这样不但可以避免每次都重新启动JVM，并且可以缓存项目结构、文件、任务等信息。每次启动AS的时候，你可能会注意到如下这个提示，其实就是AS默认打开了gradle守护进程：

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200805222550660-189587292.png)

但是如果使用守护进程特性会有一个问题，就是可能会出现多个守护进程的场景，这是因为守护进程可能在某些方面无法满足请求构建环境。比如如果守护进程运行在Java 8运行时，但是请求的环境调用Java 10，那么守护进程是不兼容的，必须启动另一个。此外，Java运行时的某些属性在JVM启动后无法更改。这也可能导致出现多个守护进程。

为了避免出现这种情况，一个最好的解决方式时我们每次使用gradle进行项目构建时，尽量使用相同的JDK配置。如果我们在命令行中使用gradle，会自动使用JAVA_HOME环境变量指向的JDK，如果在AS中使用gradle，使用的是如下指向的JDK
![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200805221541606-1552863309.png)

所以为了两者一致，我们需要将此处的JDK改为JAVA_HOME环境变量指向的JDK。修改完之后AS的告警提示信息也自然消失了。
![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200805230821788-1845237150.png)

另外注意下从Gradle 6.3版本才开始正式支持JDK 14: <https://docs.gradle.org/6.3/release-notes.html>
