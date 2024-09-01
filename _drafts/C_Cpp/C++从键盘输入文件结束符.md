        当我们使用一个istream对象作为条件时，其效果是检测流的状态。如果流是有效的，即流未遇到错误，那么检测成功。当遇到文件结束符，或遇到一个无效输入时（例如需要将输入读到一个int变量中，但实际从键盘输入的是字符），istream对象的状态会变成无效。处于无效的istream对象会是条件变为假。

       当从键盘向程序输入数据时，对于如何指出文件结束符，不同的操作系统有不同的实现。在Windows平台中，输入文件结束符的方法是：按Ctrl+z，然后按Enter。在Unix或Linux下是按Ctrl+d，无需Enter，当然，由于当你输入Ctrl+d后，它仍然停留在系统的输入缓冲区中，所以你还是需要使用一个Enter使其生效。下面是几个关于该用法的示例：

```CPP
#include <iostream>
#include <string>

using namespace std;
/*
测试标准输入cin和文件结束符
测试平台：Windows
*/
int test_string_one();
int test_string_two();
int test_string_three();

int main()
{
    //test_string_one();
    test_string_two();
}
int test_string_one() //第一个程序：输入的是整数
{
    int num;
    while(cin>>num)
        cout << num << " ";
    return 0;
}
/*
输入：1 2 3 4 5 Ctrl+d Enter
输出：1 2 3 4 5
此处之所以循环停止，是因为遇到一个无效输入（Ctrl+d），而不是遇到了文件结束符。
因为在windows平台，结束符是Ctrl+z，然后按Enter。
例如输入：1 2 3 4 5 a Enter
输出仍是：1 2 3 4 5
当然如果该测试用例用于Linux下，那么由于系统的结束符是Ctrl+d，所以虽然输出一样，
但是之所以循环停止，是因为到达了文件结束，而不是得到了一个无效输入。
*/


int test_string_two() //第二个程序：输入的是字符串
{
    string word;
    while(cin>>word)
        cout << word << " ";
    return 0;
}
/*
输入：hello world Ctrl+z 回车
输出：hello world
此处之所以循环停止，是因为遇到一个文件结束符。
因为在windows平台，结束符是Ctrl+z，然后按Enter。
*/
```