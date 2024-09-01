## XShell使用问题汇总

Xshell是一款公认的优秀SSH连接管理软件，被广泛用于管理Linux服务器或VPS。

## 解决xshell中vim显示中文乱码的问题
打开一个用utf8编码的中文文件，在vim中，执行`set encoding=utf-8 termencoding=gbk fileencoding=utf-8`后可正常显示中文。`encoding`是设置档案的当前编码。`termencoding`是用于vim屏幕的显示编码，由于xshell默认用于显示屏幕的编码是gbk,所以此处设置为gbk。同理，假设你修改了xshell的默认编码为utf-8，那么此处自然应该utf-8。`fileencoding`档案保存时的编码，此编码应和encoding保持一致，否则会弹出警告
至于xshell，打开`file->Properties`，点击`Terminal`节点，修改`Terminal Type`为linux(键盘映射模式，默认为xtrem，此种模式下对于vim小键盘输入数字会出现乱字符号)，修改Encoding为uft-8(一般情况下linux系统采用此编码，可用locale命令查看自己系统的默认编码，修改为一致的就行)。
同理，也可以修改xftp的编码为utf-8以正常显示中文。

## Xshell利用登录脚本从服务器登录到另外一个服务器
通过脚本设置，可以实现从这个服务器登录到另外一个服务器。打开Xshell 4的会话属性（【文件】->【属性】），左边的类别下选择【登录脚本】，在右边底下你可以看到有个【连接会话是运行脚本】的复选框。

![](http://images2015.cnblogs.com/blog/611264/201702/611264-20170207235057041-2128114645.png)

登录脚本的格式如下： 
```VBS
Sub Main
	xsh.Screen.Send "ssh 用户名@服务器地址"
	xsh.Screen.Send VbCr
	xsh.Screen.WaitForString "password: "
	xsh.Screen.Send "登录密码"
	xsh.Screen.Send VbCr
End Sub
```
将上面内容保存成一个vbs后缀的文件（最好保存到Xshell安装文件下面），准备好脚本文件后在Xshell中打开

会话属性，勾选【连接会话是运行脚本】这个复选框，选择刚才保存的那个vbs后缀的文件就可以了。

如果想进一步了解Xshell支持的脚本API，可以查看Xshell的帮助文档：

![](http://images2015.cnblogs.com/blog/611264/201702/611264-20170207235214151-52018514.png)