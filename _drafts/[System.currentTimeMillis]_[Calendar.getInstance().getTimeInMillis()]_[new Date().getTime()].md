欢迎和大家交流技术相关问题：
邮箱: jiangxinnju@163.com
博客园地址: <http://www.cnblogs.com/jiangxinnju>
GitHub地址: <https://github.com/jiangxincode>
知乎地址: <https://www.zhihu.com/people/jiangxinnju>

在Java中,生成当前的时间戳大致上有这么几种方法,分别是:

* `System.currentTimeMillis()`,它属于`java.lang.System`

* `Calendar.getInstance().getTimeInMillis()`,它属于`java.util.Calendar`

* `new Date().getTime()`,它属于`java.util.Date`;

他们都是返回从1970/1/1返回到现在所经过的毫秒数，从实现上来看`new Date().getTime()`也是依据`System.currentTimeMillis()`

```
    public Date() {
        this(System.currentTimeMillis());
    }
```

单从性能方面考虑，优先使用`System.currentTimeMillis()`，采用如下方式比较性能，输入结果为：

System.currentTimeMillis(): 477
Calendar.getInstance().getTimeInMillis(): 16415
new Date().getTime(): 433

```
		startTime = System.currentTimeMillis();
		for (int i = 0; i < times; i++) {
			System.currentTimeMillis();
		}
		endTime = System.currentTimeMillis();
		System.out.println("System.currentTimeMillis(): " + (endTime - startTime));
		
		startTime = System.currentTimeMillis();
		for (int i = 0; i < times; i++) {
			Calendar.getInstance().getTimeInMillis();
		}
		endTime = System.currentTimeMillis();
		System.out.println("Calendar.getInstance().getTimeInMillis(): " + (endTime - startTime));
		
		startTime = System.currentTimeMillis();
		for (int i = 0; i < times; i++) {
			new Date().getTime();
		}
		endTime = System.currentTimeMillis();
		System.out.println("new Date().getTime(): " + (endTime - startTime));
```