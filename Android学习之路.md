# Andriod学习之路

* 开发者网站中文: <https://developer.android.google.cn>
* 开发者网站英文: <https://developer.android.com>

* Developer guide: <https://developer.android.com/guide>
  * Permissions: <https://developer.android.com/training/permissions/requesting>
  * Android 权限的一些细节: <http://blog.csdn.net/u013553529/article/details/53167072>
  * Data and file storage overview: <https://developer.android.com/training/data-storage>
  * Autofill framework: <https://developer.android.com/guide/topics/text/autofill>

* Managing the System UI: <https://developer.android.com/training/system-ui/index.html>
* Create and manage notification channels: <https://developer.android.com/develop/ui/views/notifications/channels>
* Support different screen sizes: <https://developer.android.com/guide/topics/large-screens/support-different-screen-sizes>
* Enhance graphics with wide color content: <https://developer.android.com/training/wide-color-gamut>

* NDK: <https://developer.android.com/ndk/>

* Intent: <https://developer.android.com/reference/android/content/Intent.html>
* PendingIntent: <https://developer.android.com/reference/android/app/PendingIntent>
* Settings.Global: <https://developer.android.com/reference/android/provider/Settings.Global>

* Android开发者预览版: <https://developer.android.com/preview/>

* Android Jetpack: <https://developer.android.com/jetpack>
* AndroidX 概览: <https://developer.android.com/jetpack/androidx>

* App Shortcuts: <https://developer.android.com/guide/topics/ui/shortcuts>
* SDK版本关系: <https://developer.android.com/guide/topics/manifest/uses-sdk-element.html>
* 支持库: <https://developer.android.com/topic/libraries/support-library/index>
* uses-library: <https://developer.android.com/guide/topics/manifest/uses-library-element.html>

* Android Studio: <http://www.android-studio.org/>
* Xamarin: <https://www.xamarin.com/>
* Android Support Overview: <http://www.jetbrains.com/help/idea/android-support-overview.html>

## AOSP

* AOSP项目官网中文：<https://source.android.google.cn>
* AOSP项目官网英文：<https://source.android.com>

### AOSP源码在线查看

* Android Code Search: <https://cs.android.com/>
* AOSPXRef: <http://aospxref.com/>
* androidxref: <http://androidxref.com/>
* Android Cross Reference: <http://aosp.opersys.com/>
* Android OS: <https://www.androidos.net.cn/sourcecode>
* Git repositories on android: <https://android.googlesource.com/>

### AOSP构建

* Building Android: <https://source.android.com/setup/build/building>
* Codenames, Tags, and Build Numbers: <https://source.android.com/setup/start/build-numbers>
* 将AOSP源码导入到Android Studio进行查看: <https://www.cnblogs.com/jiangxinnju/p/14426645.html>
* Android构建系统: <https://www.cnblogs.com/jiangxinnju/p/14402000.html>
* Android soong build系统介绍: <https://www.jianshu.com/p/80013a768a45>
* Repo实践指南: <https://www.cnblogs.com/jiangxinnju/p/14274982.html>

* ~~使用 Jack 编译 (AOSP 6.0 - 8.1): <https://source.android.google.cn/docs/setup/build/jack>~~
* ~~Android 新一代编译 toolchain Jack & Jill 简介: <https://yq.aliyun.com/articles/40811>~~
* ~~Google 又弃坑了，Jack+Jill vs. javac+dx: <https://zhuanlan.zhihu.com/p/25814519>~~

### 系统架构

* 系统启动流程（init进程、Zygote进程、SystemServer）：<https://juejin.cn/post/6962038395505737765>
* android关机流程 安卓关机流程: <https://blog.51cto.com/u_16099295/6984333>
* Android BOOTCLASSPATH详解: <https://blog.csdn.net/qqxiaoqiang1573/article/details/78715846>

### WMS

* WMS转屏流程: <https://www.jianshu.com/p/65bf626c66d5>
* Android WMS动画系统初探(一): <https://juejin.cn/post/7021082548985921567>
* WindowManagerService理解与深入（Android Q）: <https://blog.csdn.net/xxzxxzdlut/article/details/103205047>
* android中Activity中的WindowManager与Window: <https://www.cnblogs.com/meizixiong/p/3546397.html>
* 浅析onWindowsFocusChanged()方法: <https://blog.csdn.net/a282255307/article/details/74906518>
* Window.setFlags 各种Flag笔记: <https://blog.csdn.net/sdjianfei/article/details/53505874>
* Activity的创建（从Activity的角度理解IWindowSession）: <https://blog.csdn.net/lu1024188315/article/details/74911179>
* Android多点触控问题解决(windowEnableSplitTouch, splitMotionEvents): <https://blog.csdn.net/yztbydh/article/details/82734884>

### 手势导航相关

* Ensure compatibility with gesture navigation: <https://developer.android.com/develop/ui/views/touch-and-input/gestures/gesturenav>
* 深入分析 Android 系统返回手势的实现原理: <https://juejin.cn/post/7103503592119599117>
* Android 13 返回导航大变更：返回键彻底废弃 + 可预见型返回手势: <https://juejin.cn/post/7105645114760331300>
* Android 14 之返回界面升级：预览目标界面 + 全新返回箭头：<https://juejin.cn/post/7241125859729260600>
* 开启全面屏体验 | 手势导航 (一): <https://cloud.tencent.com/developer/article/1542904>
* 处理视觉冲突 | 手势导航 (二): <https://cloud.tencent.com/developer/article/1545958>
* 如何处理手势冲突 | 手势导航连载 (三): <https://cloud.tencent.com/developer/article/1555442>
* 沉浸模式 | 手势导航连载 (四) :<https://cloud.tencent.com/developer/article/1563846>

### Input相关

* 图解 Android 事件分发机制: <https://www.jianshu.com/p/e99b5e8bd67b>
* requestDisallowInterceptTouchEvent() 阻止父层的View截获touch事件(事件处理机制): <https://blog.csdn.net/cl18652469346/article/details/53184508>
* View·InputEvent事件投递源码分析: <https://www.jianshu.com/p/b7f33f46d33c>
* Android 输入系统【1】通过 IMS 的创建理解 Android 的输入流程: <https://mp.weixin.qq.com/s/Gv6bATNKfC8FyIs-b_0DoA>
* input子系统详解: <https://www.cnblogs.com/zhaobinyouth/p/6257662.html>
* 图解Android - Android GUI 系统 (5) - Android的Event Input System: <https://www.cnblogs.com/samchen2009/p/3368158.html>
* Android input专题: <https://www.jianshu.com/c/51d936cc1714>
* Android InputDispatch事件派发-＞选择目标窗口: <https://blog.csdn.net/woai110120130/article/details/112424370>
* 10.12 android输入系统_InputStage理论: <https://www.cnblogs.com/liusiluandzhangkun/p/9173373.html>
* Android Input 4: <https://www.jianshu.com/p/06fcccb2bb16>
* kOS(13)：inputflinger—InputReader线程: <https://zhuanlan.zhihu.com/p/196635542>
* Android Input (4) -- inputDispatcher到ViewRootImpl: <https://blog.csdn.net/wd229047557/article/details/100766728>
* 【Android休眠】之Android对PowerKey事件的处理(2)EventHub: <https://blog.csdn.net/u013686019/article/details/53691888>
* Android_input系统分析EventHub::getevents: <https://blog.csdn.net/weixin_38140931/article/details/100772033>
* Linux/Android——Input系统之InputReader (七): <https://blog.csdn.net/jscese/article/details/42739197>
* Android触摸事件的传递（四-1）--输入系统-InputReader: <https://www.jianshu.com/p/34f5c7d55337>
* Input源码解读——从"Show tabs"开始: <https://www.cnblogs.com/jiangxinnju/p/17035554.html>
* input-samples: <https://github.com/android/input-samples>

### Accessibility

* Android AccessibilityService机制源码解析: <https://juejin.cn/post/6844903623013597198>

### 电源管理

* Android电源键亮灭屏流程: <https://blog.csdn.net/feelabclihu/article/details/115410675>
* Optimize for Doze and App Standby: <https://developer.android.com/training/monitoring-device-state/doze-standby>
* App Standby Buckets: <https://developer.android.com/topic/performance/appstandby>
* Doze模式简介: <https://blog.csdn.net/thh159/article/details/113839799>
* Android中的Doze模式: <https://www.jianshu.com/p/d62d58d6ba5a>
* Android 8.1 Doze模式分析（一）: <https://blog.csdn.net/liu362732346/article/details/85290519>
* Android 11(R) Power HAL AIDL简析 -- 基本接口: <https://www.cnblogs.com/roger-yu/p/15189708.html>
* AOD 息屏是什么？背后技术原理是什么？<https://www.zhihu.com/question/332932501>
* AOD相关机制: <https://blog.csdn.net/cr459464757/article/details/108054816>

### 生物识别

* Android8.0 Fingerprint指纹启动流程详细分析: <https://blog.csdn.net/weixin_43943188/article/details/88321101>
* FingerPrintAuth: <https://github.com/hetaoyuan-android/FingerPrintAuth/blob/9d9b82ea2ab6b717dec1f0f1d11e0e7d2251f586/app/src/main/java/com/feelschaotic/MainActivity.java>

### Battery相关

* Android 8.1 Battery系列(一) BatteryService分析: <https://blog.csdn.net/FightFightFight/article/details/82353373>
* Android 8.1 Battery系列(二) BatteryStatsService分析: <https://blog.csdn.net/FightFightFight/article/details/82384336>
* Android 8.1 Battery系列(三) PowerProfile和power_profile.xml: <https://blog.csdn.net/FightFightFight/article/details/82428483>
* [Android Framework] 8.1 Battery系列(四) 电量还需多长时间充满时间计算: <https://blog.csdn.net/FightFightFight/article/details/82467246>
* [Android Framework] 8.1 Battery系列(五) 电量预计可用多长时间计算: <https://blog.csdn.net/FightFightFight/article/details/82628707>
* [Android Framework] 8.1 Battery系列(六) 上次充满电计算: <https://blog.csdn.net/FightFightFight/article/details/82629645>
* Android 8.1 Battery系列(七) BatteryStatsHelper类和耗电量统计: <https://blog.csdn.net/FightFightFight/article/details/82694381>

* 通过 Battery Historian 工具分析 Android APP 耗电情况: <https://www.cnblogs.com/huansky/p/14545770.html>
* AndroidO Battery saver省电助手实现原理: <https://blog.csdn.net/yun_hen/article/details/78143442>

* battery-historian: <https://github.com/google/battery-historian>

### Alarm

* How to read "adb shell dumpsys alarm" output: <https://stackoverflow.com/questions/28742884/how-to-read-adb-shell-dumpsys-alarm-output>
* android后台执行定时任务（保活）&&使用AlarmManager的各种坑: <https://blog.csdn.net/u013095264/article/details/91880916>
* Schedule alarms: <https://developer.android.google.cn/develop/background-work/services/alarms/schedule?hl=en>

### 剪贴板框架

* 复制和粘贴: <https://developer.android.com/develop/ui/views/touch-and-input/copy-paste>

### 输入法与输入法框架

* 关于Android外设键盘导致系统输入法隐藏的解决方案: <https://blog.csdn.net/xiaolei10086/article/details/41212845>

### USB

* USB 主机和配件概览: <https://developer.android.google.cn/develop/connectivity/usb>
* Android 开放配件 (AOA): <https://source.android.google.cn/docs/core/interaction/accessories/protocol?hl=zh-cn>
* Android Open Accessory 协议分析与开发: <https://www.hackermi.com/2015-04/aoa-analyse/>
* Android下USB Accessory的实现分析: <https://blog.csdn.net/yingzhao80/article/details/45511351>

* Android 对 USB 音频类的支持: <https://source.android.com/docs/core/audio/usb?hl=zh-cn#androidSupport>
* How to enable USB "Audio Source" option on Android 9+? <https://android.stackexchange.com/questions/225334/how-to-enable-usb-audio-source-option-on-android-9>

### Binder

* 架构概览: <https://source.android.google.cn/docs/core/architecture>
* 适用于 HAL 的 AIDL: <https://source.android.google.cn/docs/core/architecture/aidl/aidl-hals>
* Android Binder设计与实现 - 设计篇: <http://blog.csdn.net/universus/article/details/6211589>
* Here comes Treble: A modular base for Android: <https://android-developers.googleblog.com/2017/05/here-comes-treble-modular-base-for.html>
* Service/Binder/Messenger/AIDL: <https://developer.android.com/guide/components/services>+《Android开发艺术探索》第2章、第9章
* 深入Android HAL binder: <https://sniffer.site/2018/06/06/%E6%B7%B1%E5%85%A5android-hal-binder/>
* HwBinder入门篇-Android10.0 HwBinder通信原理(一): <https://blog.csdn.net/yiranfeng/article/details/107751217>
* HIDL详解-Android10.0 HwBinder通信原理(二): <https://blog.csdn.net/yiranfeng/article/details/107824605>
* BpHwBinder: <https://android.googlesource.com/platform/system/libhwbinder/+/062365942b0fd54cc5e6af46e12a5f90eeb5d4a1/BpHwBinder.cpp>
* Android源码的Binder权限是如何控制？<https://www.zhihu.com/question/41003297/answer/89328987>
* Android Binder异常传递流程分析: <https://blog.csdn.net/zhangjg_blog/article/details/83420068>
* HIDL 简单介绍: <https://blog.csdn.net/lei7143/article/details/80931412>
* 使用Android的HIDL+AIDL方式编写从HAL层到APP层的程序: <http://www.max-shu.com/blog/?p=1075>
* AIDL interface between Java and C++: <https://stackoverflow.com/questions/65284392/aidl-interface-between-java-and-c>

### Service

* About Background work: <https://developer.android.com/develop/background-work>
* 深入源码解析Android中的Handler,Message,MessageQueue,Looper: <http://blog.csdn.net/iispring/article/details/47180325>
* Android使用JobService实现后台服务: <https://www.jianshu.com/p/aba38b9e11e7>
* Android 中设置线程优先级的正确方式（2种方法）: <https://blog.csdn.net/u011578734/article/details/110549238>
* 微信团队原创分享：Android版微信后台保活实战分享(进程保活篇): <http://www.52im.net/thread-210-1-1.html>
* Android单应用开多进程与单进程跑多应用: <https://blog.csdn.net/ragnaro/article/details/51569096>
* Android中使用ContentProvider进行跨进程方法调用: <https://blog.csdn.net/cnzx219/article/details/46645519>
* Android 进程管理篇（五）-调度策略与优先级: <https://www.jianshu.com/p/1d2f6a5bbe76>
* Android性能优化之实现拥有Looper的线程--HandlerThread: <https://blog.csdn.net/chenliguan/article/details/54585646>

### 稳定性

* AtomicFile: <https://developer.android.com/reference/android/util/AtomicFile>
* ResilientAtomicFile: <https://android.googlesource.com/platform/frameworks/base/+/master/services/core/java/com/android/server/pm/ResilientAtomicFile.java>
* Linux sync详解: <https://www.python100.com/html/120303.html>
* ANDROID 设备写入文件，立即断电重启后，文件丢失，数据没有保存问题: <https://blog.csdn.net/qijingwang/article/details/125381781>
* 系统反复重启--RescueParty触发recovery记录: <https://blog.csdn.net/xiaoqiaoq0/article/details/107237769>
* android-O RescueParty 介紹: <https://www.twblogs.net/a/5b829c732b717766a1e91145>
* Rescue Party: <https://source.android.google.cn/docs/core/tests/debug/rescue-party?hl=en>
* 理解Native Crash处理流程: <https://blog.csdn.net/u010144805/article/details/78560529>
* ANR Broadcast TimeOut 超时判断: <https://blog.csdn.net/qq_23452385/article/details/89784523>
* Android ANR：原理分析及解决办法: <https://www.jianshu.com/p/388166988cef>

### 性能分析

* Overview of system tracing: <https://developer.android.com/topic/performance/tracing>
* Inspect CPU activity with CPU Profiler: <https://developer.android.com/studio/profile/cpu-profiler>
* Simpleperf: <https://android.googlesource.com/platform/system/extras/+/master/simpleperf/doc/README.md>
* Android Systrace 基础知识: <https://www.androidperformance.com/2019/05/28/Android-Systrace-About/>
* systrace.py环境配置: <https://blog.csdn.net/zc37093/article/details/105415843>

* Perfetto: <https://perfetto.dev/>
* PerfettoUI: <https://ui.perfetto.dev/#!/>

* TraceView(已弃用): <https://developer.android.com/studio/profile/traceview>
* Android性能优化—TraceView的使用: <https://www.jianshu.com/p/7e9ca2c73c97>

* PerfDog性能狗: <https://perfdog.qq.com/>

* Eight Ways Your Android App Can Leak Memory: <https://blog.nimbledroid.com/2016/05/23/memory-leaks.html>
* Eight Ways Your Android App Can STOP Leaking Memory: <https://blog.nimbledroid.com/2016/09/06/stop-memory-leaks.html>
* Android性能优化: <http://liuwangshu.cn/tags/Android%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96/>
* 使用meminfo分析Android单个进程内存信息: <https://my.oschina.net/shaorongjie/blog/128442>
* How do I discover memory usage of my application in Android? <https://stackoverflow.com/questions/2298208/how-do-i-discover-memory-usage-of-my-application-in-android>

* Android adb bugreport工具分析和使用: <https://blog.csdn.net/createchance/article/details/51954142>
* ChkBugReport: <https://github.com/sonyxperiadev/ChkBugReport>
* loganalysis(Android日志分析工具): <https://cs.android.com/android/platform/superproject/+/refs/heads/master:tools/loganalysis/src/com/android/loganalysis/LogAnalyzer.java>
* Android单条日志太长导致被截断的问题分析和解决: <https://blog.csdn.net/realDonaldTrump/article/details/128468204>

* 性能优化工具（十）- Android内存分析命令: <https://www.jianshu.com/p/9edfe9d5eb34>
* Android内存优化（使用SparseArray和ArrayMap取代HashMap）:<https://www.cnblogs.com/yjbjingcha/p/7074266.html>
* Android--＞iostat(显示CPU和IO系统负载情况): <https://blog.csdn.net/angcyo/article/details/51104326>
* 内存耗用：VSS/RSS/PSS/USS: <https://blog.csdn.net/adaptiver/article/details/7084364>

### 动效

* 各种转场动画: <https://github.com/lgvalle/Material-Animations>
* Android:去掉系统自带的Activity跳转动画，跳转无动画,返回无动画: <http://blog.csdn.net/qq_24697659/article/details/49660275>
* Android 属性动画 常用方法 与 插值器 Interpolator: <https://blog.csdn.net/qq_30889373/article/details/78881140>
* Property Animation框架详解(一): <https://blog.csdn.net/u012422440/article/details/51352852>
* Android动画之Interpolator(插值器): <https://blog.csdn.net/pzm1993/article/details/77926373>
* Android 路径绘制艺术——贝塞尔曲线: <https://www.jianshu.com/p/12fcc3fedbbc>
* 三阶贝塞尔曲线Interpolator的应用: <https://blog.csdn.net/xsl_bj/article/details/47722489>
* 在线演示: <https://cubic-bezier.com/><http://inloop.github.io/interpolator/>
* Android颜色透明度百分比和十六进制对应关系: <https://blog.csdn.net/zhangcanyan/article/details/78400179>
* Android 关于Path的FillType: <https://www.jianshu.com/p/ce808a9e7e38>
* Android中使用SVG实现炫酷动画效果: <https://blog.csdn.net/SilenceOO/article/details/78629028>
* SVG 的 PathData 在 Android 中的使用: <https://blog.csdn.net/zwlove5280/article/details/73196543>
* Android矢量图(一)--VectorDrawable基础: <https://www.jianshu.com/p/0972a0d290e9>
* 在 Android 开发中使用 SVG: <https://enzowyf.github.io/svg_android.html>
* 手把手教学， android 使用 SVG: <https://www.jianshu.com/p/5c81970ddf33>

### 控件

* Caching Bitmaps: <https://developer.android.com/topic/performance/graphics/cache-bitmap>
* 不同版本上 Bitmap 内存分配与回收原理对比: <https://zhuanlan.zhihu.com/p/553523811>
* Android Drawable Resource学习（一）、Drawable Resource简介: <https://blog.csdn.net/LonelyRoamer/article/details/8148147>
* How to convert multiple svgs to Android vector drawable in one shot: <https://medium.com/@bhojwaniravi/how-to-convert-multiple-svgs-to-vector-drawable-in-one-shot-8b5083417747>
* Drawable图像资源抽象类: <https://www.jianshu.com/p/2e7c5ad7d5c8>
* 将Canvas转换为Drawable: <http://cn.voidcc.com/question/p-tvemojow-rp.html>
* Carson带你学Android：自定义View Canvas类使用教程: <https://blog.csdn.net/carson_ho/article/details/60598775>
* Android中Canvas绘图之PorterDuffXfermode使用及工作原理详解: <https://blog.csdn.net/iispring/article/details/50472485>

### Statsd

* Statsd: <https://source.android.google.cn/docs/core/architecture/modular-system/statsd?hl=zh-cn>
* android WMS中的Proto/ProtoLog/ProtoLogTool日志原理介绍: <https://blog.csdn.net/learnframework/article/details/130203370>
* Android中使用 Protobuf: <https://blog.csdn.net/zhaoyanjun6/article/details/125116393>
* Language Guide (proto 2): <https://protobuf.dev/programming-guides/proto2/>
* Protocol Buffers: <https://protobuf.dev/>
* Protobuf语法指南（proto2）: <https://blog.csdn.net/qq_22660775/article/details/89044538>
* Android中的StatsLog: <https://blog.csdn.net/ho_mgx/article/details/113486753>
* Statsd In android 9 (2): <https://maplestorys.github.io/2018/12/19/Statsd-In-android-9-2/>

### 文本分类

* android.view.textclassifier: <https://developer.android.com/reference/android/view/textclassifier/package-summary>

* Implement text classifier: <https://source.android.google.cn/docs/core/display/textclassifier>

* TextClassification – Part 1: <https://blog.stylingandroid.com/textclassification-part-1/>
* TextClassification – Part 2: <https://blog.stylingandroid.com/textclassification-part-2/>
* TextClassification – Part 3: <https://blog.stylingandroid.com/textclassification-part-3/>

* TensorFlow Lite: <https://www.tensorflow.org/lite>
* TensorFlow Lite 视频系列教程: <https://www.bilibili.com/video/BV18Q4y137NB/>
* MediaPipe: <https://developers.google.com/mediapipe>
* Google MediaPipe：设备端机器学习【完整解决方案】背后的技术实现: <https://mp.weixin.qq.com/s/pIyLdRpL_mzK5XCH2DEkdQ>

### App Links

* 处理 Android 应用链接: <https://developer.android.google.cn/training/app-links?hl=zh-cn>

### Sensor

* Android 4.4 Kitkat Phone工作流程浅析(十一)__PSensor工作流程浅析: <https://blog.csdn.net/yihongyuelan/article/details/43449851>

### Vibrator

* 触感反馈: <https://source.android.google.cn/docs/core/interaction/haptics>

## Article

* I18n Translation Search: <https://i18ns.com/>

* androidcommunity: <http://androidcommunity.com/>
* AndroidDevTools: <http://www.androiddevtools.cn/>

* Material Design: <https://m3.material.io/>

* Graphics: <https://source.android.com/devices/graphics>
* Supporting Multiple Users: <https://source.android.com/docs/devices/admin/multi-user>
* Android5.1--多用户模式: <https://blog.csdn.net/kitty_landon/article/details/47123767>

* Android OTA升级: <https://www.cnblogs.com/jiangxinnju/p/14404073.html>
* Android系统架构-[Android取经之路]: <https://blog.csdn.net/yiranfeng/article/details/103549149>
* Android R Framework流程分析: <https://juejin.cn/column/6982159044094427173>
* Fragment相关源码解析一——FragmentManagerImpl和BackStackRecord: <https://blog.csdn.net/chengkun_123/article/details/72548373>
* Fragment相关源码解析二——生命周期: <https://blog.csdn.net/chengkun_123/article/details/73302779>
* Fragment相关源码解析三——状态保存与恢复: <https://blog.csdn.net/chengkun_123/article/details/72832728>

* Android 编程与兼容性问题: 《Android Programming The Big Nerd Ranch Guide 3rd[Android编程权威指南（第3版）》 6.2 7.8 7.9
* lntentfilter的匹配规则: 《Android开发艺术探索》 1.3
* .nomedia: 《解析 Google Android SDK-智能手机开发范例手册》5.3
* Android：MediaSession框架介绍: <https://www.oschina.net/question/2561862_2150611>
* StrictMode: 《Android核心原理与系统应用高效开发》 9.2.3

* Handler内存泄漏详解及其解决方案: <http://blog.csdn.net/javazejian/article/details/50839443>
* Android中Handler的使用: <http://blog.csdn.net/iispring/article/details/47115879>
* Android异步更新UI的几种方法: <https://blog.csdn.net/ydxlt/article/details/51247822>
* AsyncTaskLoader vs AsyncTask: <https://stackoverflow.com/questions/7120813/asynctaskloader-vs-asynctask>
* 子线程调用Toast报Can't create handler inside thread that has not called Looper.prepare() 错误: <https://blog.csdn.net/niuls/article/details/22850631>
* Handler延迟消息执行机制，会阻塞吗？<https://blog.csdn.net/u010126792/article/details/85091348>
* Handler、Thread、HandlerThread三者的区别: <https://blog.csdn.net/weixin_41101173/article/details/79687313>

* Fragments：Pro Android 5[精通Android 3] Chapter 8
* Android Fragment的用法（一）: <https://www.cnblogs.com/guop/p/5072572.html>
* 为什么要用Fragment.setArguments(Bundle bundle)来传递参数: <https://blog.csdn.net/tu_bingbing/article/details/24143249>
* IllegalStateException: Can not perform this action after onSaveInstanceState with ViewPager: <https://stackoverflow.com/questions/7575921/illegalstateexception-can-not-perform-this-action-after-onsaveinstancestate-wit?rq=1>

* Hardware acceleration: <https://developer.android.com/guide/topics/graphics/hardware-accel>
* Android应用程序UI硬件加速渲染技术简要介绍和学习计划: <https://blog.csdn.net/Luoshengyang/article/details/45601143>
* Android 显示系统：SurfaceFlinger详解: <https://www.cnblogs.com/blogs-of-lxl/p/11272756.html>
* 关于 UI 渲染，你需要了解什么？<https://www.jianshu.com/p/279f727b00bc>
* Android P 图形显示系统（一）硬件合成HWC2: <https://www.jianshu.com/p/824a9ddf68b9>
* Android图形系统（十一）-Choreographer: <https://www.jianshu.com/p/bab0b454e39e>
* HenCoder——给高级 Android 工程师的进阶手册: <https://hencoder.com/>

* Android | 打印堆栈: <https://blog.csdn.net/u011386173/article/details/88394346>

* 多屏幕多分辨率的支持: <https://www.cnblogs.com/tianjian/p/3430085.html>
* Android开发中dip，dpi，density，px等详解: <http://blog.qiji.tech/archives/2581>
* 一种非常好用的Android屏幕适配: <https://www.jianshu.com/p/1302ad5a4b04>
* 最清晰的Android多屏幕适配方案: <https://www.cnblogs.com/soaringEveryday/p/4835839.html>
* Android 刘海屏适配全攻略: <https://blog.csdn.net/u011810352/article/details/80587531>

* Android ActionBar完全解析，使用官方推荐的最佳导航栏(上): <http://blog.csdn.net/guolin_blog/article/details/18234477>
* Android完美获取状态栏高度、标题栏高度、编辑区域高度的获取: <http://blog.csdn.net/a_running_wolf/article/details/50477965>
* menu中的item标签的showAsAction属性可以取哪些值: <https://www.jianshu.com/p/4106e1414d64>
* 什么是android.R.id.content？ <http://blog.csdn.net/colinandroid/article/details/77748695>
* Android应用坐标系统全面详解: <http://blog.csdn.net/yanbober/article/details/50419117/>
* Android中visibility属性VISIBLE、INVISIBLE、GONE的区别: <http://blog.csdn.net/chindroid/article/details/8000713>
* 如何在Root的手机上开启ViewServer，使得HierachyViewer能够连接: <http://maider.blog.sohu.com/255448342.html>
* Formatting and Plurals: Android UI Fundamentals[Android UI基础教程](Formatting and Plurals)
* Android vector标签 PathData 画图超详解: <https://www.cnblogs.com/yuhanghzsd/p/5466846.html>
* 高斯模糊: <https://zh.wikipedia.org/wiki/%E9%AB%98%E6%96%AF%E6%A8%A1%E7%B3%8A>
* 总结一下Android中主题(Theme)的正确玩法: <https://www.cnblogs.com/zhouyou96/p/5323138.html>
* Android中`@`和`?`区别以及`?attr/**`与`@style/**`等的区别: <http://blog.csdn.net/xx326664162/article/details/64125654>
* 用ColorFilter为安卓按钮增加效果: <https://www.jianshu.com/p/9cae2250d0ed>
* MaterialDesign之SearchView解锁 仿网易云音乐搜索: <http://www.sohu.com/a/142436167_611601>
* Android下setTextSize的正确使用姿势: <https://www.jianshu.com/p/7f2941dbfb17>
* Mipmap drawables for icons: <https://stackoverflow.com/questions/23935810/mipmap-drawables-for-icons>
* Android “getActionBar()返回NullPointerException”问题分析: <https://www.jianshu.com/p/feb4cc119659>
* setEnabled() vs setClickable(), what is the difference? <https://stackoverflow.com/questions/15615823/setenabled-vs-setclickable-what-is-the-difference>
* ListView中getView的原理与解决多轮重复调用的方法: <https://www.cnblogs.com/lirizhi/p/3357771.html>
* Android控件--ProgressBar: <https://blog.csdn.net/hardworkingant/article/details/71910731>
* 拖放框架: <https://developer.android.com/guide/topics/ui/drag-drop>

* Android核心分析: <https://blog.csdn.net/maxleng/category_9260799.html>
* Android系统开篇: <http://gityuan.com/android/>
* 对于android.intent.action.MAIN和android.intent.category.LAUNCHER的理解: <http://blog.csdn.net/lindroid20/article/details/51993247>
* 详解 Android 通信: <http://www.androidchina.net/5028.html>
* Android Application的使用及其生命周期: <https://www.cnblogs.com/carlo/p/4734291.html>
* Android Partitions Explained: boot, system, recovery, data, cache & misc: <https://www.addictivetips.com/mobile/android-partitions-explained-boot-system-recovery-data-cache-misc/>
* Android for work总结(上): <http://blog.csdn.net/liu1314you/article/details/52028823>
* Android for work总结(下): <http://blog.csdn.net/liu1314you/article/details/52038916>
* android获取内置和外置SD卡路径: <http://blog.csdn.net/chadeltu/article/details/43736093>
* Android之Adapter用法总结：<http://blog.csdn.net/fznpcy/article/details/8658155/>
* Android命令行/c语言/java设置获取系统属性的方法: <http://www.mikewootc.com/wiki/android/other/system_property.html>
* Implementation vs API dependency: <https://jeroenmols.com/blog/2017/06/14/androidstudio3/>
* android怎样调用@hide和internal API: <http://blog.csdn.net/linghu_java/article/details/8283042>
* android下的SuppressLint与TargetApi: <http://blog.csdn.net/pony_maggie/article/details/52115884>
* Android软键盘遮挡的四种解决方案: <https://www.cnblogs.com/jerehedu/p/4194125.html>
* 全面的Android文件目录解析和获取方法(包含对6.0系统的说明)：<https://blog.csdn.net/zhangbuzhangbu/article/details/23257873>
* Android 那些年，处理getActivity()为null的日子: <https://www.jianshu.com/p/9d75e328f1de>
* Android 汉字转拼音的多种实现方式: <https://blog.csdn.net/zhuwentao2150/article/details/70230341>
* Android 修改阿拉伯语数字显示: <https://blog.csdn.net/wangchezheng/article/details/51065470>
* Android Notification常见样式总结: <https://blog.csdn.net/w804518214/article/details/51231946>
* Android 5.0 在优先模式下依然能收到微信的提醒是什么原理？<https://www.zhihu.com/question/26692324>
* Android之分屏模式解析（上）: <https://blog.csdn.net/itluochen/article/details/52127126>
* Android之分屏模式解析（下）: <https://blog.csdn.net/itluochen/article/details/52127222>
* Android中app进程ABI确定过程: <https://blog.csdn.net/weixin_40107510/article/details/78138874>
* Context, What Context? <https://possiblemobile.com/2013/06/context/>
* INSTALL_FAILED_TEST_ONLY: <https://blog.csdn.net/zou_pl/article/details/78679394>
* Android兼容性测试CTS Verifier-环境搭建、测试执行、结果分析: <https://www.cnblogs.com/wi100sh/p/4613502.html>
* Why do most fields (class members) in Android tutorial start with `m`? <https://stackoverflow.com/questions/2092098/why-do-most-fields-class-members-in-android-tutorial-start-with-m>
* Android多语言国际化适配(兼容7.0): <https://blog.csdn.net/pigdreams/article/details/81277110>
* android程序自动化生成apk的过程: <https://blog.csdn.net/f2006116/article/details/52254519>
* Enable multidex for apps with over 64K methods: <https://developer.android.com/build/multidex#about>
* dex-method-counts: <https://github.com/jiangxincode/dex-method-counts>
* NDK编译脚本：Android.mk or CMakeLists.txt: <https://blog.csdn.net/u011686167/article/details/106458899/>
* 升级ndk报错：No toolchains found in the NDK toolchains folder for ABI with prefix: mips64el-linux-android: <https://blog.csdn.net/qq_37299249/article/details/90290468>

* What is the difference between system apps and privileged apps on Android? <https://stackoverflow.com/questions/19868138/what-is-the-difference-between-system-apps-and-privileged-apps-on-android>
* Android加密之文件级加密: <http://blog.csdn.net/myfriend0/article/details/77094890>
* Android属性allowBackup安全风险浅析: <http://www.freebuf.com/articles/terminal/60778.html>
* Android签名机制之---签名过程详解: <http://blog.csdn.net/jiangwei0910410003/article/details/50402000>
* android文件读写以及不同应用之间的文件读写操作: <http://blog.csdn.net/zyb243380456/article/details/7426449>
* Android 将自己的应用改为系统应用: <https://blog.csdn.net/xx326664162/article/details/53406933>
* Android逆向之旅---解析编译之后的AndroidManifest文件格式: <https://blog.csdn.net/jiangwei0910410003/article/details/50568487>
* Android DEX安全攻防战: <https://blog.csdn.net/androidsecurity/article/details/9428861>
* Android Dex文件格式(一): <https://www.cnblogs.com/dacainiao/p/6035274.html>
* 目前最全面的Android安全工具清单: <https://www.ctocio.com/top%E6%B8%85%E5%8D%95/23912.html>
* Open files using storage access framework: <https://developer.android.com/guide/topics/providers/document-provider>
* READ_EXTERNAL_STORAGE: <https://developer.android.com/reference/android/Manifest.permission#READ_EXTERNAL_STORAGE>
* FileProvider: <https://developer.android.com/reference/androidx/core/content/FileProvider>
* Contacts Provider: <https://developer.android.com/guide/topics/providers/contacts-provider>

* 了解一下，Android 10中的APEX: <https://blog.csdn.net/Innost/article/details/103776120>
* Android-APEX化之后如何替换对应的文件: <https://blog.csdn.net/cheriyou_/article/details/108540771>

* 安卓应用在各大应用市场上架方法整理: <https://blog.csdn.net/niezhipeng8/article/details/79103436>

* Android8.0及以上，获取模拟器root权限: <https://blog.csdn.net/weixin_42814931/article/details/81253678>
* Android真机安装sqlite3的方法: <https://www.cnblogs.com/jiangxinnju/p/8227625.html>
* 使用 Intel HAXM 为 Android 模拟器加速，媲美真机: <http://www.cnblogs.com/beginor/archive/2013/01/13/2858228.html>
* [Android] 为Android安装BusyBox —— 完整的bash shell: <https://www.cnblogs.com/xiaowenji/archive/2011/03/12/1982309.html>
* MIUI ROM适配之旅第一天——认识Android手机: <http://www.miui.com/thread-402302-1-1.html>

## Android相关的知识

* 从圆角到圆角: <https://zhuanlan.zhihu.com/p/29560646>
* J 的艺术，R 的艺术: <http://www.hi-id.com/?p=3231>
* HDR详解 - 什么是HDR？<https://zhuanlan.zhihu.com/p/212141989>

## Gradle/Gradle Wrapper/Android Plugin for Gradle

* Gradle: <http://gradle.org/>
* Gradle User Guide: <https://docs.gradle.org/current/userguide/userguide_single.html>
* Chapter 6. The Gradle Wrapper: <https://docs.gradle.org/current/userguide/gradle_wrapper.html>
* Getting Started With Gradle: <https://www.petrikainulainen.net/getting-started-with-gradle/>
* Android Gradle原理解释: <https://juejin.cn/post/6844904104486141965>
* Android Studio点击Run背后发生了什么？<https://juejin.cn/post/6844904104494366733>
* Android Studio Library 模块中 Native 代码进行 debug 的一些坑: <https://fucknmb.com/2017/05/11/Android-Studio-Library%E6%A8%A1%E5%9D%97%E4%B8%ADNative%E4%BB%A3%E7%A0%81%E8%BF%9B%E8%A1%8Cdebug%E7%9A%84%E4%B8%80%E4%BA%9B%E5%9D%91/>
* Android gradle打包涉及task源码解析（一）准备工作: <https://www.jianshu.com/p/e73510605c56>

* 彻底搞懂Gradle、Gradle Wrapper与Android Plugin for Gradle的区别和联系: <https://www.cnblogs.com/jiangxinnju/p/8229129.html>
* 通过设置JDK解决存在多个Gradle后台进程的问题: <https://www.cnblogs.com/jiangxinnju/p/13443183.html>
* Gradle Could not find method leftShift() for arguments: <https://blog.csdn.net/qq_30596077/article/details/88837029>

* Gradle学习系列之一——Gradle快速入门: <http://www.cnblogs.com/davenkin/p/gradle-learning-1.html>
* gradle使用文档: <https://yq.aliyun.com/articles/54151>
* Gradle修改本地仓库的位置: <http://blog.csdn.net/xq328220454/article/details/30233759>
* gradle cache目录(.gradle)剖析: <https://zhuanlan.zhihu.com/p/26473930>

* (老)Gradle Plugin User Guide: <http://tools.android.com/tech-docs/new-build-system/user-guide>
* 加速Android Studio/Gradle构建: <https://isming.me/2015/03/18/android-build-speed-up/>
* 用Gradle 构建你的android程序: <https://www.cnblogs.com/youxilua/archive/2013/05/20/3087935.html>
* 用Gradle 构建你的android程序-依赖管理篇: <http://www.cnblogs.com/youxilua/archive/2013/05/22/3092657.html>

* Android Gradle and the curious case of invisible dependency: <https://proandroiddev.com/android-gradle-and-the-curious-case-of-invisible-dependency-7f1bcc8bb79e>

## Android Studio

* JetBrains Plugins Repository: <https://plugins.jetbrains.com>
* Android Studio常用插件汇总: <https://www.cnblogs.com/jiangxinnju/p/13736788.html>
* 在 AndroidStudio 工程点击 Run 按钮， 实际上做了什么操作呢？<https://www.zhihu.com/question/65289196>

* 设置应用 ID: <https://developer.android.com/studio/build/application-id.html>
* (新)配置构建: <https://developer.android.com/studio/build/index.html>
* 创建和管理虚拟设备: <https://developer.android.com/studio/run/managing-avds>
* 对您的应用进行版本控制: <https://developer.android.com/studio/publish/versioning.html>
* dumpsys: <https://developer.android.com/studio/command-line/dumpsys>
* Debug Your layout with Layout Inspector and Layout Validation: <https://developer.android.com/studio/debug/layout-inspector>
* Configure Android Studio: <https://developer.android.com/studio/intro/studio-config.html>
* Configure hardware acceleration for the Android Emulator: <https://developer.android.com/studio/run/emulator-acceleration>

* Android Studio移动鼠标显示悬浮提示的设置方法: <https://www.cnblogs.com/jiangxinnju/p/8227442.html>
* ANDROID STUDIO详细教程汇总: <http://stormzhang.com/devtools/2015/06/17/android-studio-all/>
* Android Studio 3.0+ 新Dex编译器D8 Desugar R8: <https://blog.csdn.net/jamin0107/article/details/81123154>
* Android Studio系列教程一--下载与安装: <http://stormzhang.com/devtools/2014/11/25/android-studio-tutorial1/>
* Android Studio系列教程二--基本设置与运行: <http://stormzhang.com/devtools/2014/11/28/android-studio-tutorial2/>
* Android Studio系列教程三--快捷键: <http://stormzhang.com/devtools/2014/12/09/android-studio-tutorial3/>
* Android Studio系列教程四--Gradle基础: <http://stormzhang.com/devtools/2014/12/18/android-studio-tutorial4/>
* ANDROID STUDIO系列教程五--GRADLE命令详解与导入第三方包: <http://stormzhang.com/devtools/2015/01/05/android-studio-tutorial5/>
* ANDROID STUDIO系列教程六--GRADLE多渠道打包: <http://stormzhang.com/devtools/2015/01/15/android-studio-tutorial6/>
* Android Studio优化技巧：<http://blog.oneapm.com/apm-tech/257.html>
* Android Studio相关目录解析: <https://www.cnblogs.com/jiangxinnju/p/8323569.html>
* ERROR Android emulator gets killed: <https://stackoverflow.com/questions/36841461/error-android-emulator-gets-killed/47578244>

## Libraries

* Dagger2 使用: <https://blog.csdn.net/d0d0bird/article/details/119576002>
* butterknife: <https://github.com/JakeWharton/butterknife>
* xUtils3: <https://github.com/wyouflf/xUtils3>
* SlidingMenu: <https://github.com/jfeinstein10/SlidingMenu>
* ViewPagerIndicator: <https://github.com/JakeWharton/ViewPagerIndicator>
* Android-Universal-Image-Loader: <https://github.com/nostra13/Android-Universal-Image-Loader>
* hugo: <https://github.com/JakeWharton/hugo>
* 极光推送: <http://docs.jiguang.cn/jpush/resources/#android-sdk>
* 移动服务SDK：<http://www.mob.com/download>
* Retrofit(A type-safe HTTP client for Android and Java): <https://github.com/square/retrofit>

## Tools

* busybox: <https://busybox.net/>
* Test DPC APK Download for Android: <http://www.testdpc.com/>
* fastlane screenshots for Android: <https://docs.fastlane.tools/getting-started/android/screenshots/>
* Android 应用开发调试利器——开发助手，数十倍效率提升: <http://www.trinea.cn/android/android-develop-and-debug-tools/>
* 奇兔刷机：<http://www.7to.cn/>
* dexcount-gradle-plugin: <https://github.com/KeepSafe/dexcount-gradle-plugin>
* leakcanary: <https://github.com/square/leakcanary>
* Display and control your Android device: <https://github.com/Genymobile/scrcpy>
* LibChecker: <https://github.com/zhaobozhen/LibChecker>

## SVGA

* SVGA: <http://svga.io/>
* SVGAPlayer-Android: <https://github.com/svga/SVGAPlayer-Android>

## Lottie

* Lottie: <https://github.com/airbnb/lottie-android>
* Lottie - 让复杂动画如此简单: <https://www.jianshu.com/p/282d098cf928>

## Flutter

* Flutter: <https://flutter.dev/>
* Flutter中文网: <https://flutterchina.club/get-started/install/>

## Android模拟器

* genymotion: <https://www.genymotion.com/>
* genymotion个人免费版: <https://www.genymotion.com/fun-zone/>
* genymotion-idea-plugin: <https://plugins.jetbrains.com/plugin/7269-genymotion>
* 夜神模拟器: <https://www.yeshen.com/>

## ADB

* awesome-adb: <https://github.com/mzlogin/awesome-adb>
* ADB: <http://adbshell.com/>
* 解决adb push时出现的"Read-only file system"问题: <https://www.cnblogs.com/jiangxinnju/p/8186390.html>
* android adb push 与 adb install的比较（两种安装APK的方法）: <http://blog.csdn.net/liranke/article/details/6795984>
* Android 8.0 adb shell dumpsys activity activities | findstr mFocusedActivity 获取当前的 activity 显示空的: <https://www.cnblogs.com/yinzhuoqun/p/9090030.html>
* Android adb shell svc 知识详解: <https://blog.csdn.net/wenzhi20102321/article/details/132779708>
* Android 系统内的守护进程 - core类中的服务 (1) : adbd: <https://blog.csdn.net/Xiaoma_Pedro/article/details/103919142>

## App Development Platform

* Firebase: <https://firebase.google.com/>
* Plugin Fierbase Services was not installed:Cannot download...: <https://blog.csdn.net/u010368726/article/details/105263487>
* Does Firebase Work in China?: <https://www.21cloudbox.com/solutions/does-firebase-work-in-china.html>
* Supabase: <https://supabase.com/>
* Parse: <https://parseplatform.org/>
* 友盟: <https://www.umeng.com/analytics>
* bugly: <https://bugly.qq.com>
* 蒲公英：<https://www.pgyer.com/>

## XMPP

* <http://xmpp.org/>

* rfc3920: <https://tools.ietf.org/html/rfc3920>
* rfc3920翻译: <http://wiki.jabbercn.org/RFC3920>

* Open Realtime: <https://www.igniterealtime.org/>
* smack: <https://github.com/igniterealtime/Smack>

* 环信即时通讯云: <https://www.easemob.com/download/im>
* Android之基于XMPP协议即时通讯软件(一): <https://blog.csdn.net/way_ping_li/article/details/17385379>
* Android之基于XMPP协议即时通讯软件(二): <https://blog.csdn.net/way_ping_li/article/details/17403929>
* Android之基于XMPP协议即时通讯软件(三): <https://blog.csdn.net/way_ping_li/article/details/17490377>

* 基于xmpp openfire smack开发之openfire介绍和部署[1]: <https://blog.csdn.net/shimiso/article/details/8816558>
* 基于xmpp openfire smack开发之smack类库介绍和使用[2]: <https://blog.csdn.net/shimiso/article/details/8816540>
* 基于xmpp openfire smack开发之Android客户端开发[3]: <https://blog.csdn.net/shimiso/article/details/11225873>
* 基于xmpp openfire smack开发之Android消息推送技术原理分析和实践[4]: <https://blog.csdn.net/shimiso/article/details/8156439>

* 基于XMPP协议的Android聊天IM客户端: <http://archive.dutycode.com/?post=85> <http://code.google.com/p/chatchat/>

* Openfire 的安装和配置: <http://www.cnblogs.com/hoojo/archive/2012/05/17/2506769.html>
* Jabber 协议 概述: <https://blog.csdn.net/hezhi007/article/details/614359>
* Smack编写jabber客户端: <https://blog.csdn.net/qqiabc521/article/details/6393721>
* Subscriptions 运行机制: <http://www.moon-soft.com/doc/28326.htm>
* XMPP协议分析-原理篇: <https://blog.csdn.net/xutaozero21/article/details/4873439>

## Player

* Universal Android Music Player: <https://github.com/android/uamp>
* 百度音视频处理: <https://cloud.baidu.com/doc/MCT/index.html>
* ApolloMod: <https://github.com/Splitter/android_packages_apps_apolloMod>
* android-visualizer: <https://github.com/felixpalmer/android-visualizer/tree/master/src/com/pheelicks/visualizer>
* Vitamio 4.2.2版本之前的源码: <https://github.com/yixia/VitamioBundle>
* Vitamio 5.0.0版本之后的源码: <https://github.com/yixia/VitamioBundleStudio>
* 使用Vitamio打造自己的Android万能播放器: <http://www.cnblogs.com/over140/archive/2012/04/26/2471060.html>
