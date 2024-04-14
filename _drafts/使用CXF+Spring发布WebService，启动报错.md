使用CXF+Spring发布WebService，启动报错，日志如下:

```shell
五月 12, 2017 9:01:37 下午 org.apache.tomcat.util.digester.SetPropertiesRule begin
警告: [SetPropertiesRule]{Server/Service/Engine/Host/Context} Setting property 'source' to 'org.eclipse.jst.jee.server:JavaWebTest' did not find a matching property.
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server version:        Apache Tomcat/8.0.15
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server built:          Nov 2 2014 19:25:20 UTC
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Server number:         8.0.15.0
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: OS Name:               Windows 10
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: OS Version:            10.0
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Architecture:          amd64
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: JAVA_HOME:             C:\Java\jdk1.8.0_74\jre
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: JVM Version:           1.8.0_74-b02
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: JVM Vendor:            Oracle Corporation
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: CATALINA_BASE:         D:\temp\Java\.metadata\.plugins\org.eclipse.wst.server.core\tmp0
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: CATALINA_HOME:         C:\apache-tomcat-8.0.15
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Dcatalina.base=D:\temp\Java\.metadata\.plugins\org.eclipse.wst.server.core\tmp0
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Dcatalina.home=C:\apache-tomcat-8.0.15
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Dwtp.deploy=D:\temp\Java\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Djava.endorsed.dirs=C:\apache-tomcat-8.0.15\endorsed
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.VersionLoggerListener log
信息: Command line argument: -Dfile.encoding=UTF-8
五月 12, 2017 9:01:37 下午 org.apache.catalina.core.AprLifecycleListener lifecycleEvent
信息: The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: C:\Java\jdk1.8.0_74\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:/Java/jre1.8.0_102/bin/server;C:/Java/jre1.8.0_102/bin;C:/Java/jre1.8.0_102/lib/amd64;C:\tools;C:\Program Files\Git\bin;D:\temp\Go\GOPATH\bin;C:\go\bin;C:\ProgramData\Oracle\Java\javapath;C:\apache-maven-3.3.9\bin;C:\Program Files (x86)\Vim\vim80;C:\Java\jdk1.8.0_102\bin;C:\Java\jdk1.8.0_102\jre\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files\TortoiseSVN\bin;C:\Program Files\VisualSVN Server\bin;C:\Program Files\Git\cmd;C:\TDM-GCC-64\bin;C:\Program Files\TortoiseGit\bin;C:\Program Files (x86)\sbt\bin;;C:\Users\jiang\AppData\Local\Microsoft\WindowsApps;C:\Program Files (x86)\Microsoft VS Code\bin;C:\eclipse;;.
五月 12, 2017 9:01:37 下午 org.apache.coyote.AbstractProtocol init
信息: Initializing ProtocolHandler ["http-nio-8080"]
五月 12, 2017 9:01:37 下午 org.apache.tomcat.util.net.NioSelectorPool getSharedSelector
信息: Using a shared selector for servlet write/read
五月 12, 2017 9:01:37 下午 org.apache.coyote.AbstractProtocol init
信息: Initializing ProtocolHandler ["ajp-nio-8009"]
五月 12, 2017 9:01:37 下午 org.apache.tomcat.util.net.NioSelectorPool getSharedSelector
信息: Using a shared selector for servlet write/read
五月 12, 2017 9:01:37 下午 org.apache.catalina.startup.Catalina load
信息: Initialization processed in 530 ms
五月 12, 2017 9:01:37 下午 org.apache.catalina.core.StandardService startInternal
信息: Starting service Catalina
五月 12, 2017 9:01:37 下午 org.apache.catalina.core.StandardEngine startInternal
信息: Starting Servlet Engine: Apache Tomcat/8.0.15
五月 12, 2017 9:01:38 下午 org.apache.catalina.util.SessionIdGeneratorBase createSecureRandom
信息: Creation of SecureRandom instance for session ID generation using [SHA1PRNG] took [532] milliseconds.
五月 12, 2017 9:01:58 下午 org.apache.catalina.core.ApplicationContext log
信息: No Spring WebApplicationInitializer types detected on classpath
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/D:/temp/Java/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/JavaWebTest/WEB-INF/lib/log4j-slf4j-impl-2.8.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/D:/temp/Java/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/JavaWebTest/WEB-INF/lib/slf4j-log4j12-1.7.5.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
五月 12, 2017 9:01:58 下午 org.apache.catalina.core.ApplicationContext log
信息: Initializing Spring root WebApplicationContext
20840 [localhost-startStop-1] INFO  o.s.w.c.ContextLoader - Root WebApplicationContext: initialization started
20933 [localhost-startStop-1] INFO  o.s.w.c.s.XmlWebApplicationContext - Refreshing Root WebApplicationContext: startup date [Fri May 12 21:01:58 CST 2017]; root of context hierarchy
21006 [localhost-startStop-1] INFO  o.s.b.f.x.XmlBeanDefinitionReader - Loading XML bean definitions from ServletContext resource [/WEB-INF/classes/applicationContext.xml]
attribute added
org.springframework.web.context.support.ServletContextScope:org.springframework.web.context.support.ServletContextScope@a5fec7e
21956 [localhost-startStop-1] INFO  c.m.v.l.MLog - MLog clients using log4j logging.
22008 [localhost-startStop-1] INFO  c.m.v.c.C3P0Registry - Initializing c3p0-0.9.1.2 [built 21-May-2007 15:04:56; debug? true; trace: 10]
22869 [localhost-startStop-1] INFO  o.a.c.w.s.f.ReflectionServiceFactoryBean - Creating Service {employeemanager.webservice.jiangxin.edu}EmployeeService from class edu.jiangxin.webservice.employeemanager.EmployeeManager
23054 [localhost-startStop-1] WARN  o.s.w.c.s.XmlWebApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean---1459474130': Invocation of init method failed; nested exception is java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
23058 [localhost-startStop-1] ERROR o.s.w.c.ContextLoader - Context initialization failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean---1459474130': Invocation of init method failed; nested exception is java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1628) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:555) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:197) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:761) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:866) ~[spring-context-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:542) ~[spring-context-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.web.context.ContextLoader.configureAndRefreshWebApplicationContext(ContextLoader.java:443) ~[spring-web-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.web.context.ContextLoader.initWebApplicationContext(ContextLoader.java:325) [spring-web-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.web.context.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:107) [spring-web-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:4772) [catalina.jar:8.0.15]
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5196) [catalina.jar:8.0.15]
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150) [catalina.jar:8.0.15]
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1409) [catalina.jar:8.0.15]
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1399) [catalina.jar:8.0.15]
	at java.util.concurrent.FutureTask.run(FutureTask.java:266) [?:1.8.0_74]
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142) [?:1.8.0_74]
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617) [?:1.8.0_74]
	at java.lang.Thread.run(Thread.java:745) [?:1.8.0_74]
Caused by: java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
	at java.lang.Class.getDeclaredConstructors0(Native Method) ~[?:1.8.0_74]
	at java.lang.Class.privateGetDeclaredConstructors(Class.java:2671) ~[?:1.8.0_74]
	at java.lang.Class.getConstructor0(Class.java:3075) ~[?:1.8.0_74]
	at java.lang.Class.getDeclaredConstructor(Class.java:2178) ~[?:1.8.0_74]
	at org.apache.cxf.common.util.ReflectionUtil$4.run(ReflectionUtil.java:105) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.common.util.ReflectionUtil$4.run(ReflectionUtil.java:102) ~[cxf-core-3.1.11.jar:3.1.11]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:1.8.0_74]
	at org.apache.cxf.common.util.ReflectionUtil.getDeclaredConstructor(ReflectionUtil.java:102) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.common.jaxb.JAXBUtils.getValidClass(JAXBUtils.java:587) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxb.JAXBContextInitializer.addClass(JAXBContextInitializer.java:324) ~[cxf-rt-databinding-jaxb-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxb.JAXBContextInitializer.begin(JAXBContextInitializer.java:187) ~[cxf-rt-databinding-jaxb-3.1.11.jar:3.1.11]
	at org.apache.cxf.service.ServiceModelVisitor.visitOperation(ServiceModelVisitor.java:97) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.service.ServiceModelVisitor.walk(ServiceModelVisitor.java:74) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxb.JAXBDataBinding.initialize(JAXBDataBinding.java:315) ~[cxf-rt-databinding-jaxb-3.1.11.jar:3.1.11]
	at org.apache.cxf.service.factory.AbstractServiceFactoryBean.initializeDataBindings(AbstractServiceFactoryBean.java:86) ~[cxf-core-3.1.11.jar:3.1.11]
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.buildServiceFromClass(ReflectionServiceFactoryBean.java:470) ~[cxf-rt-wsdl-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxws.support.JaxWsServiceFactoryBean.buildServiceFromClass(JaxWsServiceFactoryBean.java:696) ~[cxf-rt-frontend-jaxws-3.1.11.jar:3.1.11]
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.initializeServiceModel(ReflectionServiceFactoryBean.java:530) ~[cxf-rt-wsdl-3.1.11.jar:3.1.11]
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.create(ReflectionServiceFactoryBean.java:263) ~[cxf-rt-wsdl-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxws.support.JaxWsServiceFactoryBean.create(JaxWsServiceFactoryBean.java:199) ~[cxf-rt-frontend-jaxws-3.1.11.jar:3.1.11]
	at org.apache.cxf.frontend.AbstractWSDLBasedEndpointFactory.createEndpoint(AbstractWSDLBasedEndpointFactory.java:102) ~[cxf-rt-frontend-simple-3.1.11.jar:3.1.11]
	at org.apache.cxf.frontend.ServerFactoryBean.create(ServerFactoryBean.java:168) ~[cxf-rt-frontend-simple-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxws.JaxWsServerFactoryBean.create(JaxWsServerFactoryBean.java:211) ~[cxf-rt-frontend-jaxws-3.1.11.jar:3.1.11]
	at org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean.create(NamespaceHandler.java:60) ~[cxf-rt-frontend-jaxws-3.1.11.jar:3.1.11]
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[?:1.8.0_74]
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[?:1.8.0_74]
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[?:1.8.0_74]
	at java.lang.reflect.Method.invoke(Method.java:498) ~[?:1.8.0_74]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeCustomInitMethod(AbstractAutowireCapableBeanFactory.java:1758) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1695) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1624) ~[spring-beans-4.3.8.RELEASE.jar:4.3.8.RELEASE]
	... 21 more
attribute added
org.springframework.web.context.WebApplicationContext.ROOT:org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean---1459474130': Invocation of init method failed; nested exception is java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
五月 12, 2017 9:02:00 下午 org.apache.catalina.core.StandardContext listenerStart
严重: Exception sending context initialized event to listener instance of class org.springframework.web.context.ContextLoaderListener
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean---1459474130': Invocation of init method failed; nested exception is java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1628)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:555)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:483)
	at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:306)
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:302)
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:197)
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:761)
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:866)
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:542)
	at org.springframework.web.context.ContextLoader.configureAndRefreshWebApplicationContext(ContextLoader.java:443)
	at org.springframework.web.context.ContextLoader.initWebApplicationContext(ContextLoader.java:325)
	at org.springframework.web.context.ContextLoaderListener.contextInitialized(ContextLoaderListener.java:107)
	at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:4772)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5196)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1409)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1399)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:745)
Caused by: java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
	at java.lang.Class.getDeclaredConstructors0(Native Method)
	at java.lang.Class.privateGetDeclaredConstructors(Class.java:2671)
	at java.lang.Class.getConstructor0(Class.java:3075)
	at java.lang.Class.getDeclaredConstructor(Class.java:2178)
	at org.apache.cxf.common.util.ReflectionUtil$4.run(ReflectionUtil.java:105)
	at org.apache.cxf.common.util.ReflectionUtil$4.run(ReflectionUtil.java:102)
	at java.security.AccessController.doPrivileged(Native Method)
	at org.apache.cxf.common.util.ReflectionUtil.getDeclaredConstructor(ReflectionUtil.java:102)
	at org.apache.cxf.common.jaxb.JAXBUtils.getValidClass(JAXBUtils.java:587)
	at org.apache.cxf.jaxb.JAXBContextInitializer.addClass(JAXBContextInitializer.java:324)
	at org.apache.cxf.jaxb.JAXBContextInitializer.begin(JAXBContextInitializer.java:187)
	at org.apache.cxf.service.ServiceModelVisitor.visitOperation(ServiceModelVisitor.java:97)
	at org.apache.cxf.service.ServiceModelVisitor.walk(ServiceModelVisitor.java:74)
	at org.apache.cxf.jaxb.JAXBDataBinding.initialize(JAXBDataBinding.java:315)
	at org.apache.cxf.service.factory.AbstractServiceFactoryBean.initializeDataBindings(AbstractServiceFactoryBean.java:86)
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.buildServiceFromClass(ReflectionServiceFactoryBean.java:470)
	at org.apache.cxf.jaxws.support.JaxWsServiceFactoryBean.buildServiceFromClass(JaxWsServiceFactoryBean.java:696)
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.initializeServiceModel(ReflectionServiceFactoryBean.java:530)
	at org.apache.cxf.wsdl.service.factory.ReflectionServiceFactoryBean.create(ReflectionServiceFactoryBean.java:263)
	at org.apache.cxf.jaxws.support.JaxWsServiceFactoryBean.create(JaxWsServiceFactoryBean.java:199)
	at org.apache.cxf.frontend.AbstractWSDLBasedEndpointFactory.createEndpoint(AbstractWSDLBasedEndpointFactory.java:102)
	at org.apache.cxf.frontend.ServerFactoryBean.create(ServerFactoryBean.java:168)
	at org.apache.cxf.jaxws.JaxWsServerFactoryBean.create(JaxWsServerFactoryBean.java:211)
	at org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean.create(NamespaceHandler.java:60)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeCustomInitMethod(AbstractAutowireCapableBeanFactory.java:1758)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1695)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1624)
	... 21 more

initializedorg.apache.catalina.core.ApplicationContextFacade@5361fb9
五月 12, 2017 9:02:00 下午 org.apache.catalina.core.StandardContext startInternal
严重: Error listenerStart
五月 12, 2017 9:02:00 下午 org.apache.catalina.core.StandardContext startInternal
严重: Context [/JavaWebTest] startup failed due to previous errors
attribute removed
org.apache.logging.log4j.spi.LoggerContext.INSTANCE:org.apache.logging.log4j.core.LoggerContext@3a43c847
destroyedorg.apache.catalina.core.ApplicationContextFacade@5361fb9
五月 12, 2017 9:02:00 下午 org.apache.catalina.core.ApplicationContext log
信息: Closing Spring root WebApplicationContext
attribute removed
org.springframework.web.context.WebApplicationContext.ROOT:org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.apache.cxf.jaxws.spring.NamespaceHandler$SpringServerFactoryBean---1459474130': Invocation of init method failed; nested exception is java.lang.VerifyError: (class: edu/jiangxin/webservice/employeemanager/jaxws_asm/Add, method: setEmployee signature: (Ledu/jiangxin/webservice/employeemanager/Employee;)V) Illegal instruction found at offset 1
五月 12, 2017 9:02:00 下午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
警告: The web application [JavaWebTest] appears to have started a thread named [Log4j2-TF-2-Scheduled-2] but has failed to stop it. This is very likely to create a memory leak. Stack trace of thread:
 sun.misc.Unsafe.park(Native Method)
 java.util.concurrent.locks.LockSupport.parkNanos(LockSupport.java:215)
 java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject.awaitNanos(AbstractQueuedSynchronizer.java:2078)
 java.util.concurrent.ScheduledThreadPoolExecutor$DelayedWorkQueue.take(ScheduledThreadPoolExecutor.java:1093)
 java.util.concurrent.ScheduledThreadPoolExecutor$DelayedWorkQueue.take(ScheduledThreadPoolExecutor.java:809)
 java.util.concurrent.ThreadPoolExecutor.getTask(ThreadPoolExecutor.java:1067)
 java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1127)
 java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
 java.lang.Thread.run(Thread.java:745)
五月 12, 2017 9:02:00 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["http-nio-8080"]
五月 12, 2017 9:02:00 下午 org.apache.coyote.AbstractProtocol start
信息: Starting ProtocolHandler ["ajp-nio-8009"]
五月 12, 2017 9:02:00 下午 org.apache.catalina.startup.Catalina start
信息: Server startup in 22504 ms
```

解决方法是：更新ASM的maven依赖，并去除项目中对asm的间接依赖。