pom.xml中添加了taglist-maven-plugin配置，片段如下：

```xml
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>taglist-maven-plugin</artifactId>
                    <version>2.4</version>
                    <configuration>
                        <tags>
                            <tag>fixme</tag>
                            <tag>FixMe</tag>
                            <tag>FIXME</tag>
                            <tag>@todo</tag>
                            <tag>todo</tag>
                            <tag>TODO</tag>
                            <tag>@deprecated</tag>
                        </tags>
                    </configuration>
                </plugin>
```

执行`mvn clean package site`时报错`[WARNING] Using legacy tag format.  This is not recommended.`，详细报错如下：

```powershell
[INFO] Generating "Tag List" report      --- taglist-maven-plugin:2.4:taglist
[WARNING] Using legacy tag format.  This is not recommended.
```

这个WARNING指taglist-maven-plugin新版本指定tag的方式有所变更，新方式功能更强大，详细信息可以查看：<http://jira.codehaus.org/browse/MTAGLIST-49>。新版本的使用实例如下：

```xml
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>taglist-maven-plugin</artifactId>
                    <version>2.4</version>
                    <configuration>
                        <tagListOptions>
                            <tagClasses>
                                <tagClass>
                                    <displayName>Todo Work Annotation</displayName>
                                    <tags>
                                        <tag>
                                            <matchString>TODO</matchString>
                                            <matchType>ignoreCase</matchType>
                                        </tag>
                                        <tag>
                                            <matchString>@todo</matchString>
                                            <matchType>ignoreCase</matchType>
                                        </tag>
                                        <tag>
                                            <matchString>FIXME</matchString>
                                            <matchType>exact</matchType>
                                        </tag>
                                    </tags>
                                </tagClass>
                                <tagClass>
                                    <displayName>Version Annotation</displayName>
                                    <tags>
                                        <tag>
                                            <matchString>@deprecated</matchString>
                                            <matchType>ignoreCase</matchType>
                                        </tag>
                                    </tags>
                                </tagClass>
                            </tagClasses>
                        </tagListOptions>
                    </configuration>
                </plugin>
```
