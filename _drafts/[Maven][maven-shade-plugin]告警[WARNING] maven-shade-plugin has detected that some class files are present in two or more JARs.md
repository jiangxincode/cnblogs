pom.xml中添加了maven-shade-plugin配置，片段如下：

```xml
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.2.2</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer
                                    implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <manifestEntries>
                                        <Main-Class>edu.jiangxin.apktoolbox.main.MainFrame</Main-Class>
                                    </manifestEntries>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```

执行`mvn clean package`时报错`[WARNING] maven-shade-plugin has detected that some class files are present in two or more JARs.`，详细报错如下：

```powershell
[INFO] --- maven-shade-plugin:3.2.2:shade (default) @ APKToolBoxGUI ---
[INFO] Including commons-io:commons-io:jar:2.6 in the shaded jar.
[INFO] Including org.apache.commons:commons-collections4:jar:4.3 in the shaded jar.
[INFO] Including org.apache.commons:commons-lang3:jar:3.9 in the shaded jar.
[INFO] Including org.jdom:jdom2:jar:2.0.6 in the shaded jar.
[INFO] Including org.apache.logging.log4j:log4j-api:jar:2.13.0 in the shaded jar.
[INFO] Including org.apache.logging.log4j:log4j-core:jar:2.13.0 in the shaded jar.
[INFO] Including org.apache.commons:commons-configuration2:jar:2.7 in the shaded jar.
[INFO] Including org.apache.commons:commons-text:jar:1.8 in the shaded jar.
[INFO] Including commons-logging:commons-logging:jar:1.2 in the shaded jar.
[INFO] Including commons-beanutils:commons-beanutils:jar:1.9.4 in the shaded jar.
[INFO] Including commons-collections:commons-collections:jar:3.2.2 in the shaded jar.
[INFO] Including cpdetector:cpdetector:jar:1.0.7 in the shaded jar.
[INFO] Including org.antlr:com.springsource.antlr:jar:2.7.7 in the shaded jar.
[INFO] Including jargs:jargs:jar:1.0 in the shaded jar.
[INFO] Including org.mozilla.intl:chardet:jar:1.0 in the shaded jar.
[INFO] Including com.googlecode.juniversalchardet:juniversalchardet:jar:1.0.3 in the shaded jar.
[INFO] Including org.apache.httpcomponents:httpclient:jar:4.5.7 in the shaded jar.
[INFO] Including org.apache.httpcomponents:httpcore:jar:4.4.11 in the shaded jar.
[INFO] Including commons-codec:commons-codec:jar:1.11 in the shaded jar.
[INFO] Including org.json:json:jar:20190722 in the shaded jar.
[INFO] Including junit:junit:jar:4.13 in the shaded jar.
[INFO] Including org.hamcrest:hamcrest-core:jar:1.3 in the shaded jar.
[WARNING] httpclient-4.5.7.jar, httpcore-4.4.11.jar, log4j-api-2.13.0.jar, log4j-core-2.13.0.jar define 3 overlapping resources: 
[WARNING]   - META-INF/DEPENDENCIES
[WARNING]   - META-INF/LICENSE
[WARNING]   - META-INF/NOTICE
[WARNING] commons-beanutils-1.9.4.jar, commons-codec-1.11.jar, commons-collections-3.2.2.jar, commons-collections4-4.3.jar, commons-configuration2-2.7.jar, commons-io-2.6.jar, commons-lang3-3.9.jar, commons-logging-1.2.jar, commons-text-1.8.jar, jdom2-2.0.6.jar define 1 overlapping resources: 
[WARNING]   - META-INF/LICENSE.txt
[WARNING] APKToolBoxGUI-0.0.4.jar, chardet-1.0.jar, com.springsource.antlr-2.7.7.jar, commons-beanutils-1.9.4.jar, commons-codec-1.11.jar, commons-collections-3.2.2.jar, commons-collections4-4.3.jar, commons-configuration2-2.7.jar, commons-io-2.6.jar, commons-lang3-3.9.jar, commons-logging-1.2.jar, commons-text-1.8.jar, cpdetector-1.0.7.jar, hamcrest-core-1.3.jar, httpclient-4.5.7.jar, httpcore-4.4.11.jar, jargs-1.0.jar, jdom2-2.0.6.jar, json-20190722.jar, junit-4.13.jar, juniversalchardet-1.0.3.jar, log4j-api-2.13.0.jar, log4j-core-2.13.0.jar define 1 overlapping resources: 
[WARNING]   - META-INF/MANIFEST.MF
[WARNING] commons-beanutils-1.9.4.jar, commons-codec-1.11.jar, commons-collections-3.2.2.jar, commons-collections4-4.3.jar, commons-configuration2-2.7.jar, commons-io-2.6.jar, commons-lang3-3.9.jar, commons-logging-1.2.jar, commons-text-1.8.jar define 1 overlapping resources: 
[WARNING]   - META-INF/NOTICE.txt
[WARNING] maven-shade-plugin has detected that some class files are
[WARNING] present in two or more JARs. When this happens, only one
[WARNING] single version of the class is copied to the uber jar.
[WARNING] Usually this is not harmful and you can skip these warnings,
[WARNING] otherwise try to manually exclude artifacts based on
[WARNING] mvn dependency:tree -Ddetail=true and the above output.
[WARNING] See http://maven.apache.org/plugins/maven-shade-plugin/
[INFO] Replacing original artifact with shaded artifact.
```

从日志中可以看出核心问题是依赖的不同jar包中同时包含相同的文件，导致maven-shade-plugin不知道选用哪个放到最终的合一jar包中，一种规避方式就是把这些文件进行过滤，不merge到最后的jar包中。当然如果涉及License、Notice等法务文件，需要自己重新将文件归一后打包到最终的合一jar包中。

```xml
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.2.2</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer
                                    implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <manifestEntries>
                                        <Main-Class>edu.jiangxin.apktoolbox.main.MainFrame</Main-Class>
                                    </manifestEntries>
                                </transformer>
                            </transformers>
                            <filters>
                                <filter>
                                    <artifact>*:*</artifact>
                                    <excludes>
                                        <exclude>META-INF/DEPENDENCIES</exclude>
                                        <exclude>META-INF/LICENSE*</exclude>
                                        <exclude>META-INF/NOTICE*</exclude>
                                        <exclude>META-INF/MANIFEST*</exclude>
                                    </excludes>
                                </filter>
                            </filters>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```
