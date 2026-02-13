---
title: "Jetpack/Compose/KMP"
categories:
  - android
tags:
  - Jetpack
  - Compose
  - KMP
toc: true
---

## 概念

### **Flutter**

> Flutter 是一个开源框架，用于从单一代码库构建美观的、原生编译的多平台应用程序。

> Flutter是基于Dart的。

* Flutter: <https://flutter.dev/>

### Kotlin Multiplatform(KMP)

> `Kotlin Multiplatform`如名字所示，可以创建跨平台的应用程序，以此开发的应用程序可以在 iOS、Android、macOS、Windows、Linux 等平台上运行。

* Kotlin Multiplatform：<https://www.jetbrains.com/kotlin-multiplatform/>

### Compose Multiplatform

> `Compose Multiplatform`是一套声明式 UI 框架，可以帮助让 Android、iOS、桌面和Web开发共享 UI。将`Compose Multiplatform`集成到`Kotlin Multiplatform`项目中，可以更快地交付应用程序和功能，而无需维护多个 UI 实现。

* Compose Multiplatform：<https://www.jetbrains.com/zh-cn/compose-multiplatform/>

`Compose Multiplatform`由 `Kotlin Multiplatform` 和 `Jetpack Compose` 提供支持。由 JetBrains 开发。

有时你可能还会听到`Kotlin Multiplatform Mobile(KMM)`，不过为了避免引起混乱已经弃用了。详见：

* Update on the Name of Kotlin Multiplatform：<https://blog.jetbrains.com/kotlin/2023/07/update-on-the-name-of-kotlin-multiplatform/>

### Android Jetpack

> Jetpack 是一套库，旨在帮助开发者遵循最佳实践，减少样板代码，并编写在各个 Android 版本和设备上始终如一运行的代码，使开发者能够专注于他们关心的代码。

* Android Jetpack(AndroidX)：<https://developer.android.com/jetpack>

* Explore the Jetpack libraries by type：<https://developer.android.com/jetpack/androidx/explorer>

> Android Jetpack是既支持Kotlin也支持Java。

有一部分Android Jetpack库已经支持在跨平台（Android/iOS）支持，详见：

* Multiplatform Jetpack libraries：<https://developer.android.google.cn/kotlin/multiplatform>

### Native Android UI

现在有两种native Android UI：`View`和`Jetpack Compose`。

#### 基于View的工作流（不推荐）

<https://developer.android.com/develop/ui/views/layout/declaring-layout>

#### Jetpack Compose（推荐）

> Jetpack Compose是Android Jetpack的一个子项目。

<https://developer.android.com/develop/ui/compose/documentation>

## 参考

* Jetpack Compose 和 Compose Multiplatform 还有 KMP 的关系：<https://juejin.cn/post/7462776363734564916>
* Flutter 与 Compose 应该怎么选择？它们冲突吗？<https://zhuanlan.zhihu.com/p/357092577>
