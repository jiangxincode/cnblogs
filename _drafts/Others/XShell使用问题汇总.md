## XShell使用问题汇总

Xshell是一款公认的优秀SSH连接管理软件，被广泛用于管理Linux服务器或VPS。

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