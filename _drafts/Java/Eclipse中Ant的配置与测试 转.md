
Ant是Java平台下非常棒的批处理命令执行程序，能非常方便地自动完成编译，测试，打包，部署等等一系列任务，大大提高开发效率。如果你现在还没有开始使用Ant，那就要赶快开始学习使用，使自己的开发水平上一个新台阶。Eclipse中已经集成了Ant，我们可以直接在Eclipse中运行Ant。以前面建立的Hello工程为例，创建以下目录结构：

![](http://images2015.cnblogs.com/blog/611264/201512/611264-20151211222840887-2057018532.jpg)

新建一个build.xml，放在工程根目录下。build.xml定义了Ant要执行的批处理命令。虽然Ant也可以使用其它文件名，但是遵循标准能更使开发更规范，同时易于与别人交流。 通常，src存放Java源文件，classes存放编译后的class文件，lib存放编译和运行用到的所有jar文件，web存放JSP等web文件，dist存放打包后的jar文件，doc存放API文档。然后在根目录下创建build.xml文件，输入以下内容：

```xml

<?xml version="1.0"?>
<project name="Hello world" default="doc">
	<!-- properies -->
	<property name="src.dir" value="src" />
	<property name="report.dir" value="report" />
	<property name="classes.dir" value="classes" />
	<property name="lib.dir" value="lib" />
	<property name="dist.dir" value="dist" />
	<property name="doc.dir" value="doc" />
	<!-- 定义classpath -->
	<path id="master-classpath">
		<fileset file="${lib.dir}/*.jar" />
		<pathelement path="${classes.dir}" />
	</path>
	<!-- 初始化任务 -->
	<target name="init">
	</target>
	<!-- 编译 -->
	<target name="compile" depends="init" description="compile the source files">
		<mkdir dir="${classes.dir}" />
		<javac srcdir="${src.dir}" destdir="${classes.dir}" target="1.4">
			<classpath refid="master-classpath" />
		</javac>
	</target>
	<!-- 测试 -->
	<target name="test" depends="compile" description="run junit test">
		<mkdir dir="${report.dir}" />
		<junit printsummary="on" haltonfailure="false" failureproperty="tests.failed"
			showoutput="true">
			<classpath refid="master-classpath" />
			<formatter type="plain" />
			<batchtest todir="${report.dir}">
				<fileset dir="${classes.dir}">
					<include name="**/*Test.*" />
				</fileset>
			</batchtest>
		</junit>
		<fail if="tests.failed">
			***********************************************************
			**** One or more tests failed! Check the output ... ****
			***********************************************************
		</fail>
	</target>
	<!-- 打包成jar -->
	<target name="pack" depends="test" description="make .jar file">
		<mkdir dir="${dist.dir}" />
		<jar destfile="${dist.dir}/hello.jar" basedir="${classes.dir}">
			<exclude name="**/*Test.*" />
			<exclude name="**/Test*.*" />
		</jar>
	</target>
	<!-- 输出api文档 -->
	<target name="doc" depends="pack" description="create api doc">
		<mkdir dir="${doc.dir}" />
		<javadoc destdir="${doc.dir}" author="true" version="true"
			use="true" windowtitle="Test API">
			<packageset dir="${src.dir}" defaultexcludes="yes">
				<include name="example/**" />
			</packageset>
			<doctitle><![CDATA[<h1>Hello, test</h1>]]></doctitle>
			<bottom><![CDATA[<i>All Rights Reserved.</i>]]></bottom>
			<tag name="todo" scope="all" description="To do:" />
		</javadoc>
	</target>
</project>

```

选中Hello工程，然后选择“Project”，“Properties”，“Builders”，“New…”，选择“Ant Build”：
    
![](http://images2015.cnblogs.com/blog/611264/201512/611264-20151211222905012-466425527.jpg)

填入Name：Ant_Builder；Buildfile：build.xml；Base Directory：${workspace_loc:/Hello}（按“Browse Workspace”选择工程根目录），由于用到了junit.jar包，搜索Eclipse目录，找到junit.jar，把它复制到Hello/lib目录下，并添加到Ant的Classpath中：

![](http://images2015.cnblogs.com/blog/611264/201512/611264-20151211222917434-787575864.jpg)

然后在Builder面板中钩上Ant_Build，去掉Java Builder：

![](http://images2015.cnblogs.com/blog/611264/201512/611264-20151211222930747-1268707877.jpg)

再次编译，即可在控制台看到Ant的输出： 

```shell

Buildfile: F:\eclipse-projects\Hello\build.xml
init:
compile:
[mkdir] Created dir: F:\eclipse-projects\Hello\classes
[javac] Compiling 2 source files to F:\eclipse-projects\Hello\classes
test:
[mkdir] Created dir: F:\eclipse-projects\Hello\report
[junit] Running example.HelloTest
[junit] Tests run: 1, Failures: 0, Errors: 0, Time elapsed: 0.02 sec
pack:
[mkdir] Created dir: F:\eclipse-projects\Hello\dist
[jar] Building jar: F:\eclipse-projects\Hello\dist\hello.jar
doc:
[mkdir] Created dir: F:\eclipse-projects\Hello\doc
[javadoc] Generating Javadoc
[javadoc] Javadoc execution
[javadoc] Loading source files for package example...
[javadoc] Constructing Javadoc information...
[javadoc] Standard Doclet version 1.4.2_04
[javadoc] Building tree for all the packages and classes...
[javadoc] Building index for all the packages and classes...
[javadoc] Building index for all classes...
[javadoc] Generating F:\eclipse-projects\Hello\doc\stylesheet.css...
[javadoc] Note: Custom tags that could override future standard tags:  
@todo. To avoid potential overrides, use at least one period character (.) in custom tag names.
[javadoc] Note: Custom tags that were not seen:  @todo
BUILD SUCCESSFUL
Total time: 11 seconds

```

Ant依次执行初始化，编译，测试，打包，生成API文档一系列任务，极大地提高了开发效率。将来开发J2EE项目时，还可加入部署等任务。并且，即使脱离了Eclipse环境，只要正确安装了Ant，配置好环境变量ANT_HOME=<Ant解压目录>，Path=…;%ANT_HOME%\bin，在命令行提示符下切换到Hello目录，简单地键入ant即可。