        conio.h不是C标准库中的头文件，在ISO和POSIX标准中均没有定义。conio是Console Input/Output（控制台输入输出）的简写，其中定义了通过控制台进行数据输入和数据输出的函数，主要是一些用户通过按键盘产生的对应操作，比如getch()函数等等。大部分DOS，Windows，Phar Lap，DOSX，OS/2等平台上的C编译器提供此文件，UNIX和Linux平台的C编译器本身通常不包含此头文件，但已经有其兼容包，可参考：
http://conio.sourceforge.net/

另外大家平时主要是利用conio.h这个头文件中的getch()函数，即读取键盘字符但是不显示出来（without echo)，但是含有conio.h的程序在linux无法直接编译通过，因为linux没有这个头文件，除了利用上述的兼容包外还可以在linux采用原生的方法达到同样的效果，那就是利用linux系统的命令stty –echo，它代表不显示输入内容，源代码如下。

```cpp
//in windows

#include<stdio.h>

#include<conio.h>

int main(){

char c;

printf("input a char:");

c=getch();

printf("You have inputed:%c \n",c);

return 0;

}

//in linux

#include<stdio.h>

int main(){

char c;

printf("Input a char:");

system("stty -echo");

c=getchar();

system("stty echo");

printf("You have inputed:%c \n",c);

return 0;

}
```