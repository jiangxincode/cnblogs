## 同步发布平台

* 博客园: <https://www.cnblogs.com/jiangxinnju/>
* CSDN: <https://blog.csdn.net/jiangxinnju>
* 掘金: <https://juejin.cn/user/166781500533079>
* 知乎: <https://www.zhihu.com/people/jiangxinnju/posts>

**未经允许，谢绝转载**

在以下位置描述了Android构建系统：<https：//source.android.com/setup/build>
你可以使用`build/envsetup.sh`设置一个"便利环境"来处理Android源代码。在当前shell环境中执行`source build/envsetup.sh`后，你可以输入hmm作为已定义函数的列表，这些函数有助于与源进行交互。  

## 概述

构建系统使用一些预设的环境变量和一系列"make"文件来构建Android系统并准备将其部署到平台上。

子项目的Android构建文件叫做Android.bp和Android.mk。

整个存储库的源树顶部只有一个名为"Makefile"的官方文件。你设置了一些环境变量，然后键入"make"或仅键入m来构建内容。你可以在make命令行（其他目标）中添加一些选项以打开详细输出或执行其他操作。

构建输出放置在`out/host`和`out/target`中。`out/host`下的东西是为你的主机平台（台式机）编译的东西。最终在`out/target/product/<platform-name>`下的内容会以特定方式被放到目标设备（或模拟器）。

目录`out/target/product/<platform-name>/obj`用于暂存"object"文件，这些文件是用于构建最终程序的中间二进制映像。实际落在目标文件系统中的内容存储在`out/target/product/<platform-name>`下的root，system和data目录中。通常，这些文件捆绑成名为system.img，ramdisk.img和userdata.img的映像文件。

这与大多数Android设备上使用的文件系统分区相匹配。

## 一些细节

### 使用什么工具

在构建期间，你将使用soong，ninja和'make'控制构建步骤。主机工具链（编译器，链接器和其他工具）和库将用于构建将在主机上运行的程序和工具。使用不同的工具链来编译将在目标（嵌入式板，设备或模拟器）上运行的C和C++代码。这通常是在X86平台上运行的"交叉"工具链，但会为其他平台（最常见的是ARM）生成代码。内核被编译为独立的二进制文件（它不使用程序加载器或链接到任何外部库）。其他项目，例如本机程序（例如init或工具箱），守护程序或库，将链接到仿生库或其他系统库。

你将使用Java编译器和大量与Java相关的工具来构建大多数应用程序框架，系统服务和Android应用程序本身。最后，使用工具打包应用程序和资源文件，并创建可以安装在设备上或与模拟器一起使用的文件系统映像。

### 告诉系统Java工具链在哪里

在构建任何东西之前，你必须告诉Android构建系统Java SDK的位置。（安装Java SDK是构建的先决条件）。
通过设置JAVA_HOME环境变量来执行此操作。

### 指定要构建的内容

为了决定要构建什么以及如何构建，构建系统要求设置一些变量。可以从同一源代码树构建具有不同软件包和选项的不同产品。可以通过带有"make"变量声明的文件来设置控制此变量的变量，也可以在环境中指定该变量。

设备供应商可以创建定义文件，以描述特定板或特定产品要包含的内容。定义文件称为：buildspec.mk，它位于顶级源目录中。你可以手动编辑此选项以对选择进行硬编码。

如果你有一个buildspec.mk文件，它会设置构建所需的所有make变量，而你不必弄乱选项。

指定选项的另一种方法是设置环境变量。构建系统具有一种相当华丽的方法来为你管理这些选项。

要设置你的构建环境，你需要在`build/envsetup.sh`中加载变量和函数。通过将文件`source`到你的shell环境中来执行此操作，如下所示：

```shell
. build/envsetup.sh
```

你可以在此时输入"help"（或"hmm"）以查看一些实用程序功能，这些功能可以使你更轻松地使用源代码。

要选择要构建的一组东西以及要构建的项目，请使用"choosecombo"功能或"lunch"功能。"choosecombo"将一步一步地引导你完成必须选择的不同项目，而"lunch"则允许你选择一些预设组合。

必须为构建定义的项目是：

• 产品（"generic"或某些特定的芯片或平台名称）
• 构建变体（"user"，"userdebug"或"eng"）
• 是否在模拟器上运行（"true"或"false"）
• 构建类型（"发布"或"调试"）

这些不同的构建变体的说明位于<http://source.android.com/porting/build_system.html#androidBuildVariants>

在这篇博客文章中，从用户角度很好地描述了构建过程：<http://blog.codepainters.com/2009/12/18/first-android-platform-build/>

### 实际构建系统

设置完毕后，实际上就可以使用"make"命令来构建系统。

要构建整个内容，请在顶层目录中运行"make"。如果要构建所有内容（例如，第一次进行构建），则构建将花费很长时间。

## 构建技巧

### 查看用于构建软件的实际命令

在"make"行上使用"showcommands"目标：

```shell
make -j4 showcommands
```

可以将其与另一个make目标结合使用，以查看该构建的命令。也就是说，"showcommands"本身不是目标，而只是指定构建的修饰符。

在上面的示例中，-j4与showcommands选项无关，并且用于执行4个并行运行的make会话。

### 制定目标

这是可用于构建系统不同部分的不同make目标的列表：

• `make sdk` - 构建属于SDK的工具（adb，fastboot等）
• `make snod` - 从当前软件二进制文件构建系统映像
• `make services`
• `make runtime`
• `make droid` - make droid是正常的构建。
• `make all` - 构建所有内容，无论是否包含在产品定义中
• `make clean` - 删除所有构建的文件（准备进行新的构建）。与`rm -rf out/<configuration>/`相同
• `make modules` - 显示可以构建的子模块的列表（所有LOCAL_MODULE定义的列表）
• `make <local_module>` - 构建一个特定的模块（请注意，这与目录名称不同。它是Android.mk文件中的LOCAL_MODULE定义）
• `make clean <local_module>` - 清理特定模块
• `make bootimage TARGET_PREBUILT_KERNEL=/path/to/bzImage` - 使用自定义bzImage创建新的启动映像

### 辅助宏和函数

当你获取envsetup.sh时，会安装一些辅助宏和函数。它们记录在envesetup.sh的顶部，但是这里是其中一些信息：

• `hmm` - 列出帮助内容
• `lunch <product_name>-<build_variant>` - 加载产品和构建变体配置（驱动程序文件，设备特定的配置等）。
• `tapas [<App1> <App2> ...] [arm | x86 | mips | armv5 | arm64 | x86_64 | mips64] [eng | userdebug | user]` - 该命令用于构建未捆绑的应用程序。如果你不提供构建版本，则默认为eng。
• `provision` - 烧录具有所有必需分区的设备。选项将传递给fastboot。

### 构建宏和函数

• `croot` - 将目录更改为树的顶部
• `m` - 从树的顶部执行"make"（即使当前目录位于其他位置）
• `mm` - 构建当前目录中的所有模块
• `mmm <dir1> ...` - 构建提供的目录中的所有模块，但不构建其依赖项。要限制正在构建的模块，请使用以下语法：`mmm dir /：target1,target2`。
• `mma` - 构建当前目录中的所有模块及其依赖项。
• `mmma <dir1> ...` - 构建提供的目录中的所有模块及其依赖项。

### Grep宏和函数

• `cgrep <PATTERN>` 在所有本地C/C++文件上显示。
• `ggrep <PATTERN>` 在所有本地Gradle文件上显示。
• `jgrep <PATTERN>` 在所有本地Java文件上使用。
• `resgrep <PATTERN>` 在所有本地res/*。xml文件上进行锁定。
• `mangrep <PATTERN>` 在所有本地AndroidManifest.xml文件上进行扫描。
• `mgrep <PATTERN>` 在所有本地Makefile文件上进行抓紧。
• `sepgrep <PATTERN>` 在所有本地Sepolicy文件上进行锁定。
• `sgrep <PATTERN>` 在所有本地源文件上进行抓紧。
• `godir <文件名>` 转到包含文件的目录

### 加快构建

你可以在make中使用'-j'选项，以同时启动多个make执行线程。

根据我的经验，你应该指定比计算机上具有处理器多2个线程。如果你有2个处理器，请使用'make -j4'；如果它们是超线程的（意味着你有4个虚拟处理器），请尝试'make -j6。

你还可以指定使用"ccache"编译器缓存，这将在你首次构建内容后加快处理速度。为此，请在你的shell命令行中指定"export USE_CCACHE = 1"。（请注意，ccache包含在存储库的预构建部分中，不必单独安装在主机上。）

对于最新的Android版本，没有预建的ccache，并且需要根据此commit，使用CCACHE_EXEC将路径设置为本地二进制文件。

### 仅构建单个程序或模块

如果使用`build/envsetup.sh`，则可以使用某些已定义的函数来仅构建树的一部分。使用"mm"或"mmm"命令执行此操作。

"mm"命令在当前目录（和子目录，我相信）中进行填充。使用"mmm"命令，你可以指定目录或目录列表，然后将其构建。
要安装你的更改，请从树的顶部开始"make snod"。"make snod"从当前的二进制文件构建新的系统映像。

### 设置模块特定的构建参数

Android系统中的某些代码可以按照其构建方式进行自定义（与构建变体以及发行版和调试选项分开）。你可以设置变量来控制各个构建选项，方法是在环境中进行设置，或者将其直接传递给"make"（或称为"make"的"m ..."函数）。

例如，可以通过设置INIT_BOOTCHART变量来构建支持bootchart日志记录的'init'程序。（有关为什么你可能要执行此操作，请参见在Android上使用Bootchart。）  

你可以使用以下任一方法来完成：

```shell
touch system/init/init.c
export INIT_BOOTCHART=true
make
```

或者

```shell
touch system/init/init.c
m INIT_BOOTCHART=true
```

## Makefile技巧

这些是你可以在自己的Android.mk文件中使用的东西的一些提示。

### 建立助手功能

在文件build/core/definitions.mk中定义了很多构建帮助器函数

尝试列出详尽的清单。`grep define build/core/definitions.mk`

通过以下方式调用它们：或不带参数：`$(call <FUNCTION>, <PARAM-1>, <PARAM-2>)$(call <FUNCTION>)`

以下是一些可能有趣的功能：

• `print-vars` - 打印所有Makefile变量，以进行调试（而不是它们的值）。
• `emit-line` - 在构建期间将线输出到文件
• `dump-words-to-file` - 将单词列表输出到文件
• `copy-one-file` - 将文件从一个地方复制到另一个地方（目标是否在目的地？）
• `all-subdir-makefiles` - 从当前目录开始递归调用所有文件（用法：）。Android.mkinclude $（调用all-subdir-makefiles）

### 构建变量

• `$(ANDROID_BUILD_TOP)` - AOSP文件系统根文件夹 
• `$(LOCAL_PATH)`- 通常为当前目录。由开发人员/用户在每个Android.mk文件中设置。
它会在文件树下的其他文件中被覆盖（例如，使用时）。`Android.mk include $(call all-subdir-makefiles)`

解决方法：

```Makefile
 SAVED_LOCAL_PATH := $(call my-dir)
 include $(call all-subdir-makefiles)
 LOCAL_PATH:= $(SAVED_LOCAL_PATH)
```

### 将文件直接添加到输出区域

你可以使用add-prebuilt-files函数将文件直接复制到输出区域，而无需构建任何内容。

从`prebuilt/android-arm/gdbserver/Android.mk`中提取的以下行将文件列表复制到输出区域的EXECUTABLES目录中：

`$(call add-prebuilt-files, EXECUTABLES, $(prebuilt_files))`

## 添加新程序以进行构建

### 将新程序添加到Android源代码树的步骤

• 在"外部"下建立目录
• 例如ANDROID/external/myprogram
• 创建你的C/cpp文件。
• 创建Android.mk作为external/ping/Android.mk的克隆
• 更改名称ping.c和ping以匹配你的C/cpp文件和程序名称
• 在external/zlib之后将ANDROID/build/core/main.mk中的目录名称添加为external/myprogram（至少从Android 7.1起不再需要）  
• 从源代码树的根开始
• 你的文件将显示在构建输出区域和系统映像中。
• 如果要将文件单独复制到目标（而不执行整个安装），则可以从构建输出区域的out/target/product/...下复制文件。

有关更多详细信息，请参见<http://www.aton.com/android-native-development-using-the-android-open-source-project/>。  

### 构建内核

内核是普通Android构建系统的"外部"（实际上，默认情况下，Android Open Source Project中不包括该内核）。但是，AOSP中有一些用于构建内核的工具。如果要构建内核，请从此页面开始：http : //source.android.com/source/building-kernels.html 

如果你正在为模拟器构建内核，则可能还需要查看：http : //stackoverflow.com/questions/1809774/android-kernel-compile-and-test-with-android-emulator 

而且，Ron M写道（在2012年5月21日在android-kernel邮件列表中）：

这篇文章很老-但就AOSP而言，什么都没有改变，所以如果有人对QEMU感兴趣并遇到此问题，请执行以下操作：
实际上，为AOSP提供的QEMU目标构建内核是一种不错的，更短的方法：

1. cd到你的内核源目录（仅金鱼2.6.29在模拟器中可用）
2. $ {ANDROID_BUILD_TOP} /external/qemu/distrib/build-kernel.sh -j = 64 --arch = x86 --out = $ YourOutDir
3. emulator -kernel ${YourOutDir}/kernel-qemu # run emulator:

步骤＃2 调用toolbox.sh包装程序脚本，该脚本可在SSE禁用gcc警告的情况下工作-在GCC <4.5时发生（如AOSP预先构建的X86工具链中一样）。

如果它是X86，该脚本会添加"-mfpmath = 387 -fno-pic"，从而消除了上面看到的编译错误。

为了更好地控制构建过程，可以使用"toolbox.sh"包装器并设置一些其他内容，而无需修改脚本文件。

下面是构建相同模拟器的示例：

```shell
# Set arch
export ARCH=x86
# Have make refer to the QEMU wrapper script for building android over x86 
(eliminates the errors listed above)
export 
CROSS_COMPILE=${ANDROID_BUILD_TOP}/external/qemu/distrib/kernel-toolchain/android-kernel-toolchain-
# Put your cross compiler here. I am using the AOSP prebuilt one in this example
export 
REAL_CROSS_COMPILE=${ANDROID_BUILD_TOP}/prebuilt/linux-x86/toolchain/i686-android-linux-4.4.3/bin/i686-android-linux-
# Configure your kernel - here I am taking the default goldfish_defconfig
make goldfish_defconfig
# build
make -j64
# Run emulator:
emulator -kernel arch/x86/boot/bzImage -show-kernel
```

这适用于2.6.29 goldfish 分支。

## 译自<https://elinux.org/Android_Build_System>
