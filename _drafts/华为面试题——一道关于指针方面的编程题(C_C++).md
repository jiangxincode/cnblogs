    int A[nSize]，其中隐藏着若干0，其余非0整数，写一个函数int Func(int* A, int nSize)，使A把0移至后面，非0整数移至数组前面并保持有序，返回值为原数据中第一个元素为0的下标。

    尽可能不使用辅助空间且考虑效率及异常问题，注释规范且给出设计思路

    注：我的方法的复杂度为O(n)，大家如果有其它方法希望可以交流一下。

```cpp
#include <iostream>
#include <random>

using namespace std;

#define ARRAYSZIE 100
int Func(int* A,int nSize)
{
    int *p_zero = A; //指向最开始的零值
    int *p_unzero = A; //指向最后的非零值
    while(1)
    {
        for(int i=(p_zero-A); i<nSize; i++)
        {
            if(A[i] == 0) //找到第一个零值
            {
                p_zero = &A[i];
                break;
            }
            if(i == nSize-1) //没有找到零值，说明全部为非零值
            {
                return -1;
            }
        }

        for(int i=(p_zero-A+1); i<nSize; i++)
        {
            if(A[i] != 0) //找到零值之后的第一个非零值
            {
                p_unzero = &A[i];
                break;
            }
            if(i == nSize-1) //没有找到下一个非零值，说明全部为零值，或者已经排序完毕
            {
                return (p_zero-A);
            }
        }

        *p_zero = *p_unzero;
        *p_unzero = 0;
        p_zero++;
    }
}
void test_exercise001()
{
    int A[ARRAYSZIE];
    default_random_engine e;
    uniform_int_distribution<> d(0,1);
    for(int i=0; i<ARRAYSZIE; i++)
    {
        A[i] = d(e); //随机产生0和1值
    }
    for(int i=0; i<ARRAYSZIE; i++)
    {
        cout << A[i] << " ";
    }
    cout << "\nThe position of the first zero is: " << Func(A,ARRAYSZIE) << endl;
    for(int i=0; i<ARRAYSZIE; i++)
    {
        cout << A[i] << " ";
    }
}
```