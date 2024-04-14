如果你用Maven进行系统构建，同时还要同步编写测试用例，获取用例成功与否以及用例覆盖率的相关报告，那么这些工具你肯定接触过不少：

* JUnit
* TestNG
* maven-surefire-plugin
* maven-surefire-report-plugin
* emma-maven-plugin
* jacoco-maven-plugin
* cobertura-maven-plugin
* maven-project-info-reports-plugin
* maven-site-plugin

是不是已经有些头晕了？没关系，我之前担任过很长时间的CI构建系统维护者，同时还是这里面几个Maven插件的Maintainer，我将尽最大努力帮你在最短的时间里理清他们的关系，帮助大家在实际项目中充分发挥这些工具的作用，提升产品质量。首先我们先大体分几个类别，让大家有个大概的印象。

* JUnit/TestNG是单元测试工具，可以帮你更方便的编写测试用例。
* maven-surefire-plugin是一个Maven插件，帮你在通过Maven构建项目的时候自动执行之前编写的测试用例。它的输出文件是txt或者xml格式的测试报告。
* maven-surefire-report-plugin是一个Maven插件，帮你将maven-surefire-plugin生成的测试报告转换为html格式，方便查看。
* emma-maven-plugin/jacoco-maven-plugin/cobertura-maven-plugin这些是帮助生成测试覆盖率报告的Maven插件，他们的输出文件也是html格式。
* maven-project-info-reports-plugin是一个Maven插件，他可以把maven-surefire-report-plugin/emma-maven-plugin/jacoco-maven-plugin/cobertura-maven-plugin这些插件生成的html格式文件进行汇总，帮助大家以更好的方式呈现。
* maven-site-plugin是一个Maven插件，帮你自动生成、部署、启动你的站点，站点里面可以有很多东西，其中最重要的部分就是你使用maven-project-info-reports-plugin生成的项目报告。

接下来我们根据之前的分类详细了解下他们：

## JUnit/TestNG

* JUnit: <http://junit.org/>
* TestNG: <https://testng.org/>

JUnit是老牌单元测试工具了，从3.X,4.X到最新的5.X版本，一直有广泛的群众基础。TestNG和JUnit一样，也是为了方便编写单元测试用例的Java类库，诞生之初就宣称是JUnit的下一代产品，事实也确实如此，在功能和易用性方面，TestNG都要强过于4.X及其更早版本的JUnit，网上有很多两者的对比文章，其中比较有名的一篇如下，感兴趣的话大家可以仔细阅读下：

* JUnit 4 Vs TestNG – Comparison: <https://mkyong.com/unittest/junit-4-vs-testng-comparison/>

JUnit面对市场份额被TestNG不断蚕食的情况，研发了更加强大的JUnit 5版本，补齐了能力差距，易用性方面也有了更大的提升。因此大家如果可以选择的话，我个人推荐大家直接使用JUnit 5，功能和易用性丝毫不逊色，还有广大的群众基础，出现问题也方便更快的搜索到解决方案。那你用JUnit或者TestNG工具写完了单元测试用例，怎么执行呢？你可以在各种IDE（比如Eclipse或者IntelliJ IDEA）使用对应的插件来帮助运行这些测试用例，当然你甚至都可以不用IDE，配置好依赖，直接命令行运行这些测试用例。

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170134052-10990627.png)

但是如何在Maven项目中自动执行这些步骤呢？这就是maven-surefire-plugin所做的事情了。

## maven-surefire-plugin

* maven-surefire-plugin: <http://maven.apache.org/surefire/maven-surefire-plugin/>

maven-surefire-plugin是Maven内嵌的一个插件，会帮助你在执行mvn test的时候自动执行用JUnit/TestNG编写的测试用例。

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170247317-1745411381.png)

除了将用例执行结果打印到屏幕上之外，还会在`target\surefire-reports`目录下生成两种形式的用例执行结果：

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170314097-523339706.png)

但是xml和txt格式的报告文件不太方便查看，要是能以html格式展示就好，所以你需要maven-surefire-report-plugin

## maven-surefire-report-plugin

* maven-surefire-report-plugin: <http://maven.apache.org/surefire/maven-surefire-report-plugin/>

maven-surefire-report-plugin的输入就是maven-surefire-plugin所产生的的xml后者txt格式的用例执行报告，输出就是html格式的用例执行报告。当你执行`surefire-report:report`时，你就会获得一个html格式的文件：

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170358803-2126291467.png)

内容如下：

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823171109951-322803827.png)

是不是感觉很丑？没有关系，我们可以利用maven-project-info-reports-plugin让他变得漂亮些。

## maven-site-plugin/maven-project-info-reports-plugin

* maven-site-plugin: <http://maven.apache.org/plugins/maven-site-plugin/index.html>
* maven-project-info-reports-plugin: <http://maven.apache.org/plugins/maven-project-info-reports-plugin/usage.html>

maven-site-plugin主要作用是帮你迅速生成(site:site)一个站点，并完成站点的部署(site:deploy)和启动(site:run)。当你执行site:site时，maven会同时调用maven-project-info-reports-plugin（所以如非定制要求，你可以不在pom.xml中配置maven-project-info-reports-plugin的依赖），生成一个项目框架结构，类似这种：

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170514421-278511798.png)

其实maven-project-info-reports-plugin还能根据你在pom.xml中配置的`<project><reporting><plugins>`配置的report插件，生成各种各样的项目报告，比如刚才说的maven-surefire-plugin生成的用例执行报告，和马上要说的用例覆盖报告。是不是感觉这里面展示的报告样式比直接打开surefire-report.html好多了？

![](https://img2020.cnblogs.com/blog/611264/202008/611264-20200823170537517-1970699000.png)

## [Emma/emma-maven-plugin][Jacoco/jacoco-maven-plugin][Cobertura/cobertura-maven-plugin]

* Emma：<http://emma.sourceforge.net/>
* emma-maven-plugin: <https://github.com/sonatype/emma-maven-plugin>
* JaCoCo/jacoco-maven-plugin: <https://www.eclemma.org/jacoco/index.html>
* Cobertura: <https://github.com/cobertura/cobertura>
* cobertura-maven-plugin: <http://www.mojohaus.org/cobertura-maven-plugin/>

这坨东西可以分为两类，一类就是检查Java用例覆盖情况的工具，另一类就是为了方便maven项目使用，开发出来的对应maven插件。其中Emma和emma-maven-plugin都很长时间没人维护了，所以我fork了这两个项目，并打算继续维护，目前为止已经解决了一些常见问题：

* Emma：<https://github.com/jiangxincode/Emma>
* emma-maven-plugin: <https://github.com/jiangxincode/emma-maven-plugin>

JaCoCo/jacoco-maven-plugin是同一个团队(EclEmma)在维护，EclEmma原本是一个Emma在Eclipse上的插件，但是在插件开发过程中越来越发现Emma在框架结构上的缺陷无法彻底解决，于是另起炉灶开发了JaCoCo，也就是说EclEmma现在除了名字外已经和Emma没有关系了。

三类用例覆盖工具中JaCoCo是最新的，也是对Java 8+新标准支持最好的，但是另外两个工具也有其特长，大家工作中根据实际情况选择即可。

## 远不止这些

前面介绍了测试用例执行情况和用例覆盖情况的报告，其实为了提升项目质量，可以提供很多种报告供大家使用，比如静态检查的findbugs、PMD等，我之前写过一个更加全面的工具汇总文章，大家可以参考：
<https://www.cnblogs.com/jiangxinnju/p/10010177.html>

理论说了一大堆，大家有没有一种冲动，把这些工具引用到自己的项目中去？这边有个例子供大家参考：

* 代码: <https://github.com/jiangxincode/ApkToolBoxGUI>
* 报告: <https://jiangxincode.github.io/ApkToolBoxGUI/>
