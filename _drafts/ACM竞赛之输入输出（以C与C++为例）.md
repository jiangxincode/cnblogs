本文转自互联网，内容、排版有修正。

在ACM程序设计竞赛中，一道题目的所有测试数据是放在一个文本文件中，选手将一道题目的程序提交给评判系统运行，程序从该文件中读取测试数据，再把运行结果输出到另一个文本文件中。系统把输出文件与标准答案比对，来评判程序编写得正确与否。ACM现场赛采用的输入输出形式有（1）文件输入、标准输出；（2）文件输入、文件输出；（3）标准的输入输出。而Web形式的ACM程序设计在线评判系统一般采用标准的输入输出，但输入结束有文件末尾标识（EOF)，这可以用于确定输入结束。

## 一、四种基本输入形式

### 1. 一组输入数据

示例：整数求和
<http://acm.njupt.edu.cn/acmhome/problemdetail.do?&method=showdetail&id=1001>

C语法：

```C
#include <stdio.h>
int main()
{
    int a,b;
    scanf("%d %d",&a, &b);
    printf("%d\n",a+b);
}
```

注意：输入前不要打印提示信息。输出完毕后立即终止程序，不要等待用户按键。

C++语法：

```C++
#include<iostream>
using namespace std;
int main()
{
    int a ,b;
    cin>>a>>b;
    cout<<a+b<<endl;
    return 0;
}
```

### 2. 多组输入数据，不说明多少组，直到读至输入文件末尾为止

示例：A + B Problem (1)
<http://acm.njupt.edu.cn/acmhome/problemdetail.do?&method=showdetail&id=1084>

C语法：

```C
#include <stdio.h>
int main()
{
    int a,b;
    while (scanf("%d %d",&a, &b) != EOF)
        printf("%d\n",a+b);
}
```

说明：scanf函数返回值就是读出的变量个数，如：scanf( “%d %d”, &a, &b );如果只有一个整数输入，返回值是1，如果有两个整数输入，返回值是2，如果一个都没有，则返回值是EOF。EOF是一个预定义的常量，等于-1

C++语法：

```C++
#include<iostream>
using namespace std;
int main()
{
    int a ,b;
    while (cin>>a>>b)
        cout<<a+b<<endl;
    return 0;
}
```

cin是一个对象，表达式cin >> m >> n在读入发生错误返回0，否则返回cin的地址。

### 3. 多组输入数据，不说明多少组，以某特殊输入为结束标志。

示例：A + B Problem (2)
<http://acm.njupt.edu.cn/acmhome/problemdetail.do?&method=showdetail&id=1085>

C语法：

```C
#include <stdio.h>
int main()
{
    int a,b;
    while(scanf("%d %d",&a, &b) &&(a||b))
         printf("%d\n",a+b);
}
```

C++语法：

```C++
#include<iostream>
using namespace std;
int main()
{
    int a ,b;
    while(cin>>a>>b&&(a||b))
    {cout<<a+b<<endl;}
    return 0;
}
```

### 4. 多组输入数据，开始输入一个N，接下来是N组数据

示例：A + B Problem (3)
<http://acm.njupt.edu.cn/acmhome/problemdetail.do?&method=showdetail&id=1086>

C语法：

```C
#include<stdio.h>
int main()
{
    int a ,b,n;
    scanf("%d",&n);
    while(n--)
    {
        scanf("%d %d",&a, &b);
        printf("%d\n",a+b);
    }
    return 0;
}
```

C++语法：

```C++
#include<iostream>
using namespace std;
int main()
{
    int a ,b,n;
    cin>>n
    while(n--)
    {
     cin>>a>>b;
     cout<<a+b<<endl;
    }
    return 0;
}
```

## 二、字符串输入

对字符串的输入分三种情况：

### 1、每个字符串中不含空格、制表符及回车

这种情况，用scanf("%s",str)是再好不过的了，比如，测试数据中只有两个字符串：abc def。要读入abc与def，可以这样写：

```C
char str1[1000], str2[1000];
scanf("%s%s", str1, str2);
```

### 2、字符串中含有空格、制表符，但不含回车

对于这种情况，scanf("%s",str)无能为力，因为scanf用空格、制表符及回车作为字符串的分界符。对于一个含有空格、制表符及回车的字符串，如果用scanf("%s",str)来读，将读到若干个字符串，这个字符串被scanf分开了。可以用另外一个函数gets。gets函数用回车作为字符串的分界符，比如，有以下的一个字符串：`Hello world!`。要读入这个字符串，这样写：

```C
char str[1000];
gets(str);
```

这样，str的内容就是"Hello world!"了。另外，gets返回NULL表示出错或end of file。

### 3、字符串中含回车

在这种情况下，如果没有题目的说明，程序无法知道哪里是字符串的分界。那么，用scanf("%c",&ch)来读，一边读，一边判断分界条件是否满足，如果满足，则把当前读到的东西存到一个字符串中。

## 三、输出处理

在初次接触ACM程序设计竞赛时，可能认为：样例中都是输入数据和输入数据在一起，输出结果和输出结果在一起，可能会开个数组，把每组的结果存起来，等输入完了再一起输出。当遇到不知有多少组测试数据的题，就难以处理了。其实在ACM程序设计竞赛中，输入数据和输出数据是分别在两个不同的文件中进行的，程序的输入和输出是相互独立的，所以读入一组数据就输出一组结果，跟先读入所有数据再输出所有的结果，效果是完全一样的。因此，每当处理完一组测试数据，就应当按题目要求进行相应的输出操作。而不必将所有结果储存起来一起输出。在处理输出时，一般要注意：每行输出均以回车符结束，包括最后一行。

### 1. 关于空行（Blank line）

很多题目都要求在输出数据的恰当位置加空行。一个空行就是一个单独的"\n"。这里，有的题目说：“After each test case, you should output one blank line”，而有的题目说：“Between each test case, you should ouput one blank line”。要注意After和Between的区别，因为如果多了一或少了空行，将导致Presentation Error甚至Wrong Answer。

（1）After
这种情况最简单，只需要输出结果后，再加一个printf("\n")或puts("")就行了，就像这样：

```C
int i;
for (i = 0; i < 10; i++)
{
    printf("%d\n", a);
    printf("\n");
}
```

示例：A + B Problem (4)
<http://acm.njupt.edu.cn/acmhome/problemdetail.do?&method=showdetail&id=1087>

C语法:

```C
#include<stdio.h>
int main()
{
    int n,sum,a;
    while(scanf("%d",&n) && n)
    {
         sum=0;
         while(n--)
         {
             scanf("%d",&a);
             sum+=a;
         }
         printf("%d\n",sum);
printf("\n");
    }
    return 0;
}
```

C++语法：

```C++
#include<iostream>
using namespace std;
int main()
{
    int n,sum,a;
    while(cin>>n&&n)
    {
        sum=0;
        while(n--)
        {
            cin>>a;
            sum+=a;
        }
        cout<<sum<<endl;
        cout<<endl;
    }
    return 0;
}
```

（2）Between
Between和After不同的是，最后一组结果后面不应该再加单独的"\n"，应该像这样：]

```C
int i;
for (i = 0; i < 10; i++)
{
    printf("%d\n", a);
    if (i != 9)
        printf("\n");
}
```

由于有时候我们并不知道测试数据有几组（比如测试数据是以end of file 结束的），用上面的方法就不行了，于是，可以换一种写法：

```C
int a;
bool bFirst = true;
while (scanf("%d", &a) == 1)
{
    if (!bFirst)
        puts("");
    else
        bFirst = false;
    printf("%d\n", a);
}
```

这样，从第二组测试数据起，在输出每组测试数据的结果之前就会输出一个空行，和想要的效果是一样的。

### 2、关于空格、逗号以及其他分隔符

这种情况与空行的情况相当相似，处理方法也是一样的，只不过把"\n"改成相应的分隔符就行了。

### 3、带格式的字符串输出

有些题目要求输出这样的字符串：`abc*****de****f`，其中“*”代表空格。
要求是这样的：str1在前5个字符中左对齐，str2在第6到第10个字符中右对齐，str3在第11到第15个字符中右对齐。
可行的做法是，先初始化一个数组，用' '（空格）填充，再在相应的位置填相应的内容。用程序来表述：

```C
01:char str[1000];
02:char str1[] = "abc", str2[] = "de", str3[] = "f";
03:memset(str, ' ', 1000 * sizeof(char));
04:sprintf(str, "%s", str1);
05:str[strlen(str1)] = ' ';
06:sprintf(str + 5, "%5s", str2);
07:str[10] = ' ';
08:sprintf(str + 10, "%5s", str3);
09:str[15] = '\0';
10:puts(str);
```

关键的部分：
（1）在调用sprintf后，要清除不恰当字符串结束符（第5,7行）；
（2）在恰当的位置添加字符串结束符（第9行）。

### 4、二维数组的输出

首先要考虑的是数组是按行排列还是按列排列，如果是按行排列，就应该这样写：

```C
int i, j;
01: for (i = 0; i < nRow; i++)
02: {
03:     for (j = 0; j < nCol; j++)
        {
            if (j > 0)
                printf(" ");
            printf("%d", a[j]);
        }
        puts("");
    }
```

如果是按列，就要把1行和3行交换。

### 5、模拟屏幕输出

在一些模拟题中，题目要求输出一幅画，只不过这个画是由字符组成的。对于这种情况，可以采用和带格式的字符串输出相似的方法，先开一个字符数组（在这里，是二维数组），然后把数组当成屏幕输出，屏幕的(i, j)点就是数组的(i, j)号元素。最后，输出这个二维数组就行了。一般来说，可以输出一个二维字符数组的方法和输出一般数组的方法是一样的，用双重循环来做。不过，可以只用一个循环就可以了，原因是在数组每行的恰当位置（一般是末尾）加了一个'\0'，那么，数组的每一行就成了一个字符串，于是，输出程序就变成了：

```C
int i;
char str[100][100];
...
for (i = 0; i < nRow; i++)
puts(str);
```