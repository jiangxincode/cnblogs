欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

# 背景说明

作为一个团队开发，公司长期以来的实践证明，手工操作版本管理是非常不明智的，一来浪费人力，二来效率低下，三来容易犯错。那么版本管理用什么工具好呢？

在开源世界中，CVS（ConcurrentVersions System）一直都是版本控制的首选。但是现在用户有了另一个选择，就是Subversion(SVN)。SVN是下一代版本控制系统，能替代 CVS，项目主页是http://subversion.tigris.org。

SVN是一个自由、开放源码、跨平台的版本控制系统。它是一个通用系统，可用来管理任何类型的文件，
其中包括程序源码。

它的初始目标很明确，实现绝大部分CVS的已有功能；充分考虑现有的CVS用户，在使用方式上模仿CVS，同时开发了一系列工具，使得基于CVS的项目能够顺利迁移到SVN上。和CVS相比，它有很多优点，例如目录版本控制、不可分割的提交、一致的数据处理方式和更有效率的分支与标记等。

SVN有两种运行方式，一种是基于Apache Http Server，另外一种是SVN Standalone Server。一般推荐使用基于Apache Http Server的SVN，这样做几个好处：

* 能使用WebDAV（Web-based Distributed Authoring and Versioning）协议
* 能使用浏览器作为客户端工具浏览源码仓库
* 可以很容易的支持到SSPI（Security Support Provider Interface，Microsoft安全支持提供器接口即常说的Windows域认证）和LDAP（Lightweight Directory Access Protocol），这些都是Apache本身就支持的
* 能得到比较完善的Apache安全认证系统，比如 SSL加密连接

考虑到公司同事基本上一直都是在Windows下过日子，所以考虑在Windows平台下搭建SVN，并且使用Windows域用户认证的方式管理SVN的权限配置，使用浏览器和TortioseSVN作为SVN的客户端，以进一步降低使用、管理门槛。

# 配置流程

## 安装配置域控制器

我用的是Windows2003企业版，配置域控制器比较简单，就不多说了。

## 安装Apache

到http://httpd.apache.com/下载最新版的Apache For Windows，我使用的版本是apache_2.0.52-win32-x86-no_ssl.exe，安装时选择以Windows服务方式运行。注意如果IIS已在运行，需要先关闭，或者更换端口。安装完成后用浏览器打开http://127.0.0.1/看是否能看到Apache的测试页。

## 安装SubVersion

到http://subversion.tigris.org/下载最新版的SVN，我使用的版本是svn-1.1.4-setup.exe，安装程序会提示将自动修改Apache的配置文件，不要相信它，安装程序自动修改的并不完整，接下来一定要按下面的步骤重新检查配置。

## 配置域用户认证

1、检查modules下是不是已经有了mod_dav_svn.so、mod_authz_svn.so和libdb42.dll三个文件，如果没有表示SVN没有安装正常，需要重新安装
2、打开confhttpd.conf文件
3、在httpd.conf中找到这三行：

```bash
LoadModule dav_fs_modulemodules/mod_dav_fs.so
LoadModule dav_svn_modulemodules/mod_dav_svn.so
LoadModule authz_svn_modulemodules/mod_authz_svn.so
```
把它们前面的注释号#删除

4、到http://tortoisesvn.tigris.org/mod_auth_sspi.zip下载最新版的SSPI模块，我使用的版本是mod_auth_sspi/1.0.1，解开压缩包后把其中的mod_auth_sspi.so文件放到modules目录下
5、在httpd.conf中找到行“LoadModule auth_module modules/mod_auth.so”，在其前一行加入“LoadModule sspi_auth_module modules/mod_auth_sspi.so”
6、现在我们假定要在c:svn目录中存放各种SVN文件库，分别为repos1、repos2…
7、在httpd.conf文件的末尾加上

```
DAV svn
SVNParentPath c:/svn
AuthzSVNAccessFile c:/svn/accessfilesspi
Require valid-user
AuthType SSPI

AuthName "Subversion 文件库"
SSPIAuth On
SSPIAuthoritative On
SSPIDomain owl-2003.owl.local
SSPIOfferBasic On
```

* "DAV svn"表示通过Apache Web Server根目录下的svn子目录可以访问"SVNParentPathc:/svn"中定义的目录下的SVN文件库的内容；
* "AuthzSVNAccessFile c:/svn/accessfilesspi”表示"c:/svn/accessfilesspi"文件中定义了域用户与文件库资源权限控制的详细信息
* "SSPIDomain owl-2003.owl.local"表示在我的机器上域控制器名称为："owl-2003.owl.local"

AuthzSVNAccessFile定义的权限控制文件举例

```shell
#用户分组，以逗号分隔；用户名区分大小写；域用户用全称，即DOMAINUserName
[groups] 
admins = OWLAdministrator
developers = OWLwater 
docs = OWLyouwater
#管理员组拥有所有权限
[/]
@admins= rw
#开发人员可以完全控制源程序
[/myrepos] 
@developers = rw
#文档人员可以完全控制文档
[/docs] 
@docs = rw
```

8、保存httpd.conf，并重启Apache，随便用一个浏览器打开http://127.0.0.1/svn/docs测试一下吧。注意用户名输入是大小写敏感的，域用户需要输入全称。

## 安装TortioseSVN

到http://tortoisesvn.tigris.org/下载最新的TortioseSVN和中文包，我用的版本是TortoiseSVN-1.1.5-UNICODE_svn-1.1.4.exe、
LanguagePack_1.1.5_zh_CN.exe，TortioseSVN与Windows资源管理器集成在一起，重启系统后就可以使用了，首先打开资源管理器，在随意位置点击右键，选择TortioseSVN=>Setting，把语言改为简体中文，确定后生效。

# 参考内容

* Apache管理手册
* Subversion用户手册
* TortioseSVN用户手册