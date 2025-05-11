
工作中经常需要使用Eclipse远程连接Tomcat，调试Web应用程序，关于如何进行远程调试，本文不再赘述，可以参考下面的文章：

   eclipse远程调试Tomcat方法：http://blog.csdn.net/afgasdg/article/details/9236877

但是按照上面的方法进行操作可能会有一些小问题，在远程服务器中更改Tomcat的配置文件catalina.sh之后第一次重启Tomcat时，一般是没有问题的（注意设置的DEBUG端口号不要和其它已有应用端口号冲突），但是在之后的重启过程中可能会出现下面的问题：

    cd tomcat/bin
    ./shutdown.sh ; ./startup.sh ; tailf ../logs/catalina.out

    ERROR: transport error 202: bind failed
    ERROR: JDWP Transport dt_socket failed to initialize, TRANSPORT_INIT(510)
    JDWP exit error AGENT_ERROR_TRANSPORT_INIT(197): No transports initialized [../../../src/share/back/debugInit.c:690]
    FATAL ERROR in native method: JDWP No transports initialized, jvmtiError=AGENT_ERROR_TRANSPORT_INIT(197)

之所以出现这个问题，主要是因为，我们添加的DEBUG端口在关闭Tomcat时不能正常关闭，重启时又会重新开启，所以端口被占用，我们可以在关闭Tomcat之后利用下面的命令进行验证会发现，仍然有进程在占用着DEBUG端口。

    lsof -i:44121(或者 netstat -na|grep 44121)

这个其实就是我们自己之前开启的。当然我们可以在每次shutdown之后手动kill掉这个进程，但是终归不是解决之道。我现在想到的比较好的方法是在catalina.sh中配置DEBUG端口时，把需要添加的那一行添加到start条件的开始处：

    ...
    elif [ "$1" = "start" ] ; then
    CATALINA_OPTS="-Xdebug  -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
    ...
   
并且在stop条件的开始处把DEBUG端口干掉

    ...
    elif [ "$1" = "stop" ] ; then
    debug_pid=`lsof -i:44121 | tail -n 1 | awk -F" " '{print $2}'`
    kill -9 ${debug_pid}·
    ...