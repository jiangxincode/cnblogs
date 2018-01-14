# VCS(Version Control System)学习之路

## 代码托管网站

* https://github.com/ (Git)
* http://www.gitlab.cc/ (Git)
* https://bitbucket.org/ (Git Mercurial)
* https://sourceforge.net/ (Git Mercurial SVN)
* http://www.codeplex.com/
* https://sourceware.org/
* <del>http://code.taobao.org/</del> (SVN)
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

## SVN

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
* VISUALSVN SERVER // Features // Windows Authentication for Subversion: https://www.visualsvn.com/server/features/windows-auth/

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
* SVN版本库无损迁移与自动备份（一）:http://www.cnblogs.com/springside-example/archive/2011/11/30/2530176.html
* SVN版本库无损迁移与自动备份（二）:http://www.cnblogs.com/springside-example/archive/2011/11/30/2530174.html
* SVN+Apache域用户认证配置方法_Windows(转，重新排版，部分内容更新优化): http://www.cnblogs.com/jiangxinnju/p/5906377.html
* TortoiseSVN,TortoiseGit修改差异查看器为BeyondCompare: http://blog.csdn.net/sanfye/article/details/48028879
* SVN的钩子--限制强制写日志（log）: <http://duchengjiu.iteye.com/blog/1739694>
* svn ignore 的用法（忽略文件及目录）: <http://blog.csdn.net/yhl27/article/details/24318001>
* SVN版本冲突，COMMIT时出现.MINE等文件: <https://www.cnblogs.com/xiezhengcai/archive/2013/06/06/3120931.html>

### 简单教程（详细说明参考前面的教程地址，此处仅为了速查速用）

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

### SVN更新失败，提示locked

产生这种情况大多是因为上次svn命令执行失败且被锁定了，需要删除文件夹中的lock文件，即可解锁。这里介绍3种方法：

* 直接进行cleanup；对较小的文件比较管用，文件稍大些等待时间很长或不起作用；
* 选择文件，右键执行release lock；等待时间较长；
* 手动删除锁定文件：在命令提示符下cd 到svn项目出现问题的文件所在目录下，执行命令del lock /q/s。等待删除lock文件成功，重新更新SVN。

## GIT

安装了git后会附带很多linux下常用的工具，比如ssh,scp,curl,split,cat等，很方便。

* GIT：<http://git-scm.com/>
* Reference：<http://git-scm.com/docs>
* Documentation：<http://git-scm.com/doc>
* Pro Git book: <https://git-scm.com/book/en>

* git for windows：<http://gitforwindows.org/>
* posh-git: <https://github.com/dahlbyk/posh-git>
* SourceTree：https://www.sourcetreeapp.com/
* tortoisegit：https://code.google.com/p/tortoisegit/
* gitlab：https://about.gitlab.com/
* EGit：http://www.eclipse.org/egit/download/

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

* Git Community Book 中文版：<http://gitbook.liuhui998.com/index.html>
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
* Commit message 和 Change log 编写指南：http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html
* Writing a Friendly README: http://rowanmanning.com/posts/writing-a-friendly-readme/
* GitHub Pages + Hexo搭建博客: http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/
* Hexo+Next搭建Github个人静态博客: 	<http://www.cnblogs.com/cnfanhua/p/5167191.html>
* Git教程-分支和tag管理: http://blog.csdn.net/top_code/article/details/52336221
* Publishing a Website on Bitbucket Cloud: https://confluence.atlassian.com/bitbucket/publishing-a-website-on-bitbucket-cloud-221449776.html
* What are the git concepts of HEAD, master, origin? <https://stackoverflow.com/questions/8196544/what-are-the-git-concepts-of-head-master-origin>
* How do I make Git use the editor of my choice for commits?: <https://stackoverflow.com/questions/2596805/how-do-i-make-git-use-the-editor-of-my-choice-for-commits>
* 分支管理策略: <https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758410364457b9e3d821f4244beb0fd69c61a185ae0000>
* Bug分支: <https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137602359178794d966923e5c4134bc8bf98dfb03aea3000>

### git init 与 git init --bare

使用命令"git init --bare"(bare汉语意思是:裸,裸的)初始化的版本库(暂且称为bare repository)只会生成一类文件:用于记录版本库历史记录的.git目录下面的文件;而不会包含实际项目源文件的拷贝;所以该版本库不能称为工作目录(working tree);如果你进入版本目录,就会发现只有.git目录下的文件,而没有其它文件;就是说,这个版本库里面的文件都是.git目录下面的文件,把原本在.git目录里面的文件放在版本库的根目录下面;换句话说,不使用--bare选项时,就会生成.git目录以及其下的版本历史记录文件,这些版本历史记录文件就存放在.git目录下;而使用--bare选项时,不再生成.git目录,而是只生成.git目录下面的版本历史记录文件,这些版本历史记录文件也不再存放在.git目录下面,而是直接存放在版本库的根目录下面。

用"git init"初始化的版本库用户也可以在该目录下执行所有git方面的操作。但别的用户在将更新push上来的时候容易出现冲突。

比如有用户在该目录（就称为远端仓库）下执行git操作，且有两个分支(master 和 b1)，当前在master分支下。另一个用户想把自己在本地仓库（就称为本地仓库）的master分支的更新提交到远端仓库的master分支，他就想当然的敲了

git push origin master:master

于是乎出现因为远端仓库的用户正在master的分支上操作，而你又要把更新提交到这个master分支上，当然就出错了。但如果是往远端仓库中空闲的分支上提交还是可以的，比如

git push origin master:b1

解决办法就是使用”git init –bare”方法创建一个所谓的裸仓库，之所以叫裸仓库是因为这个仓库只保存git历史提交的版本信息，而不允许用户在上面进行各种git操作，如果你硬要操作的话，只会得到下面的错误（”This operation must be run in a work tree”）这个就是最好把远端仓库初始化成bare仓库的原因。

## Mercurial

* Mercurial：https://mercurial.selenic.com/
* mercurialeclipse： https://bitbucket.org/mercurialeclipse/main/wiki/Home
* tortoisehg：http://tortoisehg.bitbucket.org/

## Others

* perforce: https://www.perforce.com/
* CVS：http://www.nongnu.org/cvs/
* bazaar：http://bazaar.canonical.com/en/