# Vim学习之路

## vim如何删除某行至某行之间的内容？

删除3104至5403行之间的内容:

    :3104,5403d

## vim使光标始终在屏幕中央

* zz是卷页面使光标到中间
* M是移动光标到中间
* :set scrolloff=10 可以让光标一直在中间，调整数的大小可以控制区域

## vim的列编辑操作

* 删除列：光标定位到要操作的地方。CTRL+v 进入“可视 块”模式，选取这一列操作多少行。d 删除。
* 插入列：例如我们在每一行前都插入"() "：光标定位到要操作的地方。CTRL+v 进入“可视块”模式，选取这一列操作多少行。SHIFT+i(I) 输入要插入的内容。ESC 按两次，会在每行的选定的区域出现插入的内容。

## 利用vim查询函数用法

当光标处在函数名称时：按K即可进入函数说明（相当于man），也可以使用nK制定man的级别

## vim跨文件复制

* 打开一个文件，在该文件下复制几行到另一个文件（如到test.txt），会覆盖test.txt中的内容

    10,100w!test.txt

* 在该文件下复制几行到另一个文件，但不会覆盖原内容，即追加

    10,100w!>>test.txt

* 在一个文件中复制几行到缓冲区

    "anyy

* 在另一个文件中粘贴

    "ap

## 解决往vim里粘贴格式散乱 

有时候从编辑器里面复制粘贴代码到vim中，代码格式会完全乱套。其原因是vim开启了smartindent(智能缩减)或autoindent(自动对齐)模式。为了保持代码的格式，在粘贴前可以先停止上面的两种模式，命令为：

    :set nosmartindent
    :set noautoindent

为了一个粘贴搞出这么多事来，确实是麻烦。不过还有一个更加简单的方法，用命令开始粘贴模式，即： 

    :set paste

粘贴

:set nopaste 或者:set paste!

由于粘贴模式和上面的smartindent、autoindent模式是互斥的，而smartindent是不可少的，所以粘贴完后使用上面的两条命令之一来关闭粘贴模式。

另外还可以通过绑定自定义快捷键的方式来快速切换，例如将下属配置加入到.vimrc中

方式1：

set pastetoggle=<F4>

方式2：

:map <F8> :set paste

:map <F9> :set nopaste

注意：方式1在阅读和编辑模式下都可以使用，对粘贴模式开启和关闭进行切换；方式2是在阅读模式下使用，按下相应的快捷键就相当于执行后面定义的命令。

## 解决在insert模式下面backspace键无法删除的问题

vim 在插入模式下<BS>有几种工作方式，默认是设置成vi兼容，这样就会出现无法删除此次插入前文字的情况。执行以下命令即可：

:set backspace=indent,eol,start

或者：

set nocompatible

## vim 替换

* :0,$s/^/#/gc “ 在行首加一个#号
* :6,10s/^/#/gc “在6~10行的行首加一个#号
* :%s/^ *//g “删除行首的空格
* :%s/ *$//g “删除行尾的空格
* :%s/^\n//g “删除空行
* :g/^s*$/d “ 删除空行

## Vim局部排序

如果我们想以第4列数据进行排序，可以在vim中如此做：

1,12!sort -r -n -k4.1,5

* -r 降序排序
* -n 按数字大小排序
* -k,表示根据那个字段排序，4.1,表示第4列第一个字符开始 ，5表示到第5个字段为结束
* -t 后面跟分隔符，缺省是空格

在VIM里面, 如果你要把从当前行以下20行按字母顺序排序

.,+20!sort

## 同时打开、显示多个文件

vim还没有启动的时候：在终端里输入 

    vim file1 file2 ... filen

vim已经启动，输入

    :open file

同时显示多个文件：

:split

:vsplit

在文件之间切换：

1.文件间切换

Ctrl+6—下一个文件

:bn—下一个文件

:bp—上一个文件

对于用(v)split在多个窗格中打开的文件，这种方法只会在当前窗格中切换不同的文件。

2.在窗格间切换的方法

* Ctrl+w+方向键——切换到前／下／上／后一个窗格
* Ctrl+w+h/j/k/l ——同上
* Ctrl+ww——依次向后切换到下一个窗格中

## 用vim修改文件编码为utf-8 

网页常常会出现乱码的情况，一般都是编码设置不对造成的。例如一个网页源文件的编码不是utf8的，但声明为utf8<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />网页就会出现乱码。可以用vim修改源文件编码为utf8，

命令是 :set fileencoding=utf-8

如果用vim打开文件时里面有乱码，可能用上面的命令修改文件后无法保存。可以用其他软件打开文件，然后把内容拷贝到vim里再保存就行了。

## gvim编码配置 

Vim / gVim 在中文 Windows 下的字符编码有两个问题：

默认没有编码检测功能

如果一个文件本身采用的字符集比 GBK 大（如 UTF-8、UTF-16、GB18030），那么其中无法在 GBK 中对应的字符都会出现乱码，保存时会丢失。即使编辑文件时正确检测出文件格式也无济于事。

第一个问题的解决办法是在 ~/.vimrc 中加入以下配置：

set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1

第二个问题的解决办法是强制要求 Vim 的内部编码采用某种 UTF 编码。比如 UTF-8：

set encoding=utf-8

但是，把 Vim 的内部编码设为 UTF-8 会带来以下新问题

使用非 GUI 界面的 vim 时会乱码 

提示信息（比如E492: 不是编辑器的命令: foo）会乱码 

要解决非 GUI 界面的 vim 的乱码问题，需要设置终端编码为系统默认编码：

set termencoding=cp936

而要让提示信息不乱码则要需要使用 UTF-8 版本的提示信息：

language messages zh_CN.UTF-8

综上所述，在中文 Windows 下正确配置字符编码，需要把以下内容加入你的 ~/.vimrc 中

```
    set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1
    set encoding=utf-8
    set termencoding=cp936
    language messages zh_CN.UTF-8
```

## What is the <leader> in a .vimrc file?

:help leader

## ctags的安装

ctags工具是用来遍历源代码文件生成tags文件，这些tags文件能被编辑器或其它工具用来快速查找定位源代码中的符号（tag/symbol），如变量名，函数名等。比如，tags文件就是Taglist和OmniCppComplete工作的基础。

sudo apt-get install ctags

在程序的根目录下运行ctags -R，生成tags文件，然后在编辑程序时按Ctrl+]就会跳转到当前光标所在东西的定义处。若有多个tag，执行:ts，进行选择。按Ctrl+o即可跳回。不过，当修改过代码后，需要重新生成tags。

## VIM重新载入文件   .

有时候要使用VIM打开了一些文件，但是在其他地方把次文件改动了，例如使用git进行checkout等操作，需要重新载入此文件。

1 重新载入当前文件：

:e

:e! #放弃当前修改，强制重新载入

2 重新载入所有打开的文件：

:bufdo e 或者 :bufdo :e!

:bufdo命令表示把后面的命令应用到所有buffer中的文件。

## 大小写转换

　　vim中大小写转化的命令是：gu或者gU，形象一点的解释就是小u意味着转为小写，大U意味着转为大写。接下来说明对这两个命令的限定（限定操作的行，字母，单词）等等。

整篇文章大写转化为小写

打开文件后，无须进入命令行模式。

键入:ggguG

解释一下：ggguG分作三段gg gu G

* gg=光标到文件第一个字符
* gu=把选定范围全部小写
* G=到文件结束

整篇文章小写转化为大写

打开文件后，无须进入命令行模式。

键入:gggUG

解释一下：gggUG分作三段gg gU G

*gg=光标到文件第一个字符
*gU=把选定范围全部大写
*G=到文件结束

只转化某个单词

guw 、gue、gUw、gUe

这样，光标后面的单词便会进行大小写转换

想转换5个单词的命令如下：

gu5w、gu5e、gU5w、gU5e

转换几行的大小写

将光标定位到想转换的行上，键入：1gU

从光标所在行往下一行都进行小写到大写的转换

10gU，则进行11行小写到大写的转换

以此类推，就出现其他的大小写转换命令

* gU0 ：从光标所在位置到行首，都变为大写
* gU$ ：从光标所在位置到行尾，都变为大写
* gUG ：从光标所在位置到文章最后一个字符，都变为大写
* gU1G ：从光标所在位置到文章第一个字符，都变为大写

## vim脚本

* map
* re: reduce 被映射的序列被递归映射
* i: insert
* n: normal
* no: no

## vim7.4的python相关配置

这里只讨论官方提供的windows版本的安装文件对python的支持配置,至于自己编译vim的情况,一般都很清楚python如何配置了,不在此讨论.

官方提供的gvim安装文件默认是支持python和python3两种模式的,编译时带有该选项,但并没有附带对应的运行库和运行环境.所以在本地没有安装python时直接在vim中执行

    :py echo "ABCDE"

会提示无法加载python27.dll, 针对于这种情况,请到官方下载 windows 版本的 32位 的python 2.7.x 安装文件. 使用64位的python无法正常在gvim中使用.

python3.x系列在某些vim相关插件中仍不支持,所以依旧推荐使用2.7.x

