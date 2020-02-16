# C_CPP学习之路 [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

## Reference

* <http://www.cplusplus.com/>
* <http://cppreference.com/>
* News, Status & Discussion about Standard C++: <https://isocpp.org/>
* C++ compiler support: <https://en.cppreference.com/w/cpp/compiler_support>
* C standard library: <https://en.wikipedia.org/wiki/C_standard_library>
* C++ Standard Library: <https://en.wikipedia.org/wiki/C%2B%2B_Standard_Library>

* comp.lang.c Frequently Asked Questions: <http://c-faq.com/>
* C 语言常见问题集: <http://c-faq-chn.sourceforge.net/ccfaq/>
* The C++ Standard Library - A Tutorial and Reference: <http://www.cppstdlib.com/>

## Libraries

* boost: <http://www.boost.org/>
* Ncurses: <http://invisible-island.net/ncurses/ncurses.html>
* GMP: <https://gmplib.org/>
* Crypto++: <http://www.cryptopp.com/>
* OGLplus: <http://oglplus.org/>
* POSIX Threads for Win32: <https://www.sourceware.org/pthreads-win32/>
* Borland Graphics Interface (BGI) for Windows: <http://www.cs.colorado.edu/~main/cs1300/doc/bgi/>
* libcstl: <http://libcstl.org/>
* SWIG: <http://www.swig.org/>
* Win32 BGI implementation: <https://sourceforge.net/projects/openbgi/>
* EasyX Library for C++: <http://www.easyx.cn/>
* EGE（Easy Graphics Engine）: <http://xege.org/>
* CLucene - a C++ search engine: <https://sourceforge.net/projects/clucene/>
* Translate STL 2 C Language: <https://sourceforge.net/projects/tstl2cl/>
* Borland-style CONIO: <https://sourceforge.net/projects/conio/>
* DISLIN: <https://www.mps.mpg.de/dislin/>
* ICU - International Components for Unicode: <http://site.icu-project.org/>
* libevent: <http://libevent.org/>
* List of numerical libraries: <https://en.wikipedia.org/wiki/List_of_numerical_libraries>
* Standard Template Library Programmer's Guide: <http://www.sgi.com/tech/stl/>
* Cairo: <http://www.cairographics.org/>

## Windows C++

* /std (Specify Language Standard Version): <https://docs.microsoft.com/zh-cn/cpp/build/reference/std-specify-language-standard-version>
* CRT Library Features: <https://docs.microsoft.com/en-us/cpp/c-runtime-library/crt-library-features>
* UCRT 按字母顺序排列的函数参考: <https://docs.microsoft.com/zh-cn/cpp/c-runtime-library/reference/crt-alphabetical-function-reference>
* 从 WRL 移动到 C++/WinRT: <https://docs.microsoft.com/zh-cn/windows/uwp/cpp-and-winrt-apis/move-to-winrt-from-wrl>
* Security Features in the CRT: <https://docs.microsoft.com/en-us/cpp/c-runtime-library/security-features-in-the-crt>
* Importing and Exporting: <https://docs.microsoft.com/en-us/cpp/build/importing-and-exporting>
* OneCore.lib umbrella library (by module): <https://docs.microsoft.com/zh-cn/windows/win32/apiindex/umbrella-lib-onecore>
* Windows 8.1 API Sets: <https://docs.microsoft.com/zh-cn/windows/win32/apiindex/windows-81-api-sets>
* Windows 7 API Sets: <http://www.geoffchappell.com/studies/windows/win32/apisetschema/history/sets61.htm>
* major changes between 7.00 and 8.00: <http://www.smorgasbordet.com/pellesc/changes_700_800.htm>
* SecureZeroMemory function: <https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/aa366877(v=vs.85)>
* ShellExecuteA function: <https://docs.microsoft.com/zh-cn/windows/win32/api/shellapi/nf-shellapi-shellexecutea>
* 链接器工具错误 LNK2026: <https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/100ezk17(v=vs.90)>
* CREATEGUID Function (GUID): <https://docs.microsoft.com/en-us/previous-versions/dynamicsnav-2013r2/dd339033(v=nav.71)>
* DUMPBIN Reference: <https://docs.microsoft.com/en-us/cpp/build/reference/dumpbin-reference>
* 为 Visual C++ 项目创建的文件类型: <https://docs.microsoft.com/zh-cn/cpp/ide/file-types-created-for-visual-cpp-projects>
* I/O Completion Ports: <https://docs.microsoft.com/zh-cn/windows/win32/fileio/i-o-completion-ports>

* C/C++ Compiler and build tools errors and warnings: <https://docs.microsoft.com/en-us/cpp/error-messages/compiler-errors-1/c-cpp-build-errors>
  * C2360(initialization of 'identifier' is skipped by 'case' label)
  * C4251('identifier' : class 'type' needs to have dll-interface to be used by clients of class 'type2')
    * Exporting classes containing std:: objects (vector, map, etc) from a dll: <https://stackoverflow.com/questions/767579/exporting-classes-containing-std-objects-vector-map-etc-from-a-dll>
  * LNK4042(object specified more than once; extras ignored)
    * Visual Studio 2010's strange “warning LNK4042”: <https://stackoverflow.com/questions/3695174/visual-studio-2010s-strange-warning-lnk4042>
    * Visual Studio 2010 & 2008 can't handle source files with identical names in different folders?: <https://stackoverflow.com/questions/3729515/visual-studio-2010-2008-cant-handle-source-files-with-identical-names-in-diff>
  * LNK4098(defaultlib 'library' conflicts with use of other libs; use /NODEFAULTLIB:library)

* GetPrivateProfileString/WritePrivateProfileString(INI读取和写入): <https://docs.microsoft.com/zh-cn/windows/desktop/api/winbase/>

* C++17 Feature Removals And Deprecation: <https://devblogs.microsoft.com/cppblog/c17-feature-removals-and-deprecations/>

* atexit和onexit的主要用法和区别: <http://technet.microsoft.com/zh-cn/library/tze57ck3>
* _onexit, _onexit_m: <http://technet.microsoft.com/zh-cn/library/zk17ww08>
* Windows 8 SDK: Include files in "shared", "um", and "winrt" directories. What's the difference? <https://social.msdn.microsoft.com/Forums/vstudio/en-US/24b9c784-d642-423e-a407-8bbee14e19ab/windows-8-sdk-include-files-in-quotsharedquot-quotumquot-and-quotwinrtquot>

* VC 运行时库 /MD、/MDd 和 /MT、/MTd: <https://www.iteye.com/blog/qimo601-1550348>
* #error Please use the /MD switch for _AFXDLL builds: <https://stackoverflow.com/questions/4229120/error-please-use-the-md-switch-for-afxdll-builds>
* LINK : fatal error LNK1104: 无法打开文件“LIBCD.lib”: <https://www.cnblogs.com/hyfemma/archive/2010/11/14/1876846.html>
* error C4995: “wcscpy”: 名称被标记为 #pragma deprecated: <https://www.cnblogs.com/aliflycoris/p/11328425.html>
* VC 常用数据类型总结 俩篇: <http://www.cnblogs.com/sadier/articles/102085.html>
* 预编译头文件介绍和说明: <http://www.cppblog.com/AutomateProgram/archive/2010/10/14/129846.html>
* 预编译头文件解析: <http://www.cnblogs.com/khler/archive/2010/07/22/1782977.html>
* VC 预编译头文件的使用: <http://www.cnblogs.com/xiao-cheng/archive/2012/02/05/2338787.html>
* VC++6.0应用程序错误,0x5003eaed: <https://jingyan.baidu.com/article/1709ad80a1b2c64634c4f0eb.html>
* VC++，掀起你的盖头来——谈VC++对象模型: <http://www.cnblogs.com/chio/archive/2007/11/25/971644.html>
* Visual C++ 入门精解: <http://www.cppblog.com/yuqilin1228/archive/2010/03/26/110614.html>
* Useful enhancements for Visual Studio .NET: <http://www.codeproject.com/Articles/2704/Useful-enhancements-for-Visual-Studio-NET>
* Windows动态库与Linux共享对象比较: <https://blog.csdn.net/jatula/article/details/83324280>
* ODBC中的FX/Bulk RFX数据交换机制分析: <http://blog.csdn.net/workdog/article/details/1524126>
* VC++6.0编译时总死机，安装vcsp6补丁: <https://blog.csdn.net/xs574924427/article/details/8242414>
* MSVC vs. MinGW 之 (lib,dll,def,obj,exe) vs (a,dll,def,o,exe): <http://blog.sina.com.cn/s/blog_5ea0192f010102ig.html>
* visual studio 2008中头文件和库文件路径设置: <http://blog.sina.com.cn/s/blog_77c35cff01010u7b.html>
* VS2005调试时出现无法找到调试信息解决方案: <https://blog.csdn.net/bozhi2008/article/details/83732685>
* VS2017中设置程序以管理员身份运行: <https://blog.csdn.net/li_wen01/article/details/80110423>
* VS2017应用在XP系统上运行: <https://blog.csdn.net/baidu_33720448/article/details/84284625>
* 在 VS2017 使用所有旧版本的平台工具集: <https://bbs.pediy.com/thread-248840.htm>
* Visual Studio 如何屏蔽告警: <https://blog.csdn.net/ZHAOJUNWEI08/article/details/84288189>
* C++：在程序中获取全球唯一标识号（GUID或UUID）: <https://www.cnblogs.com/john-h/p/5886761.html>
* MSBulid、IncrediBuild命令行接口实现自动化编译: <https://blog.csdn.net/yockie/article/details/17010509>
* 理解WinRT: <http://www.cppblog.com/weiym/archive/2013/01/13/197234.html>
* 请问如何修改某个exe文件的版本信息，包括CompanyName、ProductName等？: <https://bbs.csdn.net/topics/80184784>

## 需要整理的

* DEBUG和RELEASE 版本差异及调试相关问题: <https://blog.csdn.net/orc/article/details/8758>
* Debug和Release有什么区别: <https://blog.csdn.net/chenhu_doc/article/details/932305>
* 关于VS中区分debug与release，32位与64位编译的宏定义: <https://blog.csdn.net/zhuyingqingfen/article/details/24352137>
* VC++中debug跟release编译模式的区别总结: <https://www.iteye.com/blog/javafans-609937>

## Linux C++

* GNU C Library: <https://en.wikipedia.org/wiki/GNU_C_Library>
* C POSIX library: <https://en.wikipedia.org/wiki/C_POSIX_library>
* POSIX.1-2017: <http://pubs.opengroup.org/onlinepubs/9699919799>

* GCC, the GNU Compiler Collection: <https://gcc.gnu.org/>
* The LLVM Compiler Infrastructure: <http://llvm.org/>
* clang: a C language family frontend for LLVM: <http://clang.llvm.org/>

* GNU GCC手册-1: <http://blog.chinaunix.net/uid-10386087-id-2958766.html>
* gcc的基本用法: <http://blog.chinaunix.net/uid-20183141-id-1731007.html>
* Comparison of Diagnostics between GCC and Clang: <https://gcc.gnu.org/wiki/ClangDiagnosticsComparison>
* gcc和g++的区别: <http://www.linuxsky.org/doc/dev/200804/298.html>

* GNU build system: <http://en.wikipedia.org/wiki/GNU_build_system>
* GNU_Libtool: <http://en.wikipedia.org/wiki/GNU_Libtool>
* Autotools Mythbuster: <https://autotools.io/index.html>
* Autoconf: <http://zh.wikipedia.org/wiki/Autoconf>
* Automake: <http://zh.wikipedia.org/wiki/Automake><https://baike.baidu.com/item/aotumake>

* Linux内核中无名管道pipe和有名管道fifo的分析: <http://blog.csdn.net/duanyipeng/article/details/6825232>
* 应用 Valgrind 发现 Linux 程序的内存问题: <http://www.ibm.com/developerworks/cn/linux/l-cn-valgrind/>
* 如何在linux下检测内存泄漏: <http://www.ibm.com/developerworks/cn/linux/l-mleak/>
* Linux下的时间概念(主要是其中的计时器的使用): <http://blog.chinaunix.net/uid-23215128-id-2521295.html>
* Linux 桌面应用技术专题: <http://www.ibm.com/developerworks/cn/linux/theme/desktop/index.html>
* Linux系统调用列表: <http://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html>
* Linux 套接字编程中的 5 个隐患: <http://www.ibm.com/developerworks/cn/linux/l-sockpit/>
* 使用 GLib 工具集管理 C 数据帖子发表于: <http://forum.ubuntu.org.cn/viewtopic.php?p=2614850>
* Linux静态/动态链接库的创建和使用: <https://blog.csdn.net/hcj2002/article/details/712146>
* 基于X的GNOME、GTK、GDK、XLib、GLib等之间的关系: <http://socol.iteye.com/blog/579718>

## Windows/Linux剪不断理还乱

* MinGW-w64(推荐): <http://mingw-w64.org/>
* MinGW-w64下载地址:<https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/>
* What is difference between sjlj vs dwarf vs seh? <https://stackoverflow.com/questions/15670169/what-is-difference-between-sjlj-vs-dwarf-vs-seh>
* MinGW: <http://www.mingw.org/>
* TDM-GCC: <http://tdm-gcc.tdragon.net/>
* cygwin: <http://www.cygwin.com/>
* 对话 UNIX: 在 Windows 上使用 Cygwin: <http://www.ibm.com/developerworks/cn/aix/library/au-spunix_cygwin/>
* GTK+与MFC不完全对比: <http://blog.csdn.net/absurd/article/details/1091143>
* 将 MFC 应用程序移植到 Linux: <https://www.ibm.com/developerworks/cn/linux/guitoolkit/l-mfc/index.html>
* Enabling string conversion functions in MinGW: <http://tehsausage.com/mingw-to-string>

## C++近场通讯开发

* Win32蓝牙开发: <https://docs.microsoft.com/zh-cn/windows/win32/bluetooth/bluetooth-start-page>

* Native Wifi: <https://docs.microsoft.com/zh-cn/windows/win32/nativewifi/portal>
* Wi-Fi Direct: <https://docs.microsoft.com/en-us/windows-hardware/drivers/partnerapps/wi-fi-direct>
* Wi-Fi Direct Legacy Connection C++ WRL Demo: <https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/WiFiDirectLegacyAP>
* Windows.Devices.WiFi Namespace: <https://docs.microsoft.com/en-us/uwp/api/windows.devices.wifi>
* Windows.Devices.WiFiDirect Namespace(含Wi-Fi Direct sample): <https://docs.microsoft.com/en-us/uwp/api/Windows.Devices.WiFiDirect><https://github.com/microsoft/Windows-universal-samples/tree/master/Samples/WiFiDirect>
* Windows.Devices.WiFiDirect.Services Namespace: <https://docs.microsoft.com/en-us/uwp/api/Windows.Devices.WiFiDirect.Services><https://github.com/microsoft/Windows-universal-samples/tree/master/Samples/WiFiDirectServices>

* WiFi direct 的相关特点: <https://www.cnblogs.com/TheAfter/p/9914480.html>
* NATIVE WIFI HOSTED NETWORK VS WIFI DIRECT LEGACY SOFT AP: <https://www.btframework.com/hostednetwork.htm>

## Eclipse CDT

* <http://www.eclipse.org/cdt/>
* eclipse 配置 TDM-GCC 64位版方法: <http://blog.csdn.net/luozhuang/article/details/8270522>
* eclipse写C++控制台程序，不见输出: <http://bbs.csdn.net/topics/360207855>
* eclipse C/ C++编译含有多个main函数的项目: <https://blog.csdn.net/u011039332/article/details/50389979>

## Dev-C++

* Dev-C++: <https://sourceforge.net/projects/orwelldevcpp/>

## CMake

* <https://cmake.org/>

## GDB

* GDB: The GNU Project Debugger: <http://www.gnu.org/software/gdb/>
* LINUX下GDB调试: <http://blog.csdn.net/sco_field/article/details/4310987>

## 包管理器

* Does C++ need a universal package manager? <http://pfultz2.com/blog/2017/10/27/universal-package-manager/>
* vcpkg(C++ Library Manager for Windows, Linux, and MacOS): <https://github.com/Microsoft/vcpkg>
* 解决vcpkg下载缓慢的问题: <https://blog.csdn.net/qq_39690181/article/details/82910610>
* Conan(the C / C++ Package Manager for Developers): <https://conan.io/>
* Buckaroo: <https://www.buckaroo.pm/>
* cget: <https://cget.readthedocs.io/en/latest/>
* Conda: <https://conda.io/docs/>
* CPM(Deprcated): <http://www.cpm.rocks/>
* CPPAN: <https://cppan.org/>
* Hunter: <https://docs.hunter.sh/en/latest/>

## 一点经验教训

C/C++由于历史原因，编译，构建难度相对于目前主流的其他语言如Java、Python、Go等要大的多，不同操作系统平台，不同编译工具差别很大，且没有一个完美的包管理工具，为了少花时间到环境配置上，推荐选型如下：

* 如果是Windows平台，且基本没有依赖，建议配套CLION+CMAKE+GCC(MinGW);
* 如果是Windows平台，且依赖较多，比如Gtest，OpenSSL，建议配套VS+VCPKGS;
* 如果是Linux平台，CLION+CMAKE+GCC

## Glib/GTK+/Gnome

* GLib Reference Manual: <https://developer.gnome.org/glib/stable/>
* Glib Test Framework: <https://developer.gnome.org/glib/stable/glib-Testing.html>
* GLIB 常用数据结构介绍: <http://blog.csdn.net/billxin2012/article/category/5334329>
* glib库简介: <http://liujian.is-programmer.com/posts/243.html>
* glib库异步队列和线程池代码分析: <http://blog.csdn.net/ljl1704/article/details/17243429>

* GTK+: <http://www.gtk.org/>
* Part II. GTK+ Widgets and Objects: <https://developer.gnome.org/gtk3/stable/gtkobjects.html>
* Migrating from GTK+ 2.x to GTK+ 3: <https://developer.gnome.org/gtk3/stable/gtk-migrating-2-to-3.html>
* GTK+ 2.0 Tutorial: <https://developer.gnome.org/gtk-tutorial/stable/>
* GTK+ 2.0 Tutorial(中文版): <http://www.huzheng.org/ebook/gtk2-tut/book1.html>
* GTK-Doc: <http://www.gtk.org/gtk-doc/>
* 在Windows下使用GTK+开发GUI应用程序: <http://blog.csdn.net/blackboyofsnp/article/details/3343045>
* Ubuntu下GTK的安装、编译和测试: <http://www.cnblogs.com/niocai/archive/2011/07/15/2107472.html>
* 《GTK+》编程基础: <http://guoyinghui2012.blog.163.com/blog/static/20871720020126294943228/>
* 在gtk+程序中显示中文说明: <http://blog.chinaunix.net/uid-222028-id-2658485.html>
* Gtk对于通常的gui程序，大家想做的事就是做一点事件处理(包括各种计算、文件操作等)，然后在界面上显示出来: <http://www.cnblogs.com/cy163/archive/2007/06/16/785341.html>
* GTK+2.0 中的容器控件与布局技巧: <http://www.ibm.com/developerworks/cn/linux/l-gtk/part1/>
* GTK编程: <http://jianlee.ylinux.org/Computer/C/gtk%E7%BC%96%E7%A8%8B.html>
* GTK+ 2.0 教程－－信号和回调函数的原理: <http://blog.csdn.net/lastking/article/details/67356>
* ubuntu 14.04 中找不到libgtk-x11-2.0.so: <http://www.cnblogs.com/bovenson/p/3684356.html>
* GTK v1.2 Tutorial: <https://www.gtk.org/tutorial1.2/gtk_tut.html>

* GNOME 开发者中心: <https://developer.gnome.org/>
* Gnome下载地址: <http://ftp.gnome.org/pub/gnome/>
* Port your application from GNOME 2 to GNOME 3: <https://developer.gnome.org/Gnome3PortingGuide/>
* Vala - Compiler for the GObject type system: <https://wiki.gnome.org/Projects/Vala>

* Anjuta(难用): <http://anjuta.org/>
* Glade(难用): <https://glade.gnome.org/>
* Glade User Interface Designer Reference Manual: <https://developer.gnome.org/gladeui/unstable/>
* 用Glade和libGlade设计Gtk＋图形界面: <http://blog.sina.com.cn/s/blog_606c49090100fa30.html>

### GTK中的delete_event和destroy

* delete_event 事件一般由用户或者说用户通过窗口管理器产生，即点击窗口右上角的退出按钮。假如不做任何特殊处理，窗口管理器会自动产生destroy信号；如果我们自 定义了处理delete_event事件的回调函数，是否产生destroy信号就和函数的返回值有关，如果是FALSE就产生，反之则没有效果。
* destroy，除了可以由delete_event事件产生之外，还可以通过gtk_widget_destroy函数与其它信号发生交换。同样，如果不加指定，默认结果是关闭所指向的窗口但并不结束进程。如果我们希望主窗口和进程一起关闭，必须使用gtk_main_quit()。

## QT

* <http://www.qt.io/>
* Qter开源社区: <http://www.qter.org/>
* qtcn: <http://www.qtcn.org/bbs/i.php>

## wxWidgets

* <http://www.wxwidgets.org/>

## Doxygen

* <https://github.com/doxygen/doxygen>
* 学习用 doxygen 生成源码文档: <http://www.ibm.com/developerworks/cn/aix/library/au-learningdoxygen/>
* 使用doxygen为C/C++程序生成中文文档（上）: <http://blog.csdn.net/fmddlmyy/article/details/1663898>
* Doxygen + Graphviz + Htmlhelp, 成为文档好手: <http://www.cnblogs.com/lidabo/archive/2012/12/24/2831518.html>

## Unit Test

* Google Test: <https://github.com/google/googletest>
* 玩转Google开源C++单元测试框架Google Test系列(gtest)(总): <http://www.cnblogs.com/coderzh/archive/2009/04/06/1426755.html>
* Code Blocks+gtest环境配置: <https://www.cnblogs.com/jiangxinnju/p/10163312.html>
* C++ unit test start guide, how to set up Google Test (gtest) in Eclipse?：<http://www.codeproject.com/Articles/811934/Cplusplus-unit-test-start-guide-how-to-set-up-Goog>

* CppUnit(C++ port of JUnit): <https://sourceforge.net/projects/cppunit/>
* 使用CppUnit(Windows): <http://www.cnblogs.com/zhcncn/archive/2012/12/25/2832162.html>
* cppunit helloworld详尽篇(Linux): <https://blog.csdn.net/snaill/article/details/605374>
* 开放源码 C/C++ 单元测试工具，第 3 部分: 了解 CppTest: <http://www.ibm.com/developerworks/cn/aix/library/au-ctools3_ccptest/>
* CppUnit源码解读: <http://morningspace.51.net/resource/cppunit/cppunit_anno.html>

* C Unit Testing Framework: <https://sourceforge.net/projects/cunit/>

* Parasoft C/C++test: <https://www.parasoft.com/products/ctest>

## 日志

* Log library for C++: <https://sourceforge.net/projects/log4cpp/>
* log4cplus: <https://sourceforge.net/projects/log4cplus/>
* log4cxx: <https://logging.apache.org/log4cxx/latest_stable/>

* glog: <https://github.com/google/glog>
* C++日志操作开源函数库之Google-glog: <https://www.cnblogs.com/kuliuheng/p/5046101.html>
* Google glog 使用: <https://www.cnblogs.com/zhoug2020/p/5884598.html>
* 关于glog使用中遇到的问题: <https://www.cnblogs.com/haodafeng/p/11969284.html>
* 在Windows上编译、应用glog: <https://blog.csdn.net/sagittarius_warrior/article/details/77482087>

## OpenSSL

* OpenSSL: <https://www.openssl.org>
* BoringSSL: <https://github.com/google/boringssl>
* LibreSSL: <http://www.libressl.org/>
* OpenSSL 在windows系统下的编译全解: <https://blog.csdn.net/danscort2000/article/details/81300248>

## XML

* TinyXML: <https://sourceforge.net/projects/tinyxml/> <https://github.com/leethomason/tinyxml2>
* Libxml2: <http://xmlsoft.org/>

## JSON

* jsoncpp: <https://github.com/open-source-parsers/jsoncpp>
* nlohmann/json(JSON for Modern C++): <https://github.com/nlohmann/json>

## 其它配置格式

* libconfig: <https://github.com/hyperrealm/libconfig>

## Ctags

* <https://sourceforge.net/projects/ctags/>

## CLIPS

    CLIPS is a productive development and delivery expert system tool which provides a complete environment for the construction of rule and/or object based expert systems.

* <http://clipsrules.sourceforge.net/WhatIsCLIPS.html>

## Xapian

    Xapian is an Open Source Search Engine Library, released under the GPL v2+. It's written in C++, with bindings to allow use from Perl, Python, PHP, Java, Tcl, C#, Ruby, Lua, Erlang and Node.js (so far!)

* <http://xapian.org/>

## 标准C/C++语法知识点

* C结构体之位域（位段）: <https://www.cnblogs.com/bigrabbit/archive/2012/09/20/2695543.html>
* C++ NULL与nullptr的区别: <https://www.cnblogs.com/Philip-Tell-Truth/p/6594632.html>
* nothrow: <http://www.cplusplus.com/reference/new/nothrow/>
* C++中的delete和delete[]的区别: <https://blog.csdn.net/u012936940/article/details/80919880>
* 对C++中map的四种插入方式的比较及同值覆盖问题: <https://blog.csdn.net/qq_41135605/article/details/98876749>

## Others

* C++代码质量度量工具大阅兵: <https://www.cnblogs.com/jiangxinnju/p/12292818.html>

* The International Obfuscated C Code Contest: <http://www.ioccc.org/>

* C++基础----C++ 布尔类型（bool）及BOOL和bool的区别: <https://blog.csdn.net/qiaoxinyu1989/article/details/80942364>
* size_t 类型: <https://www.cnblogs.com/xiongmao-cpp/p/5233760.html>
* C++命名空间: <https://blog.csdn.net/xiongya8888/article/details/89345539>
* c++对象的生命周期: <https://blog.csdn.net/j_factory/article/details/3582499>
* C语言内存分配方式: <https://www.cnblogs.com/dyx1024/archive/2011/01/27/2556769.html>
* C++ 中 # 和 ## 和 #@ 的使用: <https://blog.csdn.net/martinue/article/details/84344384>
* 容器元素是const元素时的错误: <https://segmentfault.com/q/1010000004125702>
* Does C++11 allow vector<const T>? <https://stackoverflow.com/questions/6954906/does-c11-allow-vectorconst-t>
* Comparing Two High-Performance I/O Design Patterns: <http://www.artima.com/articles/io_design_patterns.html>
* 使您的软件运行起来——防止缓冲区溢出：<https://www.ibm.com/developerworks/cn/security/buffer-defend/index.html#main>
* 屏幕输出VS文件输出：<http://blog.csdn.net/jiangxinnju/article/details/26081963>
* 亲密接触C可变参数函数 : <http://blog.csdn.net/linyt/article/details/2243605>
* TCP连接中的TIME_WAIT状态: <http://blog.csdn.net/sunnydogzhou/article/details/6572071>
* see also: 《TCP-IP详解卷1：协议》第十八章
* TCP可靠传输及流量控制系列六：TCP连接中的TIME_WAIT状态: <http://zenhumany.blog.163.com/blog/static/1718066332010827104655541/>
* C++项目中的extern "C" {}: <http://www.cnblogs.com/skynet/archive/2010/07/10/1774964.html>
* 由函数clock想到的: <http://blog.csdn.net/jiangxinnju/article/details/25411743>
* 理解 pkg-config 工具: <http://www.cheWebScarabnjunlu.com/2011/03/understanding-pkg-config-tool/>
* C/C++中的abort、atexit、exit和_Exit: <http://blog.csdn.net/jiangxinnju/article/details/38155973>
* setjmp()/longjmp()的使用方法和场合: <http://www.cnblogs.com/lowhere/archive/2008/08/22/1274309.html>
* C++ 工程实践(7)：iostream 的用途与局限: <http://blog.csdn.net/solstice/article/details/6612179>
* 指针的大小: <http://shansun123.iteye.com/blog/398601>
* C/C++指针原理: <http://blog.csdn.net/column/details/c-pointer.html>
* C++ STL轻松导学: <http://morningspace.51.net/resource/stlintro/stlintro.html?s=85fee499fe8534afc1f76ceceb0d41ff>
* undefined reference问题总结: <http://ticktick.blog.51cto.com/823160/431329/>
* C++ Rocks!: <http://cpprocks.com/>
* 减少C++代码编译时间的方法: <http://www.cnblogs.com/misserwell/p/4343927.html>
* C++编译错误cannot have cv-qualifier: <https://www.cnblogs.com/jiangxinnju/p/5516904.html>
* 在 console mode 中使用 C/C++ 编译器: <https://blog.csdn.net/dlyhlq/article/details/2104217>
* 基于对象和面向对象的区别: <http://www.cnblogs.com/jiangxinnju/p/5516880.html>
* const 不再迷茫: <https://www.cnblogs.com/jiangxinnju/p/5516881.html>
* C语言中随机数相关问题: <https://www.cnblogs.com/jiangxinnju/p/5516905.html>
* VS Code C++ 代码格式化方法(clang-format): <https://blog.csdn.net/core571/article/details/82867932>
* C/C++大数库简介: <https://www.cnblogs.com/jiangxinnju/p/5516911.html>
* cdecl: <http://www.cdecl.org/>
* Return-into-libc 攻击及其防御: <https://www.csdn.net/article/a/2014-03-03/15818077>
* C++资源之不完全导引: C++资源之不完全导引.docx
