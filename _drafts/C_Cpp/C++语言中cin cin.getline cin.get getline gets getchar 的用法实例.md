```CPP
#include <iostream>

#include <string>

using namespace std;

//关于cin cin.getline cin.get getline gets getchar 的用法实例

void main(int argc, char* argv[])

{

//1、cin>>

//method one， 也就是最常用的方法 输入一个数字

cout << "Test cin>> 用法1：" << endl;

int a,b;

cout << "input two integer:" << endl;

cin >> a >> b;

cout << "SUM =" << a + b << "\n" << endl;

//method two，输入一个字符串，遇到“空格 回车 Tab”都结束

cout << "Test cin>>用法2：" << endl;

char array[10];

cout << "input a char array:" << endl; 

cin >> array;

cout << array << "\n" << endl;

//2、cin.get()

//one cin.get(字符变量名) 可以用来接收字符

cout << "Test cin.get(字符变量名)：" << endl;

char ch;

char cch;

cout << "Input a char:" << endl;

ch = cin.get(); //把之前输入的回车符号滤去

cch = cin.get(); //or cin.get(ch);

cout << cch << "\n" << endl;

//two cin.get(字符数组，接收的字符数) 用来接收一行字符串可以接收空格

cout << "Test cin.get(字符数组，接收的字符数):" << endl;

char array1[20];

cout << "Input a char array:" << endl;

ch = cin.get(); //把之前输入的回车符号滤去

cin.get(array1,10);

cout << array1 << "\n" << endl;

//注:cin.get(无参数)主要用来舍弃输入流中不需要的字符 或者舍弃回车

//从而弥补了cin.get(字符数组，接收的字符数)的不足

//3、cin.getline(cin,str)  接收一个字符串 可以接收空格

cout << "Test cin.getline() 的用法：" << endl;

char array2[20];

cout << "Input a char array:" << endl;

ch = cin.get(); //把之前输入的回车符号滤去

cin.getline(array2,20);

cout << array2 << "\n" << endl;

//实际上cin.get(字符数组，接收的字符数) 和cin.getline(字符数组，接收的字符数)

//有三个参数cin.getline(字符数组，接收字符数，结束字符) 第三个参数默认是'\0'

//多维数组中也经常用到cin.getline(字符数组，接收的字符数)的用法

cout << "cin.get(字符数组，接收的字符数) is used in multidimensional array:" << endl;

char array3[3][10];

for (int i = 0;i < 3;i ++)

{

cout << "请输入第" << i+1 << "行的字符串：" << endl;

cin.getline(array3[i],10);

}

for (int j = 0;j < 3;j ++)

{

cout << "第" << j+1 << "行：" << array3[j] << endl;

}

//4、getline(cin,str)的用法 接收一个可以包含空格的字符串(这儿是string类型的) 需要包含头文件#include <string>

//getline(cin,str)是string流不是i/o流

cout << "Test getline(cin,str):" << endl;

string str;

cout << "Input a string:" << endl;

//ch = cin.get(); //把之前输入的回车符号滤去

getline(cin,str);

cout << str << "\n" << endl;

//5、gets(char *) 接收一个可以包含空格的字符串 需要包含头文件#include <string>

cout << "Test gets(char *)的用法" << endl;

char array4[20];

cout << "input a char array:" << endl;

ch = cin.get(); //把之前输入的回车符号滤去

gets(array4);

//The gets function reads a line from the standard input stream stdin and stores it in buffer. 

//The line consists of all characters up to and including the first newline character ('\n').

//gets then replaces the newline character with a null character ('\0') before returning the line

cout << array4 << "\n" << endl;

//gets(char *)也可以用在多维数组里面 跟cin.getline()用法类似

//6、getchar(无参数) 接收一个字符 需要包含头文件#include <string>

cout << "Test getchar(无参数)的用法：" << endl;

char ch1;

 

cout << "input a char:" << endl;

ch1 = getchar(); // 不能写成getchar(ch1);

cout << ch1 << "\n" << endl;

//getchar()是C的函数 C++是兼容C 所以也可以使用 但尽量不用或少用

}
```