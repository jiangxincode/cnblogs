BeyondCompare支持不同的版本控制系统相关工具，官网说明: <http://www.scootersoftware.com/support.php?zz=kb_vcs>。本文仅针对比较常用的TortoiseSVN/TortoiseGit进行说明

## TortoiseSVN

在资源管理器右键菜单中：TortoiseSVN-Settings

1. 设置比较不同版本文件的程序，选择External(外部)，在下面文本框中填入如下内容，其中前半部分是BComp.exe所在目录：
`"C:\Program Files\Beyond Compare 4\BComp.exe" %base %mine /title1=%bname /title2=%yname /leftreadonly`

2. 设置读取GNU patch files的程序，选择External(外部)，在下面文本框中填入BCompare.exe所在目录：
`C:\Program Files\Beyond Compare 4\BCompare.exe`

![](https://img2020.cnblogs.com/blog/611264/202101/611264-20210109113438890-50940543.png)

3. 设置解决文件冲突的程序,选择External(外部)，在下面文本框中填入如下内容，其中前半部分是BComp.exe所在目录：
`"C:\Program Files\Beyond Compare 4\BComp.exe" %mine %theirs %base %merged /title1=%yname /title2=%tname /title3=%bname /title4=%mname`

![](https://img2020.cnblogs.com/blog/611264/202101/611264-20210109113449706-495206858.png)

操作完成后点击确定结束。

## TortoiseGit

在资源管理器右键菜单中：TortoiseGit-Settings，后续操作步骤和TortoiseSVN相同:
![](https://img2020.cnblogs.com/blog/611264/202101/611264-20210109113503069-903682193.png)

![](https://img2020.cnblogs.com/blog/611264/202101/611264-20210109113508634-1811462627.png)
