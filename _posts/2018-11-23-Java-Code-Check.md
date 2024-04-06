---
title: "Java代码质量度量工具大阅兵"
categories:
  - Blog
tags:
  - Java
  - Code Check
toc: true
---

以下大部分工具使用样例请访问: <https://github.com/jiangxincode/ApkToolBoxGUI>

## FindBugs

    FindBugs, a program which uses static analysis to look for bugs in Java code.  It is free software, distributed under the terms of the Lesser GNU Public License. The name FindBugs™ and the FindBugs logo are trademarked by The University of Maryland. FindBugs has been downloaded more than a million times.

* FindBugs：<http://findbugs.sourceforge.net/>
* FindBugs Bug Descriptions：<http://findbugs.sourceforge.net/bugDescriptions.html>
* FindBugs详解: <http://www.cnblogs.com/jiangxinnju/p/6582404.html>
* FindBugs Maven Plugin(for Maven 1.x): <http://maven-plugins.sourceforge.net/maven-findbugs-plugin/>
* FindBugs Maven Plugin(for Maven 2.0+): <https://gleclaire.github.io/findbugs-maven-plugin/>
* Jenkins+findbugs对java代码进行静态代码分析: <https://blog.csdn.net/fighterandknight/article/details/51424257>

## spotbugs

    SpotBugs is a fork of FindBugs (which is now an abandoned project), carrying on from the point where it left off with support of its community. Please check the official manual for details.

* spotbugs: <https://spotbugs.github.io/>

## CheckStyle

    Checkstyle is a development tool to help programmers write Java code that adheres to a coding standard. It automates the process of checking Java code to spare humans of this boring (but important) task. This makes it ideal for projects that want to enforce a coding standard.

* CheckStyle：<http://checkstyle.sourceforge.net/>
* Eclipse Checkstyle Plug-in: <https://sourceforge.net/projects/eclipse-cs/>
* Checkclipse: <https://sourceforge.net/projects/checkclipse/>
* CheckStyle-IDEA: <http://plugins.jetbrains.com/plugin/1065-checkstyle-idea>
* maven-checkstyle-plugin: <http://maven.apache.org/plugins/maven-checkstyle-plugin/>

## PMD

    PMD is a source code analyzer. It finds common programming flaws like unused variables, empty catch blocks, unnecessary object creation, and so forth. It supports Java, JavaScript, Salesforce.com Apex and Visualforce, PLSQL, Apache Velocity, XML, XSL.
    Additionally it includes CPD, the copy-paste-detector. CPD finds duplicated code in Java, C, C++, C#, Groovy, PHP, Ruby, Fortran, JavaScript, PLSQL, Apache Velocity, Scala, Objective C, Matlab, Python, Go, Swift and Salesforce.com Apex and Visualforce.

* PMD(various plugin addresses included)：<https://pmd.github.io/>
* PMD Rules: <https://pmd.github.io/pmd-5.3.6/pmd-java/rules/index.html>
* maven-pmd-plugin: <http://maven.apache.org/plugins/maven-pmd-plugin/>

## p3c

    Alibaba Java Coding Guidelines pmd implements and IDE plugin

* p3c: <https://github.com/alibaba/p3c>

## JDeodorant

    JDeodorant is an Eclipse plug-in that detects design problems in Java software, known as code smells, and recommends appropriate refactorings to resolve them.

* JDeodorant: <https://github.com/tsantalis/JDeodorant>

## Jdepend(Not Recommend)

    JDepend traverses Java class file directories and generates design quality metrics for each Java package. JDepend allows you to automatically measure the quality of a design in terms of its extensibility, reusability, and maintainability to manage package dependencies effectively.
    Jdepend很久没有维护了，后续不建议使用

* Jdepend：<http://www.clarkware.com/software/JDepend.html>
* JDepend4Eclipse：<http://marketplace.eclipse.org/content/jdepend4eclipse>
* JDepend Maven Plugin（这个插件我也在维护）: <https://github.com/jiangxincode/jdepend-maven-plugin>

## Metrics

* Eclipse Metrics plugin: <https://sourceforge.net/projects/metrics/>
* Eclipse Metrics plugin continued: <https://sourceforge.net/projects/metrics2/>
* Metrics 3 - Eclipse Metrics Plugin Continued 'Again': <https://github.com/qxo/eclipse-metrics-plugin>

## Emma(Not Recommend)

    a free Java code coverage tool
    Emma很久没有维护了，不支持Java 8+语法，后续不建议使用

* Emma：<http://emma.sourceforge.net/>
* 我做了一些优化和升级：<https://github.com/jiangxincode/Emma>

* eclemma(Emma Eclipse Plugin, 开始基于Emma后来基于JaCoCo)：<http://www.eclemma.org/>

* emma-maven-plugin(我开发的插件，欢迎大家使用，多提issues): <https://github.com/jiangxincode/emma-maven-plugin>

## JaCoco(Recommend)

    JaCoCo is a free code coverage library for Java, which has been created by the EclEmma team based on the lessons learned from using and integration existing libraries for many years.

* JaCoCo: <https://www.eclemma.org/jacoco/index.html>
* Getting “Skipping JaCoCo execution due to missing execution data file” upon executing JaCoCo? <https://stackoverflow.com/questions/18107375/getting-skipping-jacoco-execution-due-to-missing-execution-data-file-upon-exec>

## Cobertura(Not Recommend)

    Cobertura is a free Java code coverage reporting tool.

* Cobertura: <https://github.com/cobertura/cobertura>
* eCobertura(Cobertura Eclipse Plugin)：<http://ecobertura.johoop.de/>
* cobertura-maven-plugin: <http://www.mojohaus.org/cobertura-maven-plugin/>
* 学习Maven之Cobertura Maven Plugin: <https://www.cnblogs.com/qyf404/archive/2015/12/12/5040593.html>

## Coverlipse(Not Recommend)

    Coverlipse is an Eclipse plugin that visualizes the code coverage of JUnit Tests. It is unique for it integrates seamlessly in Eclipse. The coverage results are given directly after a JUnit run. This makes it the perfect tool for developers to recognize their tests fullfil their task. 

* Coverlipse: <http://coverlipse.sourceforge.net/>

## JavaNCSS(Not Recommend)

    JavaNCSS - A Source Measurement Suite for Java. 
    JavaNCSS很久没有维护了，不支持Java 8+语法，后续不建议使用

* JavaNCSS: <http://www.kclee.de/clemens/java/javancss/>
* 当前有些源码分支还在开发，但完成度不高：<https://github.com/codehaus/javancss>
* javancss-maven-plugin: <http://www.mojohaus.org/javancss-maven-plugin/usage.html>

## Simian

    Simian (Similarity Analyser) identifies duplication in Java, C#, C, C++, COBOL, Ruby, JSP, ASP, HTML, XML, Visual Basic, Groovy source code and even plain text files. In fact, simian can be used on any human readable files such as ini files, deployment descriptors, you name it.

* Simian：<http://www.harukizaemon.com/simian/>
* simian-maven-plugin(我开发的插件，欢迎大家使用，多提issues): <https://github.com/jiangxincode/simian-maven-plugin>

注：If you like simian-maven-plugin, you can vote for my answer on <http://stackoverflow.com/questions/1077700/how-do-you-use-the-maven-simian-plugin-in-maven2>

## SourceMonitor

    SourceMonitor lets you see inside your software source code to find out how much code you have and to identify the relative complexity of your modules. For example, you can use SourceMonitor to identify the code that is most likely to contain defects and thus warrants formal review.

* SourceMonitor: <https://github.com/SourceMonitor/SM-Info>
* 代码度量工具——SourceMonitor的学习和使用：<http://www.cnblogs.com/bangerlee/archive/2011/09/18/2178172.html>

## iPlasma

    iPlasma is an integrated environment for quality analysis of object-oriented software systems that includes support for all the necessary phases of analysis: from model extraction (including scalable parsing for C++ and Java) up to high-level metrics-based analysis, or detection of code duplication. iPlasma has three major advantages: extensibility of supported analysis, integration with further analysis tools and scalability, as it was used in the past to analyse large-scale projects in the size of millions of code lines (e.g. Eclipse and Mozilla).

* <http://loose.cs.upt.ro/index.php?n=Main.IPlasma>

## inFusion

    Whether you own, are responsible for, or are acquiring software projects in C/C++ or Java, inFusion puts you in full control of architecture and design quality. inFusion makes quality assurance of multi-million LOC systems not merely practical, but effective, successfully handling both object oriented and procedural style code.

* <http://www.intooitus.com/products/infusion>(deprecated)
* InFusion错误类型分析：<http://www.cnblogs.com/Leo_wl/p/3493231.html>
* 软件设计度量工具inFusion(一)：inFusion的基本概念: <http://blog.csdn.net/aitangyong/article/details/50206419>
* 软件设计度量工具inFusion(二)：看懂inFusion度量结果: <http://blog.csdn.net/aitangyong/article/details/50250967>

## structure101

* <https://structure101.com/>
* 软件设计度量工具structure101学习(一)：structure101试用版licence的获取以及众多的structure101系列工具: <https://blog.csdn.net/aitangyong/article/details/50054403>
* 软件设计度量工具structure101学习(二)：Call Graph、Class Hierarchy、Collaboration、Composition视图: <https://blog.csdn.net/aitangyong/article/details/50054671>
* 软件设计度量工具structure101学习(三)：Slices视图: <https://blog.csdn.net/aitangyong/article/details/50060703>
* 软件设计度量工具structure101学习(三.1)：解决slices视图遗留问题: <https://blog.csdn.net/aitangyong/article/details/50081885>
* 软件设计度量工具structure101学习(四)：complexity的使用与计: <https://blog.csdn.net/aitangyong/article/details/50084357>
* 软件设计度量工具structure101学习(五)：repository的使用: <https://blog.csdn.net/aitangyong/article/details/50085403>
* 软件设计度量工具structure101学习(六)：Project Properties: <https://blog.csdn.net/aitangyong/article/details/50110605>

## coverity

    Coverity® static application security testing (SAST) helps you build software that’s more secure, higher-quality, and compliant with standards.

* <http://www.coverity.com/>
* COVERITY CI: <https://scan.coverity.com/>

## pinpoint

    静态分析，源代码审计

* Sourcebrella Pinpoint: <https://www.sourcebrella.com/pinpoint/>

## Infer

    Infer is a static analysis tool - if you give Infer some Java or C/C++/Objective-C code it produces a list of potential bugs. Anyone can use Infer to intercept critical bugs before they have shipped to users, and help prevent crashes or poor performance.

* <https://fbinfer.com/>
* infer-maven-plugin（简单封装，意义不大，可以直接使用其它方式进行CI集成）: <https://github.com/anthemengineering/infer-maven-plugin>

## FireLine

* <http://magic.360.cn/>
* fireline-maven-plugin(我开发的插件，欢迎大家使用，多提issues): <https://github.com/jiangxincode/fireline-maven-plugin>

## cloc

    cloc counts blank lines, comment lines, and physical lines of source code in many programming languages.

* cloc: <https://github.com/AlDanial/cloc>

## 额外阅读

* 浅淡静态代码分析工具：<http://www.cnblogs.com/hyddd/archive/2008/12/16/1356310.html>
* 七款代码味道识别工具【简介】：<http://blog.csdn.net/lovelion/article/details/18467149>
