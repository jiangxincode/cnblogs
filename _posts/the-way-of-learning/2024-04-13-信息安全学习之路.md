---
title: "密码恢复工具分析"
categories:
  - others
tags:
  - Password Recovery
---

## 开源密码恢复工具

* 主流格式压缩包密码破解方法+字典枚举 整理+工具: <https://www.52pojie.cn/thread-1478639-1-1.html>
* 解压缩全能王，一个解压缩的Android软件，支持密码破解，原理类似于Wifi王能钥匙，根据上传文件和对应的密码，组成一个词典，使用者上传文件的MD5值，即可能查询到对应的密码

### Kali

* Kali: <https://www.kali.org/>
* Kali Tools: <https://www.kali.org/tools>
* hydra(九头蛇): <https://www.kali.org/tools/hydra/>
* Hashcat: <https://www.kali.org/tools/hashcat/>

### John the Ripper

* John the Ripper password cracker: <https://www.openwall.com/john/>
* Johnny - GUI for John the Ripper: <https://openwall.info/wiki/john/johnny>
* Hash Suite: <https://hashsuite.openwall.net/>
* 使用John the ripper 破解RAR、ZIP、Word、Excel、PDF文件密码: <https://www.cnblogs.com/AirCrk/p/12939305.html>

### rarcrack

官网已经从`rarcrack`改为`JPassword Recovery Tool`

* rarcrack: <https://www.kali.org/tools/rarcrack/>
* JPassword Recovery Tool: <https://sourceforge.net/projects/jpassrecovery/>

### 压缩包字典破解脚本(bat)

百度贴吧一个叫做`鸢一折纸`的作者，写的一个简单的bat脚本，利用7zip程序进行字典密码遍历。

对应文件: `字典破解2.0(支持7z并且支持中文).zip`

* 鸢一折纸 1.0: <https://tieba.baidu.com/p/5159166828>
* 鸢一折纸 2.0: <https://tieba.baidu.com/p/5789842044>

### ArchivePasswordTestTool(C#)

`世界丿凌晨`在`鸢一折纸`的`压缩包字典破解2.0`bat脚本基础上做了优化，后面又写了C#版本即`ArchivePasswordTestTool`。主要是利用`SevenZipSharp`库，读取密码后进行并行密码尝试。做的比较好的是增加了程序自检更新功能。但是整体功能比较简单。

对应文件: `ArchivePasswordTestTool.zip`

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/202405182236.png)

* 介绍: <https://www.bilibili.com/read/cv6101558>
* ArchivePasswordTestTool: <https://github.com/dawn-lc/ArchivePasswordTestTool>
* SevenZipSharp: <https://github.com/squid-box/SevenZipSharp>

### ArchivePasswordTestTool(Java)

一个多线程读取字典文件，并使用`zip4j`库进行解压密码尝试的工具。使用Java语言编写，有个简单的Swing界面。

对应文件: `ArchivePasswordTestTool-windows-20220429.7z`

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/202405182233.jpg)

* ArchivePasswordTestTool: <https://github.com/RiverChu0/ArchivePasswordTestTool>

### zip-file-cracker(Java)

使用WinRar破解各种类型的压缩文件，使用了多线程技术，但是整体速度较慢。使用Java语言，没有GUI界面。

* zip-file-cracker: <https://github.com/shuanglong1104/zip-file-cracker>

### Compressor(Java)

使用Java语言编写，有个简单的Swing界面。使用`java-unrar`和`commons-compress`做暴力尝试。

* Compressor: <https://github.com/xu-ben/Compressor>
* jukka/java-unrar(No maintance): <https://github.com/jukka/java-unrar>
* java-unrar(No maintance, based on jukka/java-unrar): <https://code.google.com/archive/p/java-unrar/>
* commons-compress: <https://commons.apache.org/proper/commons-compress/>

### password_crack(Java)

使用Java语言编写，无界面。使用`zip4j`做暴力尝试。

* password_crack: <https://gitee.com/yymagicer/password_crack>
* zip4j: <https://github.com/srikanth-lingala/zip4j>

### PasswordCrackerMultiThread

使用Java语言编写，无界面。多线程计算枚举密码的hash值。

* PasswordCrackerMultiThread: <https://github.com/olzhabay/PasswordCrackerMultiThread>

### Passwordcracker

使用Java语言编写，无界面。主要是做了一个简单的框子用来做字典密码尝试。

* passwordcracker: <https://github.com/chandra1123/passwordcracker>

### bkcrack/pkcrack

ZIP明文攻击开源软件

* bkcrack: <https://github.com/kimci86/bkcrack>
* pkcrack: <https://github.com/keyunluo/pkcrack>

### qpdf

* <https://github.com/qpdf/qpdf>

### pdfcrack

* pdfcrack: <https://sourceforge.net/projects/pdfcrack/>
* PDFCrack-GUI: <https://github.com/tedsmith/PDFCrack-GUI>

## 闭源密码恢复工具

### Passware Kit Forensic

* <https://www.passware.com/kit-forensic/>

### Passper for XXX

比如Passper for ZIP，支持恢复PDF，RAR，ZIP等文件类型的密码

* <https://passper.imyfone.com/>

另外有几款类似工具，感觉都是`Passper for XXX`魔改了下:

* <https://www.yunjiemi.net/Passper/index.html>
* <https://www.ifindpass.com/zip-password-recovery-online/>

### PDF Password Remover(VeryPDF)

VeryPDF(一家专业处理PDF的公司)研发的PDF密码恢复软件

* <https://www.verypdf.com/app/pdf-password-remover/index.html>

### PDF Password Remover

* <https://www.pdfpasswordremover.com/>

### Rar Password Unlocker

官网已不可访问

* ~~<http://www.passwordunlocker.com/>~~

### Ziperello（Zip Password Recovery Tool）

原名 Turbo ZIP Cracker，自1.4版起更改了软件名，支持暴力破解和字典破解，官网已不可访问。

* ~~<http://www.ziperello.com>~~

### Free Rar Password Recovery

* <https://amazing-share.com/free-rar-password-recovery.html>

### PassFab for XXX

比如PassFab for RAR，支持恢复PDF，RAR，ZIP等文件类型的密码

* <https://www.passfab.com/>

### Accent XXX Password Recovery

比如Accent OFFICE Password Recovery，支持恢复PDF，RAR，ZIP等文件类型的密码

* <https://passwordrecoverytools.com/>

### Advanced XXX Password Recovery

* Advanced Archive Password Recovery(ARCHPR): <https://www.elcomsoft.com/archpr.html>
* Advanced Office Password Recovery(AOPR): <https://www.elcomsoft.com/aopr.html>
* Advanced PDF Password Recovery(APDFPR): <https://www.elcomsoft.com/apdfpr.html>

## 字典

* EroPassword，一些常用的解压密码组成的字典文件：<https://github.com/baidusama/EroPassword>
* 某百度网盘的密码库，提取码1234：<https://pan.baidu.com/s/1gY9I89LHJ3jLTNiMBRZ52g>
* skullsecurity: <https://wiki.skullsecurity.org/index.php/Passwords>
* CrackStation's Password Cracking Dictionary: <https://crackstation.net/crackstation-wordlist-password-cracking-dictionary.htm>
* weakpass: <https://weakpass.com/download>
