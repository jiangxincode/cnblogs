欢迎关注我的社交账号：

博客园地址: http://www.cnblogs.com/jiangxinnju/p/4781259.html
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

eclipse插件在线发布发布和版本更新(web site)

在eclipse插件开发过程中免不了要发布1.0, 1.1, 1.2…….等等，随着版本的递增，假如每次都发布一个插件zip包，那使用者就想骂街了，每次都要先uninstall，然后install，中间还要两次eclipse的重启。

一般第三方插件会有2中形式共developer使用，一种是发布zip包，另一种是发布一个web site，eclipse对web site的支持相当好。Install时只需copy插件资源的URL（插件的update site）即可获取插件资源进行安装。之后有版本更新时，用户只需点击update按钮即可更新。So easy

做为 developer，下面来说说eclipse 插件 web site 的发布

Web site 的发布

要发布web site，首先要为插件项目创建Feature Project 和 Update Site Project，对这个不太清楚的朋友可以看下我的上一篇文章“eclipse plugin 导出插件包”这边已经准备好了一个Update Site Project
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193557885-957250712.png)




既然是web，那必须创建一个web服务器，比如Apache或者Tomcat。。。

用着方便，我在本地部署了一个Apache服务器（对web服务器的使用不熟悉的可以另找机会或者来信沟通）

Apache服务搭建完成之后，把Update Site Project整个工程都copy到Apache下可访问的目录中（对eclipse来说，实质是要Update Site Project下的5个File）。

发布服务完成之后的效果
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193618198-1845688740.png)




OK，其实已经完成了，把地址copy一下，丢给人家就搞定了，不过现在演示，用的localhost，发布记得要把IP改成可访问的静态IP。

送佛送到西，演示一下安装吧。
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193630276-563734592.png)




一路Next,搞定。

插件安装完成之后
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193646495-1045213878.png)

![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193704448-313766334.png)






很高兴的看到插件安装后的结果。仔细看下版本是1.1.0

Web site 发布更新

当我们想把1.1.0的版本升级到1.2.0的时候，很简单，只需要发布一个1.2.0的web site即可，然后使用者只需要点一下上图中的Update按钮就可以做插件更新，下面具体说说。

注意：插件版本更新需要更新几个文件（还没有找到一次更新多个文件的方式）

1. 插件本身的plugin.xml文件
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193723854-207450760.jpg)




2. Feature Project中feature.xml文件

Overview编辑器中

![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193739073-588027991.jpg)



Plug-ins编辑器中
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193748464-1584151231.jpg)




3. Feature Project下category.xml文件

修改前：
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193818464-1056678984.jpg)




修改后：
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193823651-997096172.jpg)




4. Update Site Project 中 site.xml 文件

在这个文件中修改完Feature后记得要再次Build，否则前功尽弃
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193834104-222443008.jpg)




到此为止，版本修改完成，并且Update Site Project 已经Build完成。

按照 Web Site 发布的步骤再把之前发布的几个文件替换掉

注意：URL不能改变，否则用户无法直接做Update

插件更新的演示

回到之前插件安装完成后的窗口
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193850698-1980311310.png)




选中需要更新的插件，点击Update按钮。
![](http://images2015.cnblogs.com/blog/611264/201601/611264-20160102193904323-1675695507.png)




看到1.2.0的新版本了吧，OK，一路Next。搞定。

通过Web Site发布eclipse插件版本，应该是现在比较流行的方式。

以上这些方式都是个人在开发过程中根据当前需要，不断尝试得到的。如有更好的或者更简便的方法，欢迎来信沟通分享。