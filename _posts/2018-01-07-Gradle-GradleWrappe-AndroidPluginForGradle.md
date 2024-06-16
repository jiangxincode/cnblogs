---
title: "彻底搞懂Gradle_Gradle Wrapper与Android Plugin for Gradle的区别和联系"
categories:
  - Blog
tags:
  - Android
  - Gradle
  - Gradle Wrapper
  - Android Plugin for Gradle
---

对于初次学习Android应用开发的同学来讲，经常会被Gradle/Gradle Wrapper/Android Plugin for Gradle这三个概念搞蒙，他们的作用分别是什么？相互之间的关系是怎样的？希望本文可以给你答疑解惑。

首先用一段通俗易懂但是不是非常专业的话描述一下三者的概念、区别和联系。

* Gradle是个构建系统，能够简化你的编译、打包、测试过程。熟悉Java的同学，可以把Gradle类比成Maven。
* Gradle Wrapper的作用是简化Gradle本身的安装、部署。不同版本的项目可能需要不同版本的Gradle，手工部署的话比较麻烦，而且可能产生冲突，所以需要Gradle Wrapper帮你搞定这些事情。Gradle Wrapper是Gradle项目的一部分。
* Android Plugin for Gradle是一堆适合Android开发的Gradle插件的集合，主要由Google的Android团队开发，Gradle不是Android的专属构建系统，但是有了Android Plugin for Gradle的话，你会发现使用Gradle构建Android项目尤其的简单。

另外需要说明的一点是Gradle、Gradle Wrapper与Android Plugin for Gradle不一定要和Android Studio一起使用，你可以完全脱离Android Studio，使用三者独立进行Android项目的构建。下面是三者官方的指导文档（从地址可以看出Gradle Wrapper是Gradle项目的一部分）：

* Gradle: <https://docs.gradle.org/current/userguide/userguide_single.html>
* Gradle Wrapper: <https://docs.gradle.org/current/userguide/gradle_wrapper.html>
* Android Plugin for Gradle: <https://developer.android.com/studio/build/index.html>

为了加深大家对于三者的理解，我们聊一聊在实际的项目构建中，这三者的关系，之前已经说过三者可以脱离Android Studio独立使用，但是这种情况在实际开发场景中并不多见，所以本文还是使用Android Studio作为开发工具进行介绍。当我们新建一个Android项目时，会出现类似于下图所示的目录结构：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/20180107182239596.png)

可以看到一个gradle/wrapper目录，其中有两个文件：gradle-wrapper.jar/gradle-wrapper.properties，gradle-wrapper.jar是Gradle Wrapper的主体功能包。在Android Studio安装过程中产生gradle-wrapper.jar（如果默认安装的话会在`C:\Program Files\Android\Android Studio\plugins\android\lib\templates\gradle\wrapper\gradle\wrapper\gradle-wrapper.jar`）。然后每次新建项目，会将gradle-wrapper.jar拷贝到你的项目的gradle/wrapper目录中。gradle-wrapper.properties文件主要指定了该项目需要什么版本的Gradle，从哪里下载该版本的Gradle，下载下来放到哪里，如下图所示：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/20180107182326299.png)

其中GRADLE_USER_HOME一般指`~/.gradle`，从图示项目中可以知道我要使用gradle-4.1版本，从`https://services.gradle.org/distributions/gradle-4.1-all.zip`下载，下载到本地的`~/.gradle/wrapper/dists`目录。

有时由于网络问题，可能无法正常下载对应的gradle版本，导致Sync Project With Gradle Files失败，此时可以在AS报错后在`~/.gradle/wrapper/dists`目录中找到gradle版本对应的那个目录，比如`~/.gradle/wrapper/dists/gradle-4.1-all/cdund22i8guosqylfo49op4dv`，然后从网上下载gradle-4.1-all.zip并将其放到该目录中，重新Sync Project With Gradle Files即可。

那是不是各个项目的Gradle都要通过Gradle Wrapper下载，能不能所有的项目共用一个Gradle？这样理论上是可以的，但是由于Gradle本身不一定保持完全的兼容性，所以新老项目共用一个Gradle有时可能会遇到意想不到的问题。指定对应版本的Gradle，而不通过Gradle Wrapper下载的设置方式是勾选如下图中的`Use local gradle distribution`，同时指定Gradle home：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/20180107184405143.png)

Gradle对应版本下载完成之后，Gradle Wrapper的使命基本完成了，Gradle会读取build.gradle文件，该文件中指定了该项目需要的Android Plugin for Gradle版本是什么，从哪里下载该版本的Android Plugin for Gradle。如下图所示：

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/20180107184419674.png)

从图示项目中可以知道我们要使用3.0.1版本，从google和jcenter处下载，那么下载到我们本地的哪里呢？它会下载到`~\.gradle\caches\modules-2\files-2.1\com.android.tools.build`中。有时候大家网络装填不好，选择下图中的`Offline work`时可能出现"No cached version of com.android.tools.build:gradle:xxx available for offline mode"问题，此时你只要将对应版本的Android Plugin for Gradle下载到本地的`C:\Program Files\Android\Android Studio\gradle\m2repository\com\android\tools\build`中即可。

好了，三者的关系从样例项目中理清楚了。如果大家有什么疑问可以通过Github Issues给我留言。

本文首发于: <https://jiangxincode.github.io/blogs/blog/Gradle-GradleWrappe-AndroidPluginForGradle/>
