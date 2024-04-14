欢迎关注我的社交账号：


博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju


astyle是一款代码格式化工具，它的下载地址是：
http://sourceforge.net/projects/astyle

项目地址：
http://astyle.sourceforge.net/

文档说明：
http://astyle.sourceforge.net/astyle.html

## 基本命令

`astyle --style=ansi main.cs`

## 格式化目录

使用ansi风格格式当前目录下的所有cpp,cs文件，注意在批处理文件时，"%f" 要改为"%%f"

`for /R %f in (*.cpp;*.cs;) do astyle --style=ansi "%f"`

## 参数说明：

http://astyle.sourceforge.net/astyle.html


## 加入到VS2008,VS2005

+ 工具——>外部工具——>添加
+ 标题：astyle 
+ 命令：AStyle.exe （填好astyle.exe的路径）
+ 参数：--style=allman -N $(ItemDir)$(ItemFileName)$(ItemExt)
+ 初始目录：$(TargetDir)
+ 勾上“使用初始目录”
+ 点击确定完成，以后就可以在工具菜单中找到“astyle“这一项了，点击它，就可以对当前文件进行格式化操作。

## 加入到VS6

+ Tools——>Customize——>Tools
+ 标题：astyle 
+ 命令：AStyle.exe （填好astyle.exe的路径）
+ 参数：--style=ansi -s4 --suffix=.orig $(FileName)$(FileExt)
+ 初始目录：$(FileDir)
+ 勾上“Using Output Window”
+ 点击确定完成。以后就可以在工具菜单中找到“astyle“这一项了，点击它，就可以对当前文件进行格式化操作。

## 加入到Ultraedit和UltraStudio

+ 高级-->工具配置——>外部工具——>添加
+ 命令：AStyle.exe -v --style=ansi -s4 --suffix=.orig "%f"（填好astyle.exe的路径）
+ Optiones：选择 Windows program和Save Active File.
+ Output: 选择output to list box,show dos box 和no replace。
+ 点击确定完成。以后就可以在工具菜单中找到“astyle“这一项了，点击它，就可以对当前文件进行格式化操作。

## 加入到Source insight

+ Options-->Custom Command-->Add
+ Command：astyle
+ Run "D:\soft\astyle\astyle.exe" --style=ansi  -f  -p -P -U -v -n -N  %f（填好astyle.exe的路径）
+ Output：不选.
+ Control: 选择pause when done和exit to window.
+ source links in output:file, then line
+ -->menu
+ add to work menu.
+ 点击确定完成。以后就可以在Work菜单中找到“astyle“这一项了，点击它，就可以对当前文件进行格式化操作。

另外可以参考：在source insight中集成astyle: <https://www.cnblogs.com/xuxm2007/archive/2013/04/06/3002390.html>

## 控制台目录批处理(astyle.bat)

```Bash
REM 批量将本目录中的所有C++文件用Astyle进行代码美化操作
REM 设置Astyle命令位置和参数
@echo off
set astyle="astyle.exe"
REM 循环遍历目录
for /r . %%a in (*.cpp;*.c) do %astyle% --style=ansi --pad=oper --unpad=paren -s4 -n "%%a"
for /r . %%a in (*.hpp;*.h) do %astyle% --style=ansi --pad=oper --unpad=paren -s4 -n "%%a"
REM 删除所有的astyle生成文件
for /r . %%a in (*.orig) do del "%%a"
pause
```