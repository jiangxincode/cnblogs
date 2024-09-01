pom.xml中添加了taglist-maven-plugin配置，片段如下：

```xml
                <plugin>
                    <groupId>com.googlecode.l10n-maven-plugin</groupId>
                    <artifactId>l10n-maven-plugin</artifactId>
                    <version>1.8</version>
                    <configuration>
                        <locales>
                            <locale>en</locale>
                            <locale>zh_CN</locale>
                        </locales>
                    </configuration>
                </plugin>
```

执行`mvn clean package site`时报错`[WARNING] No dictionary file under folder`，详细报错如下：

```powershell
[INFO] Generating "L10n validation" report --- l10n-maven-plugin:1.8:report
[INFO] Initializing l10n validators...
[INFO] Looking for .dic files in: D:\temp\Java\ApkToolBoxGUI\src\main\resources
[WARNING] No dictionary file under folder D:\temp\Java\ApkToolBoxGUI\src\main\resources. Skipping spellcheck validation.
[INFO] Looking for .properties files in: D:\temp\Java\ApkToolBoxGUI\src\main\resources
```

解决方案:

* l10n-maven-plugin: <https://github.com/rquinio/l10n-maven-plugin>
* l10n-maven-plugin Validators: <https://github.com/rquinio/l10n-maven-plugin/wiki/Validators>
* Jazzy - Java Spell Check API: <https://sourceforge.net/projects/jazzy/>
* JazzyDicts - A Free Dictionary Set: <https://sourceforge.net/projects/jazzydicts/>