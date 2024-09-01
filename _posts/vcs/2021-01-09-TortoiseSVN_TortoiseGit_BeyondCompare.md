---
title: "在TortoiseSVN/TortoiseGit中使用BeyondCompare进行差异对比"
categories:
  - vcs
tags:
  - TortoiseSVN
  - TortoiseGit
  - BeyondCompare
toc: true
---

BeyondCompare支持不同的版本控制系统相关工具，官网说明: <http://www.scootersoftware.com/support.php?zz=kb_vcs>。本文仅针对比较常用的TortoiseSVN/TortoiseGit进行说明

## TortoiseSVN

在资源管理器右键菜单中：`TortoiseSVN-Settings`

* 设置比较不同版本文件的程序，选择`External(外部)`，在下面文本框中填入如下内容，其中前半部分是`BComp.exe`所在目录：

`"C:\Program Files\Beyond Compare 4\BComp.exe" %base %mine /title1=%bname /title2=%yname /leftreadonly`

* 设置读取`GNU patch files`的程序，选择`External(外部)`，在下面文本框中填入`BCompare.exe`所在目录：

`C:\Program Files\Beyond Compare 4\BCompare.exe`

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210109113438890-50940543.png)

* 设置解决文件冲突的程序,选择`External(外部)`，在下面文本框中填入如下内容，其中前半部分是`BComp.exe`所在目录：

`"C:\Program Files\Beyond Compare 4\BComp.exe" %mine %theirs %base %merged /title1=%yname /title2=%tname /title3=%bname /title4=%mname`

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210109113449706-495206858.png)

操作完成后点击确定结束。

## TortoiseGit

在资源管理器右键菜单中：`TortoiseGit-Settings`，后续操作步骤和`TortoiseSVN`相同:
![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210109113503069-903682193.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/611264-20210109113508634-1811462627.png)
