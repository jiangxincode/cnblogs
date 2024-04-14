欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: <http://www.cnblogs.com/jiangxinnju>
GitHub地址: <https://github.com/jiangxincode>
知乎地址: <https://www.zhihu.com/people/jiangxinnju>

* src源代码生成html格式文档: <http://www.cnblogs.com/shenliang123/archive/2012/04/23/2466483.html>
* 自己动手制作chm格式开源文档: <http://www.cnblogs.com/shenliang123/archive/2012/04/23/2466441.html>
* Javadoc转换chm帮助文档的四种方法总结: <http://lishunli.iteye.com/blog/1051688>
* 如何使用eclipse生成javadoc帮助文档: <http://jingyan.baidu.com/article/dca1fa6f4d3d7ff1a4405239.html>
* javadoc.io: <http://www.javadoc.io/>


## maven下载源码和javadoc

当在IDE中使用Maven时如果想要看引用的jar包中类的源码和javadoc需要通过maven命令下载这些源码，然后再进行引入，通过mvn命令能够容易的达到这个目的：

```shell
    mvn dependency:sources
    mvn dependency:resolve -Dclassifier=javadoc
```

命令使用方法：首先进入到相应的pom.xml目录中，然后执行以上命令。第一个命令尝试下载在pom.xml中依赖的文件的源代码。第二个命令尝试下载对应的javadocs。但是有可能一些文件没有源代码或者javadocs。也可以通过配置文件添加，打开maven配置文件 setting.xml文件(.../.m2/settings.xml) 增加如下配置：

```xml
    <profiles>
    <profile>
        <id>downloadSources</id>
        <properties>
            <downloadSources>true</downloadSources>
            <downloadJavadocs>true</downloadJavadocs>
        </properties>
    </profile>
    </profiles>

    <activeProfiles>
      <activeProfile>downloadSources</activeProfile>
    </activeProfiles>
```

配置eclipse

    Window > Preferences > Maven and checking the "Download Artifact Sources" and "Download Artifact JavaDoc" options
	

## maven中如何生成javadoc

mvn javadoc:javadoc


## javadoc注意点（原创）

javadoc生成文档时总是报java.lang.IllegalArgumentException错

JavamavenEXTSUNJDK .

javadoc生成文档时总是报java.lang.IllegalArgumentException错误,是classpath里面字符冲突引起的。我在classpath中包含了变量引用，如：%JAVA_HOME%\lib;解决方法是重新设置classpath或者删除classpath.要注意设置完成后重启下cmd或者editplus，重启后生效！

见官方参考文档 http://maven.apache.org/plugins/maven-javadoc-plugin/faq.html


## javadoc生成时出错：编码GBK的不可映射字符

由于java源代码是用的UTF-8编码，Eclipse中默认编码是GB18030，因此，在生成javadoc的时候，需要手工指定一下编码和字符集。

解决方案是：主菜单`–>Project–>Generate javadoc–>next>next–>` 在 `Extra javadoc options`下面的文本框中填入：

`-encoding UTF-8 -charset UTF-8`

## 一个例子

`javadoc -d doc -subpackages edu.jiangxin -encoding utf-8 -charset utf-8 -exclude edu.jiangxin.utils:edu.jiangxin.service:edu.jiangxin.service.impl`