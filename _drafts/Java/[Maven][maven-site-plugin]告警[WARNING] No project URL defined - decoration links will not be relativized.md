pom.xml中添加了maven-site-plugin配置，片段如下：

```xml
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-site-plugin</artifactId>
                <version>3.9.0</version>
                <configuration>
                    <locales>en_US</locales>
                    <outputDirectory>${project.build.directory}/site</outputDirectory>
                </configuration>
            </plugin>
```

执行`mvn clean package site`时报错`[WARNING] No project URL defined - decoration links will not be relativized!`，详细报错如下：

```powershell
[INFO] --- maven-site-plugin:3.9.0:site (default-site) @ APKToolBoxGUI ---
...
[INFO] Rendering site with default locale English (United States) (en_US)
[WARNING] No project URL defined - decoration links will not be relativized!
[INFO] Rendering content with org.apache.maven.skins:maven-default-skin:jar:1.3 skin.
```

这个WARNING指maven-site-plugin有个功能就是帮你将生成的site信息中的绝对路径改为相对路径，比如地址是<https://jiangxincode.github.io/ApkToolBoxGUI/findbugs.html>，且知道基础路径是<<https://jiangxincode.github.io/ApkToolBoxGUI>那么就可以帮你把地址改成相对的`findbugs.html`。默认情况下这个功能是打开的，但是你如果没有制定基础路径，插件就没有办法帮你将绝对路径改为相对路径，所以会给出一个WARNING，详细信息可以查看官网：<http://maven.apache.org/plugins/maven-site-plugin/site-mojo.html>。原因知道了，解决方案就简单了，如果你不需要改功能就直接通过配置关闭就可以了。

```xml
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-site-plugin</artifactId>
                <version>3.9.0</version>
                <configuration>
                    <locales>en_US</locales>
                    <outputDirectory>${project.build.directory}/site</outputDirectory>
                    <relativizeDecorationLinks>false</relativizeDecorationLinks>
                </configuration>
            </plugin>
```
