欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: http://www.cnblogs.com/jiangxinnju
GitHub地址: https://github.com/jiangxincode
知乎地址: https://www.zhihu.com/people/jiangxinnju

以Windows 10 + Android Studio 3.0.1为例

默认情况下，在Android Studio中将鼠标移动到函数位置处无法显示悬浮提示，需要进行如下设置：

`File -> Settings -> Editor -> General` 选中`Show quick documentation on mouse move` 点击`OK`

但是此时如果将鼠标移动到函数位置处，会显示"fetching documentation"，如果你网络比较好的话，等一会后会显示文档，但是如果网络不好的话则永远不会显示。这是因为Android Studio发现你没有在本地下载对应的文档，所以去google官网进行下载，速度比较慢。将文档下载到本地的方式是：

`Toos -> Android -> SDK Manager` 选择`SDK Tools`页签，勾选`Documentation for Android SDK` 点击OK，下载完成后重启Android Studio应该很快看到悬浮文档提示了。

但是如果还不行的话，可能原因是对应的Android Studio版本优先从网络获取文档，即使你在本地下载了文档也不行，此时需要参考下面的地址，将默认读取方法进行修改：<https://stackoverflow.com/questions/23378610/android-studio-quick-documentation-always-fetching-documentation>