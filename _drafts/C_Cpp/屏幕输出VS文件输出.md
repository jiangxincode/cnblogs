## 输出到屏幕快还是输出到文件快?

我们在编写程序时经常需要数一些数据到屏幕，来查看我们的结果是否正确，虽然直接输出到屏幕，查看起来呢很方便，但当数据量很大时，需要耗费大量的时间。于是我们想到能不能通过输出到文件来减少时间呢。相同的数据是输出到屏幕更快还是输出到文件更快？

这个地方变量有很多：磁盘速度、目的文件有没有其他IO请求、文字渲染的方式、API具体的操作流程、操作系统本身的设计等等都会影响输出到文件的速度。但一般来说还是会比直接输出到屏幕快（而且通常快几个数量级）。

比如我们可以用如下代码进行测试，如果测试输出到文件的时间就在开头加入#define ToFile，如果测试输出到屏幕的时间，就注释掉。

```c
//#define ToFile
#include <stdio.h>
#include <time.h>
 
int main()
{
    clock_t start_test,end_test;
    start_test = clock();
    FILE *output_fils;
    output_fils = fopen("output_file.txt","w");
    if(output_fils == NULL)
    {
        perror("Error to create the file\n");
    }
    long unsigned int i;
    for(i=0;i<1000000;i++)
    {
        #ifdef ToFile
            fprintf(output_fils,"item %ld\n",i);
        #else
            printf("item %ld\n",i);
        #endif
    }
    fclose(output_fils);
    end_test = clock();
    printf("The total time is: %lf",((double)(end_test-start_test)/CLOCKS_PER_SEC));
    return 0;
}
```

通过编译运行，我们会发现，如果输出到文件仅需要0.015s，但是直接输出到屏幕却需要12.906s，两者差距很大。

## 怎样编程使结果全部输出到文件?

当然，你可以在每个需要输出的地方用fprintf来设置输出到文件。但是考虑到那样太麻烦了，而且我们已经系管理直接使用printf，所以我们可以用一个函数freopen来把标准输出流导出到我们设定的文件流中，这样我们以后用printf输出到东西全部到达我们设定的文件中。

但是有个问题是，那我们如何在某些特定的时候在屏幕上输出提示信息呢？考虑到标准错误流也是输出到屏幕，所以我们可以假借这个标准错误流。示例代码如下：

```c
#include <stdio.h>

int main()
{
    int num;
    freopen("output_file.txt","w",stdout);
    fprintf (stderr,"Please input your num:"); // output to the screen
    scanf("%d",&num);
    printf("The num that you input is:%d",num); // output to the file
    fclose (stdout);
    return 0;
} 
