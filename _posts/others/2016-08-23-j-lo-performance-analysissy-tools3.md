---
title: "Java 性能分析工具，第 3 部分：Java Mission Control"
categories:
  - others
tags:
  - Android
  - Gradle
  - Gradle Wrapper
  - Android Plugin for Gradle
toc: true
---

使用在 Java 7u40 之后加入的性能监控新功能 Java Mission Control 来对 Java 应用程序进行分析

## 引言

本文为 Java 性能分析工具系列文章第三篇，这里将介绍如何使用 Java 任务控制器 Java Mission Control 深入分析 Java 应用程序的性能，为程序开发人员在使用 Java 任务控制器的时候提供帮助。 [第一篇：操作系统工具](https://www.ibm.com/developerworks/cn/java/j-lo-performance-analysissy-tools/index.html) ， [第二篇：Java 内置监控工具](https://www.ibm.com/developerworks/cn/java/j-lo-performance-analysissy-tools2/index.html) 。

JMC 是在 JAVA 7u40 发布中加入的性能监控工具。使用过 JDK 6 中 JRockit JVM 的用户并不会陌生，因为它是 Java 7 中 JMC 功能的一部分。启动 JMC 后将会显示当前机器中的所运行的 JVM 进程信息，当然我们也可以选择添加更多的 JVM 进程进行监控。图 1 中展示了使用 JMC 监控 GlassFish 应用服务器的画面。图中展示了被监控程序的基本信息，其包括 CPU 使用率和内存堆的使用率，值得注意的是，JMC 监控图中显示的是当前机器的 CPU 的使用情况，可以看到的是 JMC 监控的是整个系统，而并非只是被选中的 JVM 对 CPU 的使用情况。通过自定义设置上方仪表盘中显示的信息，既可以查看 被监控 JVM 的详细信息，例如垃圾回收，类的加载，线程的使用，以及内存堆的使用率，等等。也可以查看指定操作系统信息，例如系统的 CPU 和内存的使用率，磁盘的交换信息，平均负载等相关信息。

##### 图 1\. Java Mission Control 监控图

![图 1. Java Mission Control 监控图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img001.png)

## JFR (Java Flight Recorder)

JFR 是 JMC 中一个非常关键的功能。它记录了 JVM 所有事件的历史数据，通过这些数据，程序性能分析人员可以结合以往的历史数据对 JVM 性能瓶颈进行分析诊断。

JFR 的基本操作是开启一系列的事件（例如，一个线程为了等待锁而被阻塞）。当某个事件发生时，这个事件的所有数据将会被保存至内存或者一个文件当中。数据流被保留在一个环形缓存中，所以只有最近发生的事件的数据才是可用的。JMC 可以从 JVM 或者文件中读取并展示这些事件数据，通过这些数据，可以进行性能分析。

通过 JVM 参数，JMC 用户界面以 jcmd 命令，可以指定上文中提到的事件类型、环形缓存的大小、数据存储的位置等信息。在默认设置下，JMC 对被监控应用的影响非常小。但是随着越来越多的事件被开启，以及触发事件的阀值的改变，JMC 的影响也在变化。接下来将展示 JFR 的用户界面。

### JFR 概述

这个例子使用 JFR 记录 GlassFish 应用服务器的 6 分钟内的相关数据。图 2 展示了 JMC 将这些数据加载之后的到总体视图。

##### 图 2\. JMC 数据加载示例图

![图 2. JMC 数据加载示例图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img002.png)

这张图上的信息类似于 JMC 基本信息监控所看到的画面。上面的仪表盘显示的是 CPU 使用率和内存堆使用率，在其上方有一条标示事件顺序的时间轴，垂直柱状体代表事件。可以放大时间轴中感兴趣的部分进行详细分析，就像图中所示，从 6 分钟的时间轴选出位于末端的 1 分 6 秒进行放大。

图 2 中 CPU 使用率曲线非常清楚的看到，GlassFish 服务器所在 JVM 平均大约 70%的使用率，而机器整体的 CPU 使用率达到 100%。在最下端，有一些标签可以选择，系统属性标签，JVM 信息标签等，在画面左侧的按钮提供更加详细的应用程序运行状况。

### JFR 内存视图

JFR 内存视图收集的信息非常丰富，下图只展示了其中的一部分。从图 3 中可以看出，新生代（Young Generation) 占用的内存大小在周期性地进行有规律的波动。但有趣的是，由于没有对象需要移入老年代，应用整体的内存堆大小并没有增长。左下角面板中展示在监控期间所有类型的垃圾回收事件，在本例中一直为 ParallelScavenge。当选中一个事件时，右下角将更加细化的显示此事件，包括此事件的所有阶段以及每个阶段的时间消耗。

##### 图 3\. 新生代内存使用情况示例图

![图 3. 新生代内存使用情况示例图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img003.png)

从图中各种各样的标签可以看到包含了丰富的信息，其中包括引用对象被清理的时间和数量，并发回收器中是否有 Promotion 失败或者 Evacuation 失败，垃圾回收器自身算法的配置，等等信息。

### JFR 代码视图

JFR 代码视图展示了从记录的数据中获得的基础分析信息。如图 4 所示，第一个标签页显示了所有的包名，在其他分析工具我们并没见过类似的功能。可以看出图中使用 Java.Math 方法的执行占应用程序所有方法调用运行总时长的比重为 41%。传统的分析视角位于底部，例如热点方法和被分析代码的调用如下图所示。

##### 图 4\. Java Flight Recorder 代码视图

![图 4. Java Flight Recorder 代码视图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img004.png)

与其它分析软件不同，JFR 提供更多模式的代码可视化。Throwables 标签页展示应用中的异常处理，还有展示编译器工作信息的标签页。

JMC 还提供线程视图，I/O 视图，系统视图，所有的这些视图都是为了更好的分析 JFR 所记录的真实事件。

### JFR 事件概述

JFR 记录并保存事件流，JMC 提供不同的视图来分析这些事件，但是 JFR 事件面板（如图 5 所示）才是分析事件最有效的途径。

##### 图 5\. Java Flight Recorder 事件视图

![图 5. Java Flight Recorder 事件视图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img005.png)

通过左侧面板的过滤器可以过滤显示的事件，在图中，只选择了应用级的事件。需要注意的是，只有在 JFR 记录保存事件中指定的事件类型才会出现在这里，在这里只能在此基础上进行过滤。

从图 5 中可以看出，在 66 秒内，应用程序产生 6 种类型的事件，其中 10612 个 JVM 事件和 1536 个 JDK 库事件。线程 Park 和 Monitor 事件消耗时间长的原因在前文中已有讨论，在此不再赘述。应用程序有多个线程共消耗 40 秒向套接字内写数据（Socket Write），这对于一个使用 4 核的应用来说是一个正常值，但仍然可以通过减少向套接字内写入的数据量来提高性能。

同样的，应用程序中多个线程共消耗 143 秒从套接字读取数据 (Socket Read)。这看起来并不正常，通过查看这些事件的处理记录可以发现，由多个线程使用阻塞式 I/O 读取并不连续的管理请求。这些管理请求的时间间隔通常很长，但这些线程却在 read() 方法内被阻塞，所以导致这些线程读取数据时消耗了过多的时间。

对于 Monitor 事件，

准性能分析器可以提供线程被阻塞之后调用 CPU 和操作系统代码等待解锁的相关信息，而 Java 本地分析器能够提供这些 CPU 和操作系统代码执行的记录，正如 JVM 直接将这些信息提供给 JFR。

JFR 事件是直接获得于 JVM 之内，通过这些事件能够非常详细的了解应用程序内部的运行状况，这是其他工具所不能比的。事件的类型非常之多，在不同版本的 JDK 之间也有所差异。下面列出一些常用的事件类型，第一行描述可以由其他工具获得的信息，第二行描述除了使用 JFR 无法获得信息。

- Classloading

    被加载的类的数量和未被加载的类的数量

    加载类的类加载器（classloader），加载一个类需要的时间

- Thread statistics

    创建线程的数量、销毁线程的数量、线程快照（dump）

    阻塞指定线程的锁以及被指定锁阻塞的线程

- Throwables

    应用程序实用的异常类

    应用程序抛出的异常和错误的数量以及创建异常和错误的栈记录

- TLAB allocation

    内存堆中已分配的数量、TLAB（Thread-Local Allocation Buffers）的大小

    在内存对中指定对象的内存分配以及为这些对象分配内存的栈记录

- File and socket I/O

    进行 I/O 消耗的时间

    每一次读写调用的时间消耗，读写操作消耗时间过长的文件或套接字

- Monitor blocked

    等待监控器的线程

    阻塞某个线程的监控器、线程被阻塞的时间

- Code cache

    代码缓存的大小以及内容

    从代码缓存中移除的方法、代码缓存的配置

- Code compilation

    哪些方法被编译，OSR 编译，编译耗时

    JFR 中没有额外的信息，但 JFR 总结了多个源文件的信息

- Garbage collection

    GC 的次数，包括每一个阶段的次数、每个代的大小

    JFR 中没有额外的信息，但 JFR 总结了来自多个工具的信息

- Profiling

    检测分析和采样分析

    JFR 并不能获得分析器获得的丰富信息，但 JFR 提供了更高层次的概述


## 开启 JFR

Java Flight Recorder – JFR 默认被设置为关闭状态。通过在启动应用程序的命令中加入-XX:+UnlockCommercialFeatures –XX:+FlightRecorder 参数来开启 JFR，以及相关的一些功能。但是值得注意的是这个命令只是开启了 JFR 功能，但并没有开启记录进程各种事件，这就需要我们在开启了 JFR 功能之后，必须通过用户界面或者命令行来开启记录运行线程产生记录的功能。

### 通过 JMC 开启 JFR

最简单的方式是通过 JMC 来开启 JFR，当 JMC 启动后，界面上将显示当前系统中所有的 JVM 进程。JVM 进程以树形结构展示，展开 JVM 进程节点，通过 Flight Recorder 按钮开启 Flight Recorder 窗口，如图 6 所示。

##### 图 6\. Java Flight Recorder 记录窗口视图

![图 6. Java Flight Recorder 记录窗口视图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img006.png)

Flight Recorder 有两种模式，固定时长模式（图中为 1 分钟）和持续模式，在持续模式中，使用环形缓存保存最近的事件。

在进行前瞻性分析（Proactive Analysis）时，例如在进行负载测试时开始记录事件，应该使用固定时长模式，这样可以很好的了解 JVM 在负责测试期间的表现。

持续模式适合反应（Reactive）分析，这样可以使 JVM 保存最近的事件并导出记录响应这些事件的数据。举例来说，Weblogic 应用服务中可以设置触发器，在应用服务器响应了一个反常事件之后导出相关数据。

### 通过命令行开启 JFR

在 JVM 启动参数中加入-XX:+FlightRecorderOption=参数启动记录事件。参数为一个以逗号间隔的键值对数据。下面将介绍这些选项：

- name=name

    指定记录的名称

- defaultrecording=true/false

    是否在初始化时启动记录事件，默认为 false，对于反应分析，应设置为 true

- settings=path

    JFR 配置文件的路径

- delay=time

    开始记录前的延时

- duration=time

    记录持续时间

- filename=path

    保存记录事件的文件路径

- compress=true/false

    是否使用 gzip 压缩记录数据，默认为 false

- maxage=time

    环形缓存中保存记录的数据的最长时间

- maxsize=size

    环形缓存占用的最大空间


为了更灵活的使用 JFR，在运行过程中可以使用 jcmd 命令来动态改变这些选项的值。下面将介绍使用 jcmd 来设置 JFR 相关选项的命令。

```
% jcmd process_id JFR.start [option_list]

```

Show moreShow more icon

option\_list 是以逗号分隔的键值对，选项与上述选项一致。当使用持续模式记录事件时，可以使用下面的命令将环形缓存中的数据导出至文件中：

```
% jcm process_id JFR.dump [option_list]

```

Show moreShow more icon

选项包括：

- name=name

    指定导出数据的事件记录名

- recording=n

    JFR 事件记录号

- filename=path

    导出文件的路径


一个进程下可能有多个 JFR 事件记录在运行，可以通过下面的命令查看当前所有的事件记录：

```
% jcmd process_id JFR.check [verbose]

```

Show moreShow more icon

这些不同的事件记录以名字或者随机的记录号进行区分。使用下面的命令可以停止一个进程内正在运行的事件记录：

```
% jcmd process_id JFR.stop [option_list]

```

Show moreShow more icon

选项包括：

- name=name

    需要停止的事件记录名

- recording=n

    需要停止的事件记录号

- discard=Boolean

    如果为 true，舍弃之前保存的数据

- filename=path

    保存数据的文件路径


## 选择 JFR 事件

JFR 目前支持 77 种事件类型，大多数类型的事件为周期性事件，每隔固定时间将会产生一次，其他类型的事件为触发型，只有当达到某种设定的阀值后被触发，也就是说才会被 JFR 发现并监控起来。

收集事件数据自然会影响应用程序性能，影响的大小由开启记录的事件的类型和数量有关。默认情况下，并没有开启所有事件类型的记录，将对性能影响较大的 6 种类型事件关闭，以此达到将 JFR 对应用程的影响降到 1%以内。

但有时开启一些对应用影响较大的事件类型是值得的，例如 TLAB 是默认关闭的事件类型，但是它能够帮助人们发现某些对象是否在分配内存时直接进入老年代（Old Generation）。同样的，Profiling 事件虽然默认开启，但是每 20 毫秒触发一次，这样很容以导致采样分析出现错误。

JFR 记录的事件定义在一个模版中，可以通过 settings 选项指定。JFR 运行时有两个模版：

1. 默认模版：事件对应用性能的影响在 1%以内
2. 分析模版：设置大部分基于阀值（Threshhold）的事件为 10 毫秒触发一次，分析模版对应用性能的影响大约为 2%。

这些模版由 JMC 模版管理器（Template Manager）管理，模版管理器通过 JMC 中相应的按钮启动。存储模版的目录有两个：$HOME/.JMC/directory 和$JAVA\_HOME/jre/lib/jfr。在模版管理器中，可以选择一个全局模版、本地模版或者定义一个新模版。定义一个新模版是时，需要指定可用的事件，指定这些事件默认的状态为开启或者关闭，同时可以定义这些事件的阀值。

在图 7 中，File Read 事件被开启并且设置阀值为 15 毫秒，即当读取文件超过 15 毫秒时，此事件将触发。同时此事件还被设置为 File Read 事件生成栈记录，由于这将增加事件对应用性能的影响，所以将此选项设置为可选配置项。

##### 图 7\. Java Flight Recorder 事件模板示例图

![图 7. Java Flight Recorder 事件模板示例图](https://raw.githubusercontent.com/jiangxincode/PicGo/master/j-lo-performance-analysissy-tools3_images_img007.png)

事件模版文件为 xml 文件，所以通过读取 xml 文件很容易可以判断某个事件是否开启。也可以将本地模版文件拷贝至全局模版目录供其他用户和团队使用。

Java Flight Recorder（JFR）提供了深入 JVM 内部去看运行时的状态。这是由于 JFR 其本身就是 Java 的一部分内嵌其中的。如同其他工具，JFR 的使用某种程度上增加了对应用程序性能的开销。常规的使用 JFR 还是可以帮助我们收集大量的信息，而且对性能的开销是较低的。

## 结束语

到此为止，本系列文章已经将常用的 Java 性能分析工具进行了介绍，我们都知道一个优秀的性能分析工具是我们在分析性能问题的关键，但是不能完全，甚至过分的依赖工具所能展现的表面，我们更应当铭记，没有最好的工具，只有是否适合的工具，正如我们讲过的工具 A 也许适合大多数的应用程序分析，但是它却不能够揭示工具 B 所能指出的问题，所以我们应当学会灵活自由的使用这些工具。

对于性能分析人员来说命令行工具也是非常有帮助，所以不要拒绝它所能带来的强大力量。它往往能在自动化的性能监控，或者性能测试中发挥巨大作用。

希望这些介绍能够给性能调优人员和开发人员的日常工作带来帮助。俗话说金无足赤，人无完人，工具亦如此。每一个工具都有其各自的优劣势，只有充分了解每个工具适合的场景，才能让这些工具扬长避短，更加充分地发挥其作用。

[原文链接](https://developer.ibm.com/zh/articles/j-lo-performance-analysissy-tools3/)

李伟军, 宋翰瀛, 杨翔宇

发布: 2016-08-23