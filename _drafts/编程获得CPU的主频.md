CPU的主频，即CPU内核工作的时钟频率（CPU Clock Speed）。CPU的主频表示在CPU内数字脉冲信号震荡的速度。主频和实际的运算速度存在一定的关系，但目前还没有一个确定的公式能够定量两者的数值关系，因为CPU的运算速度还要看CPU的流水线的各方面的性能指标（缓存、指令集，CPU的位数等等）。由于主频并不直接代表运算速度，所以在一定情况下，很可能会出现主频较高的CPU实际运算速度较低的现象。

在windows操作系统中，可以使用右键点击“我的电脑”，查看属性来获取CPU的主频信息，然而该信息是存在于注册表之中的。也就是说可以通过修改注册表来伪造CPU主频信息。那能不能用其它方法获得该信息呢？

检测CPU的速度，一般是测试在单位时间内运算的指令条数，但用这种方法有太大的局限性，由于受到很多因素的影响，准确度比较低，因为你不知道在你的程序外别的程序占用了多少的时间片。其实在586及之后处理器中，已经有了一条专用的指令来测试主频，那就是 RDTSC指令，意思是读取时间标记计数器(Read Time-Stamp Counter)，Time-stamp counter 是处理器内部的一个64位的MSR (model specific register)，处理器每时钟周期递增时间标签计数器 MSR 一次，在处理器复位时将它重设为 0。RDTSC 指令把 TSC的值低32位装入EAX中，高32位装入EDX中。如果CPU的主频是200MHz，那么在一秒钟内，TSC的值增加 200,000,000 次。所以在计算的时候，把两次的TSC差值除以两次的时间差值就是CPU的主频。

从上面的资料得到了一个思路：首先使用RDTSC指令获取1个TSC的值，将其存储起来，再延时1秒，使用RDTSC指令获取1个新的TSC值，并用其减去第一次获得的TSC值，即可得到该CPU的主频。用C和汇编混合的代码如下：

```c
#include <windows.h>
#include <stdio.h>

int main(int argc,char* argv[])
{
	static int time[2];
	int quotient = 0; //商
	int remainder = 0; //余数

	__asm{
		rdtsc // read time-stamp count
		mov ebx,offset time //将time的偏移地址存入ebx
		mov [ebx+0],edx //把TSC的值的高32位存入[ebx+0]中
		mov [ebx+4],eax //把TSC的值的低32位存入[ebx+4]中
	}
	Sleep(1000);
	__asm{
		rdtsc // read time-stamp count
		mov ecx,offset time //将time的偏移地址存入ecx
		sub eax,[ecx+4] //把延时1秒后的TSC值的低32位减去1秒前的TSC值的低32位
		sbb edx,[ecx+0] //把延时1秒后的TSC值的高32位减去1秒前的TSC值的高32位

		mov ecx,1000000000 //转换成GHz
		div ecx
		mov quotient,eax //将结果中的商赋值于quotiend
		mov remainder,edx //将结果中的余数赋值于remainder
	}
	remainder = remainder / 10000000; //余数仅保留两位
	printf("该机主频为：%d.%d",quotient,remainder);
	return 0;
}
```

注意：寄存器 CR4 中的时间标签禁用 (TSD) 标志限制 RDTSC 的使用。清除 TSD 标志时，RDTSC 指令可以在任何特权级别执行；设置此标志时，指令只能在特权级别 0 执行。在特权级别 0 执行时，时间标签计数器还可以使用 RDMSR 指令读取。

但是在多核时代，RDTSC 指令的准确度大大削弱了，原因有如下几点： 

1. 不能保证同一块主板上每个核的 CPU 时钟周期数（Time Stamp Counter）是同步的； 

2. CPU 的时钟频率可能变化，例如笔记本电脑的节能功能； 

3. 乱序执行导致 RDTSC 测得的周期数不准。 虽然 RDTSC 废掉了，高精度计时还是有办法的，在 Windows 上用 QueryPerformanceCounter 和 QueryPerformanceFrequency，Linux 上用 POSIX 的 clock_gettime 函数，以 CLOCK_MONOTONIC 参数调用。

在接下来的几篇文章章中，我会继续介绍相关内容。

参考文章：

1、多核时代不宜再用 x86 的 RDTSC 指令测试指令周期和时间

http://blog.csdn.net/solstice/article/details/5196544

2、RDTSC命令详解

http://blog.csdn.net/tbwood/article/details/5536597