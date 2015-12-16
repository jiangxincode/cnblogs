# 代码托管网站:

* https://github.com/ (Git)
* http://www.gitlab.cc/ (Git)
* https://bitbucket.org/ (Git Mercurial)
* https://sourceforge.net/ (Git Mercurial SVN)
* http://www.codeplex.com/
* http://code.taobao.org/ (SVN)
* http://git.oschina.net/
* http://www.javaforge.com (Git Mercurial SVN)
* http://unfuddle.com
* https://riouxsvn.com/ (SVN)
* http://svn.jundie.net/
* http://www.svnchina.com/index.php
* http://code.svnspot.com/
* <del>http://code.google.com/</del>
* <del>http://svn.coollittlethings.com/index.php</del>
* <del>http://www.svnhost.cn/</del> (SVN)
* <del>http://www.chinasvn.com</del> (SVN)


# SVN

## 项目地址：

* 原项目地址，现在仍保留：http://subversion.tigris.org/
* 现在：http://subversion.apache.org/
* 安装包下载地址：http://subversion.apache.org/packages.html
* subclipse: http://subclipse.tigris.org/
* Subversive - SVN Team Provider: http://marketplace.eclipse.org/content/subversive-svn-team-provider
* CVS Team Provider: http://mvnrepository.com/artifact/org.eclipse.team.cvs
* Windows Command Line客户端推荐Win32Svn：http://sourceforge.net/projects/win32svn/
* Windows GUI客户端推荐TortoiseSVN：http://tortoisesvn.net/
* Linux GUI客户端推荐RabbitVCS：http://rabbitvcs.org/
* SVNKit：http://www.svnkit.com/index.html


## 教程地址：

* Subversion 与版本控制：http://svnbook.red-bean.com/
* TortoiseSVN：http://tortoisesvn.net/docs/release/TortoiseSVN_en/index.html
* TortoiseSVN命令行：http://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-automation.html
* 设置SVN忽略文件和目录（文件夹）: http://blog.csdn.net/hemingwang0902/article/details/6904205
* Google项目托管及Visual Studio 2008的SVN插件AnkhSVN的使用：http://blog.csdn.net/net_lover/article/details/4056916
* 本地搭建SVN局域网服务器：http://blog.csdn.net/sunbaigui/article/details/8466310
* windows下配置VisualSVN Server服务器(服务端和客户端)：http://myfturemydream.blog.163.com/blog/static/85763140200911243408286/
* 使用svn——项目的目录布局：http://www.cnitblog.com/stomic/archive/2008/03/17/41043.html
* 如何结合使用 Subversion 和 Eclipse：http://www.ibm.com/developerworks/cn/opensource/os-ecl-subversion/
* Eclipse + SVN + Google code搭建代码仓库：http://convolute.iteye.com/blog/564247
* MyEclipse使用总结——MyEclipse10安装SVN插件: http://www.cnblogs.com/xdp-gacl/p/3497016.html


## 简单教程（详细说明参考前面的教程地址，此处仅为了速查速用）

以Win32SVN为例，在前面所列的地址中下载Win32SVN客户端并进行安装。安装好后，bin目录下就是相应程序了。通过添加环境变量的方式，把bin目录添加到path。启动cmd，敲入 svn help 以确认是否安装成功。现在可以找到你的代码，做checkout了。在commit代码的过程中，经常会出现的一个问题是：

    svn: None of the environment variables SVN_EDITOR, VISUAL or EDITOR is set, and no 'editor-cmd' run-time configuration option was found

这表示你的系统，没有指定svn客户端通过什么样的文本编辑器来写提交的注释。我们添加环境变量，SVN_EDITOR的值为notepad。再次svn ci 代码。notepad弹出了，写完注释保存。代码提交！

注册环境变量SVN_EDITOR为"E:\Program Files\Vim\vim71\gvim.exe"，结果在svn ci的时候，出现错误:

    'E:\Program' 不是内部或外部命令，也不是可运行的程序或批处理文件。
    svn: 提交失败(细节如下):
    svn: system('E:\Program Files\Vim\vim71\gvim.exe svn-commit.tmp') 返回 1

把SVN_EDITOR改为"gvim.exe"，并且在path中添加路径"E:\Program Files\Vim\vim71",这样就可以在提交的时候用vim编写注释了。

如果你不知道命令怎么用svn命令,可通过如下方式查询：

    svn help

知道了子命令，但是不知道子命令的用法，还可以查询：

    svn help ci 

导入项目

    svn import http://svn.chinasvn.com:82/pthread --message "Start project"

导出项目

    svn checkout http://svn.chinasvn.com:82/pthread

采用 export 的方式来导出一份“干净”的项目

    svn export http://svn.chinasvn.com:82/pthread pthread

为失败的事务清场

    svn cleanup

在本地进行代码修改，检查修改状态

    svn status -v
    svn diff

更新(update)服务器数据到本地

    svn update directory
    svn update file

增加(add)本地数据到服务器

    svn add file.c
    svn add dir

取消svn add

    svn revert --recursive dir

对文件进行改名和删除

    svn mv b.c bb.c
    svn rm d.c
    svn rm dir --keep-local

提交(commit)本地文档到服务器

    svn commit
    svn ci
    svn ci -m "commit"

查看日志

    svn log directory
    svn log file


## svn ignore的用法

若想创建了一个文件夹，并且把它加入版本控制，但忽略文件夹中的所有文件的内容：

    svn mkdir spool 
    svn propset svn:ignore '*' spool 
    svn ci -m 'Adding "spool" and ignoring its contents.'

若想创建一个文件夹，但不加入版本控制，即忽略这个文件夹：

    mkdir spool 
    svn propset svn:ignore 'spool' . 
    svn ci -m 'Ignoring a directory called "spool".'

若已经创建了文件夹，并加入了版本控制，现在想忽略这个文件夹，但要保持文件夹的内容：

    svn export spool spool-tmp 
    svn rm spool 
    svn ci -m 'Removing inadvertently added directory "spool".' 
    mv spool-tmp spool 
    svn propset svn:ignore 'spool' . 
    svn ci -m 'Ignoring a directory called "spool".'

如果想在SVN提交时，忽略某个文件，也就是某个文件不提交，可以使用

    svn propedit svn:ignore 目录名称

注意，在使用这个SVN的属性编辑前，你得确保后面的“目录名称”是SVN版本控制的目录。如果要忽略此目录下的文件，可以如下操作。比如，想忽略/product目录下的test.php文件。前提是/product目录必须在svn版本控制下，而test.php文件不在svn版本控制。svn st先看一下状态，会显示如下：

    ?     /product/test.php

我们需要将test.php文件加入忽略列表。此时先设置SVN默认的编辑器

    export SVN_EDITOR=vim

然后：

    svn propedit svn:ignore /product

此时会出现一个VIM的编辑窗口，表示需要将某个文件加入到忽略列表里。我们在编辑窗口中，写入test.php。然后保存，并退出VIM编辑器。这时候会有一个提示：

    属性 “svn:ignore” 于 “product” 被设为新值。

表示文件test.php的svn:ignore属性设置成功。然后使用svn st查看，会显示：

    M        product

我们需要提交，然后这个svn:ignore属性才会起作用

    svn ci -m '忽略test.php文件'

这时候，无论你如何修改test.php文件，再使用svn st时，也不会出现修改提示符合M了。

## SVN更新失败，提示locked

产生这种情况大多是因为上次svn命令执行失败且被锁定了，需要删除文件夹中的lock文件，即可解锁。这里介绍3种方法：

* 直接进行cleanup；对较小的文件比较管用，文件稍大些等待时间很长或不起作用；
* 选择文件，右键执行release lock；等待时间较长；
* 手动删除锁定文件：在命令提示符下cd 到svn项目出现问题的文件所在目录下，执行命令del lock /q/s。等待删除lock文件成功，重新更新SVN。


## SVN版本冲突，commit时出现.mine等文件

以commit后自动生成R.java.mine，R.java.r3368，R.java.r3439为例。因为发生冲突了，别人和你都从3368这个版本对r.java这个文件进行了修改，别人修改后先提交了形成3439版本，然后你做了提交操作，这时为了避免你覆盖别人的修改工作，SVN提示你发生了冲突，并自动形成R.java.mine、R.java.r3368、R.java.r3439这三个文件。其中：

* R.java.mine 你自己修改后准备提交的那个版本；
* R.java.r3368 你们的初始版本；
* R.java.r3439 别人在你之前提交的那个版本；
* R.java 自动合并了你的版本和别人提交的版本形成的（其中用<<<<<、======、>>>>>等符号标记出了自动合并的部分）。

自动生成这些文件的目的是便于你手动合并你们两个人的修改。这时建议你查看一下这个文件的历史记录，看看3439这个版本是谁提交的，问问他修改了什么地方，然后你手动将你们两个人的修改合并到同一个文件r.java中，然后使用SVN标记“冲突已解决”，标记后多余的文件会被自动删除，然后你就可以正常提交了。


##  SVN的钩子--限制强制写日志

SVN本身并不提供这种强制写log的功能，而是通过一系列的钩子程序(我们称为hook脚本)，在提交之前(pre-commit)，提交过程中(start-commit)，提交之后(post-commit)，调用预定的钩子程序来完成一些附加的功能。本次我们要实现的是在提交到版本库之前检查用户是否已经写了注释，当然要使用pre-commit这个钩子程序。我们打开SVN的repository下的hook目录，可以发现有好几个文件，其中一个是“pre-commit.tmpl”。这个文件是一个模板文件，它告诉了我们如何实现提交前控制。打开该模板文件，我们看到如下一段说明：

```shell
    # The pre-commit hook is invoked before a Subversion txn is
    # committed.   Subversion runs this hook by invoking a program
    # (script, executable, binary, etc.) named 'pre-commit' (for which
    # this file is a template), with the following ordered arguments:
    #
    #    [1] REPOS-PATH    (the path to this repository)                             
    #    [2] TXN-NAME      (the name of the txn about to be committed) 
    #
    # The default working directory for the invocation is undefined, so
    # the program should set one explicitly if it cares.
    #
    # If the hook program exits with success, the txn is committed; but
    # if it exits with failure (non-zero), the txn is aborted, no commit
    # takes place, and STDERR is returned to the client.    The hook
    # program can use the 'svnlook' utility to help it examine the txn.
```

我们看到在一个提交事务执行之前，该hook脚本会被调用。然后向该脚本传递两个参数：REPOS-PATH和TXN-NAME，一个是用户要提交的URL，一个是本次事务的一个事务号。如果提交成功则返回0，否则返回其它非0结果。那么我们的钩子程序就是要在事务提交之前，拦截这些请求，然后通过svnlook命令来检查是否已经写了log。示例代码：

```shell
    REPOS="$1"
    TXN="$2"
    # Make sure that the log message contains some text.
    SVNLOOK=/usr/bin/svnlook
    LOGMSG=$($SVNLOOK log -t "$TXN" "$REPOS" | \
       grep "[a-zA-Z0-9]" | wc -c)
    if [ "$LOGMSG" -lt 48 ]; then
    #-eq 等于号  -gt 大于号   -lt小于号  ，显示输入的长短为10(如果数字或者字母表示最少要写9个，如果汉字是一个根据自己的需求可以任意修改
            echo -e "\n至少输入4个汉字" >&2
            exit 1
    fi
    exit 0
```


# GIT

## 项目地址：

* GIT：http://git-scm.com/
* git for windows：https://git-for-windows.github.io/
* SourceTree：https://www.sourcetreeapp.com/
* tortoisegit：https://code.google.com/p/tortoisegit/
* gitlab：https://about.gitlab.com/

* http://githuber.info/index

* Travis CI: https://travis-ci.org/
* appveyor: https://ci.appveyor.com/
* codeclimate: https://codeclimate.com/
* GITTER: https://gitter.im/home
* Waffle: https://waffle.io/
* bitdeli: https://bitdeli.com/
* COVERALLS: https://coveralls.io/
* COVERITY: https://scan.coverity.com/
* choosealicense: http://choosealicense.com/

## 教程地址：

* Reference：http://git-scm.com/docs
* http://git-scm.com/docs/gitignore
* Documentation：http://git-scm.com/doc
* Git book：http://git-scm.com/book/zh/
* Pro Git book（修改自上面）：https://git-reference.readthedocs.org/en/latest/
* Git Community Book 中文版：http://gitbook.liuhui998.com/index.html
* Permanently remove files and folders from Git repo：http://dalibornasevic.com/posts/2-permanently-remove-files-and-folders-from-a-git-repository
* git/github初级运用自如：http://www.cnblogs.com/fnng/archive/2012/01/07/2315685.html
* windows中使用Git工具连接GitHub(配置篇)：http://www.cnblogs.com/sorex/archive/2011/08/10/2132359.html
* 详解在visual studio中使用git版本系统(图文)：http://www.cnblogs.com/wojilu/archive/2011/11/16/2250721.html
* git 把文件从版本管理中移除：http://blog.sina.com.cn/s/blog_59fb90df0101980a.html
* git乱码解决方案汇总：http://zengrong.net/post/1249.htm
* git pull 和本地文件冲突问题解决：http://my.oschina.net/u/554046/blog/308614
* 打造完美 Windows git 命令行环境：http://www.v2ex.com/t/154202
* Remove sensitive data：https://help.github.com/articles/remove-sensitive-data/
* Caching your GitHub password in Git：https://help.github.com/articles/caching-your-github-password-in-git/
* github使用指南：https://github.com/NeuOL/neuola-legacy/wiki/github使用指南
* github创建tag: http://caibaojian.com/github-create-tag.html

## install

* ubuntu:
    sudu apt-get install git
* windows:
    http://git-scm.com/
    https://github.com/dahlbyk/posh-git

安装了git后会附带很多linux下常用的工具，比如ssh,scp,curl,split,cat等，很方便。

## git项目暂停开发注意事项 

每次项目暂时结束时，整理工程目录中的文件；保证所有更改均提交到服务器，无本地更改；将本地工程目录压缩；当再次开启该工程时，先从github上clone到本地，解压缩本地文件，对比一些特殊目录，添加必要文件，从新开启该工程。

## git init 与 git init --bare

使用命令"git init --bare"(bare汉语意思是:裸,裸的)初始化的版本库(暂且称为bare repository)只会生成一类文件:用于记录版本库历史记录的.git目录下面的文件;而不会包含实际项目源文件的拷贝;所以该版本库不能称为工作目录(working tree);如果你进入版本目录,就会发现只有.git目录下的文件,而没有其它文件;就是说,这个版本库里面的文件都是.git目录下面的文件,把原本在.git目录里面的文件放在版本库的根目录下面;换句话说,不使用--bare选项时,就会生成.git目录以及其下的版本历史记录文件,这些版本历史记录文件就存放在.git目录下;而使用--bare选项时,不再生成.git目录,而是只生成.git目录下面的版本历史记录文件,这些版本历史记录文件也不再存放在.git目录下面,而是直接存放在版本库的根目录下面。

用"git init"初始化的版本库用户也可以在该目录下执行所有git方面的操作。但别的用户在将更新push上来的时候容易出现冲突。

比如有用户在该目录（就称为远端仓库）下执行git操作，且有两个分支(master 和 b1)，当前在master分支下。另一个用户想把自己在本地仓库（就称为本地仓库）的master分支的更新提交到远端仓库的master分支，他就想当然的敲了

git push origin master:master

于是乎出现因为远端仓库的用户正在master的分支上操作，而你又要把更新提交到这个master分支上，当然就出错了。但如果是往远端仓库中空闲的分支上提交还是可以的，比如

git push origin master:b1

解决办法就是使用”git init –bare”方法创建一个所谓的裸仓库，之所以叫裸仓库是因为这个仓库只保存git历史提交的版本信息，而不允许用户在上面进行各种git操作，如果你硬要操作的话，只会得到下面的错误（”This operation must be run in a work tree”）这个就是最好把远端仓库初始化成bare仓库的原因。 


# Others

* CVS：http://www.nongnu.org/cvs/
* Mercurial：https://mercurial.selenic.com/
* tortoisehg：http://tortoisehg.bitbucket.org/
* bazaar：http://bazaar.canonical.com/en/
