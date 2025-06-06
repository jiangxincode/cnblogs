
使用Java语言编写应用程序最大的优点在于“一次编译，处处运行”，然而这并不是说所有的Java程序都具有跨平台的特性，事实上，相当一部分的Java程序是不能在别的操作系统上正确运行的，那么如何才能编写一个真正的跨平台的Java程序呢？
下面是在编写跨平台的Java程序是需要注意的一些事情：
1. 编写Java跨平台应用程序时，你可以选择JDK1.0，1.1，1.2或支持它们的GUI开发工具如：Jbuilder,Visual Age for Java 等等，但是必须注意你的Java程序只能使用Java核心API包，如果要使用第三方的类库包，则该类库包也要由Java核心包开发完成，否则在发布你的程序的时候还得将支持该Java类库包的JVM发布出去。也就是说，你的程序需要是100%纯Java的。举一个例子，Visual J++ 就不是纯Java的，由Visual J++编写的程序也就不具有平台无关性。
2. 无论你使用的是JDK或其他开发工具，在编译时都要打开所有的警告选项，这样编译器可以尽可能多的发现平台相关的语句，并给出警告。虽然不能保证没有编译时警告错误的程序一定是跨平台的，但含有警告错误的程序却很有可能是非平台无关的。
3. 在程序中使用任何一个方法的时候，要详细察看文档，确保你使用的方法不是在文档中已经申明为过时的方法（Deprecated method）,也不是文档中未标明的隐含方法（Undocumented method）。
4. 退出Java程序时尽量不要使用java.lang.System的exit方法。Exit 方法可以终止JVM，从而终止程序，但如果同时运行了另一个Java程序，使用exit方法就会让该程序也关闭，这显然不是我们希望看到的情况。事实上要退出Java程序，可以使用destory()退出一个独立运行的过程。对于多线程程序，必须要关闭各个非守护线程。只有在程序非正常退出时，才使用 exit方法退出程序。
5. 避免使用本地方法和本地代码，尽可能自己编写具有相应功能的Java类，改写该方法。如果一定要使用该本地方法，可以编写一个服务器程序调用该方法，然后将现在要编写的程序作为该服务器程序的客户程序，或者考虑CORBA（公共对象请求代理）程序结构。
6. Java中有一个类似于Delphi中的winexec的方法，java.lang.runtime类的exec方法，作为该方法本身是具有平台无关性的，但是给方法所调用的命令及命令参数却是与平台相关的，因此，在编写程序时要避免使用，如果一定要调用其他的程序的话，必须要让用户自己来设置该命令及其参数。比如说，在windows中可以调用notepad.exe程序，在linux 中就要调用vi程序了。
7. 程序设计中的所有的信息都要使用ASCII码字符集，因为并不是所有的操作系统都支持Unicode字符集，这对于跨平台的Java中文软件程序不能不说是一大噩耗。
8. 在程序中不要硬性编码与平台相关的任何常量，比如行分隔符，文件分隔符，路径分隔符等等，这些常量在不同的平台上是不同的，比如文件分隔符，在UNIX和 MAC中是“/”，在windows中是“\”，如果要使用这些常量，需要使用java.io.File 类 如获得文件分隔符File.separator, 获得路径分隔符:File.pathSeparator;举例：myPath + File.separator+myFileName//跨平台、可移植性好
9. 在编写跨平台的网络程序时，不要使用java.net.InetAddress类的getHostName方法得到主机名，因为不同的平台的主机名格式是不同的，最好使用getAddress得到格式相同的IP地址，另外，程序中所有的主机名都要换成IP地址，比如www.263.net就要换成相应的 IP地址。
10. 涉及文件操作的程序需要注意：不要在程序中硬性编码文件路径，理由和8中一样，只是这一点特别重要，因此单独提出。而且，不同平台对于文件名使用的字符及最大文件名长度的要求不同，编写你的程序的时候要使用一般的ASCII码字符作为文件的名字，而且不能与平台中已存在的程序同名，否则会造成冲突。
11. 如果您写的程序是GUI程序，在使用AWT组件时不能硬性设置组件的大小和位置而应该使用Java的布局管理器（layout manager）来设置和管理可视组件的大小和位置，否则有可能造成布局混乱。
12. 由于不同的操作系统，不同的机器，系统支持的颜色和屏幕的大小和分辨率都不同，如何获得这些属性呢？使用java.awt.Systemcolor类可以获得需要的颜色，如该类的inactiveCaption 就是窗口边框中活动标题的背景颜色，menu则是菜单的背景颜色。使用java.awt.Toolkit的getScreenResolution可以以 “象素每英寸”为单位显示屏幕的分辨率。该类的getScreenSize可以得到屏幕大小（英寸），loadSystemColors可以列出所有的系统颜色。
13. 有关JDBC，JDBC有四种类型，要使用纯java的JDBC驱动，不要使用ODBC桥及其他平台相关的JDBC驱动。

参考：
实现Java程序跨平台运行十二个注意事项：http://blog.chinaunix.net/uid-20550186-id-1927257.html