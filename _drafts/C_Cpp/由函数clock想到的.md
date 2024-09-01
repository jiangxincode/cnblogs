
今天介绍一下`clock`这个函数的使用，它是C标准库的一部分，声明在头文件`<time.h>`中，返回处理器使用的时间值，函数声明为：
`clock_t clock(void);`

这个函数看起来很简单，但是当使用时还是有不少需要注意的地方，让我们先看看`clock_t`这个类型，它表示程序所占用的处理器时间，具体的实现可以是整形或者浮点型，例如我们如果查看`CodeBlock 12.11`中的`time.h`文件，可以看到如下定义：

```c
/*
 * A type for measuring processor time (in clock ticks).
 */
#ifndef _CLOCK_T_DEFINED
typedef	long	clock_t;
#define _CLOCK_T_DEFINED
#endif
```

在这里，`clock_t`被定义为long类型，`MS Visual Studio`中的time.h与此完全相同，但是，如果你将其定义修改为double也没有什么不好的，虽然它的本意是指”ticks”，也就是中文中的“滴答”。那么什么是“滴答”呢？简单的将就是系统每发生一次时钟中断就会产生一个“滴答”，如果详细介绍的话，这设计很多系统内核时钟中断的问题，不过詹荣开老师在它的一篇文章`Linux内核的时钟中断`中对这些概念有着很详细透彻的解读，虽然文章发表于2003年，但其中的骨架知识仍然适用。

介绍完`clock_t`的概念，还要介绍一下`CLOCKS_PER_SEC`这个宏定义，（也是在time.h中），从它的字面意思就可得知，它指的是每秒的时钟滴答数，通过用clock函数返回值除以该值可以得到程序运行是实际秒数。`CLOCKS_PER_SEC`的实际值也是随着操作系统和编译器的差异而不同，例如现在Windows平台上的编译器通常会将其定义为1000，也就是说每秒会产生1000个时钟滴答数。而在一些比较古老的编译器中，比如说TC2.0中，该值是18.2个（当然，在TC2.0中不叫`CLOCKS_PER_SEC`，而叫`CLK_TCK`，但它们的实质是一样的，VC6.0中为了兼容保留了`CLK_TCK`的名称，但建议使用`CLOCKS_PER_SEC`），为什么不同的编译器的默认值差异这么大，这主要是因为与当时硬件条件有关，这是个历史问题，在这里就不继续探讨了。

另外，经常看到一些文章中把`CLOCKS_PER_SEC`翻译成每秒的时钟周期数，其实这是错误的，混淆了时钟周期（clock cycle）和时钟滴答（clock tick）的概念，关于这两个词的区别詹荣开老师也做了介绍。但如果你不想深挖，可以简单的认为要经过若干时钟周期才是一个时钟滴答，具体是多少个决定于系统中对可编程间隔定时器（Programmable Interval Timer，PIT）值的初始定义。

好了，说了这么多，让我们回到clock函数，它主要的用处是衡量我们程序时间开销，例如：

```c
#include <time.h>
#include <stdio.h>

int main(int argc,char* argv[])
{
    clock_t clock_time,start_time,end_time;
    long int count = 1000000000;
    start_time = clock();
    while(count--);
    end_time = clock();
    clock_time = end_time - start_time;
    printf("The program runs %lf clocks\n",(double)clock_time);
    printf("The program runs %lf s\n",(double)(clock_time/CLOCKS_PER_SEC));
    return 0;
}
```

程序的运行结果为：

```shell
The program runs 8430.000000 clocks
The program runs 8.000000 s
```

由于在我的机器上，`CLOCKS_PER_SEC`的值被定义为1000，所以从结果上看是没有问题的。但我们稍微修改一下程序，把初始的count值改为10000，看看结果有什么不同。

```c
#include <time.h>
#include <stdio.h>

int main(int argc,char* argv[])
{
　　clock_t clock_time,start_time,end_time;
　　long int count = 10000;
　　start_time = clock();
　　while(count--);
　　end_time = clock();
　　clock_time = end_time - start_time;
　　printf("The program runs %lf clocks\n",(double)clock_time);
　　printf("The program runs %lf s\n",(double)(clock_time/CLOCKS_PER_SEC));
　　return 0;
}

运行结果如下：

```shell
The program runs 0.000000 clocks
The program runs 0.000000 s
```
 
咦，为什么变成了0，结合编译器为我们指出的运行时间并联系上面的程序，可以发现程序的问题出现在由于count值很小，计算机在不到一个滴答的时间内就完成了计算，又因为clock_t的默认类型是long型，所以会截断取整，所以结果会产生错误。问题根源找到了，那有没有什么解决办法呢？欢迎大家提出自己的见解。

参考文献：`The Standart C Library P.J.Plauger`



 