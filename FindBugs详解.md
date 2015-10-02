## Find bugs误报告警的消除方法
	
### 背景介绍

在java工程中，Find bugs的静态检查能够帮助我们挖掘出代码可能存在的缺陷。在我实际使用的过程中，也确实发现了两处由于“缺少else分支”导致“引入未初始化对象”的错误。与之相对应的是，通过Find bugs也发现四处对象中使用静态成员导致Find bugs告警的情况。通过仔细阅读和分析代码逻辑，可以确认代码本身没有问题，这个是属于Find bugs误报的情况。既然我们打算使用Find bugs来做代码的静态检查，那么就有必要保持一个干净的代码环境，这里面没有任何的Find bugs告警。如果确定是代码问题，毫无疑问需要马上纠正。如果确认是Find bugs误报，也应该进行消除，以便后续的检查能够基于一个干净的环境，同样的误报不需要反复确认。Find bugs告警误报的消除非常容易，只需要在两个级别（类级别和方法进行）加上Find bugs的注解就可以消除。这里建议误报消除尽量在方法级别上进行，以控制误报消除的范围，最大限度放置将真正的代码问题也作为误报给隐藏掉了。

### 方法

* 在工程添加注解依赖的jar包：使用Find bugs注解需要用到两个jar包，annotations.jar和jsr305.jar。在eclipse中装完Find bugs插件后，在eclipse目录下可以找到这两个jar包文件。
* 添加注解：在疑问代码所在的类或者方法前面添加注解。其中，value的值就是前面提到的find bugs告警信息中的模式，因为value是一个数组，所以可以同时添加多个模式。justification的值是一句描述信息，你可以理解为是这条注解的注释，内容可以是任意的。

···java
	@edu.umd.cs.findbugs.annotations
	SuppressWarnings(value={"NM_CONFUSING"}, justification="remove findbugs")
···


* 重新运行Find bugs进行检查：添加完注解后，接下来应该重新运行find bugs工具进行检查，以确定误报已经被消除。

## MS: Field should be package protected (MS_PKGPROTECT)

A mutable static field could be changed by malicious code or by accident. The field could be made package protected to avoid this vulnerability.

我这样定义了多个数组，均使用了 public final static 修饰符：

···java
	public final static double[][][] Y_MIN_SCOPE=
	{
		{{-120, -25}},
		{{0, 254}},
		{{0, 254}},
		{{0, 254}}
	    
	};
    public final static double[] GRID_HEIGHT = {1,1,1,1};

 	public final static String[][] TAG_NAMES=
	{
		{"RSRQ(dB)","RSRP(dBm)"},
		{"TA(16*Ts)","UE TxPower(dBm)"},
		{"TA(16*Ts)","RSRP(dBm)"},
		{"TA(16*Ts)","RSRQ(dB)"}
	};
···

findbugs给的修改提示是：

···
	In LTE3DConstant 
	Field LTE3DConstant.Y_MIN_SCOPE 
	At LTE3DConstant.java:[line 53] 
	Y_MIN_SCOPE should be package protected 
	Bug Type: MS_PKGPROTECT 
	Bug Category:MALICIOUS_CODE (Malicious code vulnerability) 
	Source File: 
	Line:53
···

修改成这样就不报错了。

···java
	protected final double[][][] Y_MIN_SCOPE=
	{
		{{-120, -25}},
		{{0, 254}},
		{{0, 254}},
		{{0, 254}}
	    
	};
···

可能原因是因为其它地方没有使用到这个类的变量，所以最好将public改成protected，但是为什么要去掉static还是不理解。
