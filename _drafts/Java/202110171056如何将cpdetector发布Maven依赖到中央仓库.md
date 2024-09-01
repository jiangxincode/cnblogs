参考：
https://www.cnblogs.com/jiangxinnju/p/9903517.html

从官网下载最新版本的发布包
https://sourceforge.net/projects/cpdetector/

1、生成cpdetector_1.0.10_bundle.jar

解压后把几个依赖的包放到一起，为了简单把cpdetector*.jar和几个扩展依赖打包到一起，解压各个jar包
jar -xvf .\cpdetector_1.0.10.jar
jar -xvf .\chardet-1.0.jar
jar -xvf .\antlr-2.7.4.jar
jar -xvf .\jargs-1.0.jar
把jar包移除，然后
jar -cvfM cpdetector-1.0.10.jar .

2、生成cpdetector-1.0.10-javadoc.jar和cpdetector-1.0.10-sources.jar

jar -cvf cpdetector-1.0.10-javadoc.jar .\binary-release.txt .\MPL-1.1.txt
jar -cvf cpdetector-1.0.10-sources.jar .\binary-release.txt .\MPL-1.1.txt

3、生成cpdetector-1.0.10.pom

然后创建pom.xml，填写对应信息。

```xml
<project
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.github.jiangxincode</groupId>
    <artifactId>cpdetector</artifactId>
    <version>1.0.10</version>
    <packaging>jar</packaging>
    <name>cpdetector</name>
    <description>cpDetector is a proxy for codepage detection of documents. It delegates to multiple instances that try to detect the codepage by different techinques. A command line executeable is shipped that allows to sort documents by codepage.</description>
    <url>https://sourceforge.net/projects/cpdetector/</url>
    <licenses>
        <license>
            <name>MPL-1.1</name>
            <url>https://www.mozilla.org/en-US/MPL/1.1/</url>
        </license>
    </licenses>
    <scm>
        <url>git://git.code.sf.net/p/cpdetector/sourcecode cpdetector-sourcecode</url>
        <connection>git://git.code.sf.net/p/cpdetector/sourcecode cpdetector-sourcecode</connection>
        <developerConnection>git://git.code.sf.net/p/cpdetector/sourcecode cpdetector-sourcecode</developerConnection>
    </scm>
    <developers>
        <developer>
            <name>achimwestermann</name>
        </developer>
    </developers>
</project>
```

4、生成对应的asc签名文件

gpg --gen-key创建密钥(密码12345678)

pub   rsa3072 2021-10-17 [SC] [expires: 2023-10-17]
      6F52975E26BFE145B5A23C55A11AA01F0E9838A9
uid                      Aloys <jiangxinnju@163.com>
sub   rsa3072 2021-10-17 [E] [expires: 2023-10-17]

分发公钥到某个公钥服务器
gpg --keyserver hkp://keyserver.ubuntu.com --send-keys 6F52975E26BFE145B5A23C55A11AA01F0E9838A9

gpg -ab .\cpdetector-1.0.10.jar
gpg -ab .\cpdetector-1.0.10-javadoc.jar
gpg -ab .\cpdetector-1.0.10-sources.jar
gpg -ab .\cpdetector-1.0.10.pom

5、打包到一起
jar -cvf bundle.jar cpdetector-1.0.10*