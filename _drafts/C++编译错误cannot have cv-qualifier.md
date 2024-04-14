const关键字放在非静态成员函数声明的尾部,表示该非静态成员函数不修改对象内容。volatile关键字放到非静态函数声明的尾部，表示该非静态成员函数是线程安全的。注意他们都只能放到非静态成员函数声明的尾部，否则会产生如下报错：
`error: non-member function 'xxx' cannot have cv-qualifier`
放到非成员函数声明的尾部

```CPP
#include <iostream>

using namespace std;

double getSqureArea(int a) const
{
    return a * a;
}


int main(int arg, char *argv[])
{
    cout << getSqureArea(2) << endl;
    return 0;
}
```

编译上面的C++程序，报错如下：

```shell
g++ -c const_volatile_test.cpp -o const_volatile_test.o
const_volatile_test.cpp:12:28: error: non-member function 'double getSqureArea(int)' cannot have cv-qualifier
```

放到静态成员函数声明的尾部

```CPP
#include <iostream>

using namespace std;

class CStatic
{
    private:
    static int static_value;
    public:
    static int get_static_value() const
    {
        return static_value;
    }
};

int CStatic::static_value = 1;
int main(int argc,char *argv[])
{
    cout << CStatic::get_static_value()<<endl;
    return 0;
}
```

编译上面的C++程序，报错如下：

```shell
g++ -c const_volatile_test.cpp -o const_volatile_test.o
const_volatile_test.cpp:17:39: error: static member function 'static int CStatic::get_static_value()' cannot have cv-qualifier
```
 