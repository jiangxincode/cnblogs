```cpp
/*
    Function:method of Josephus question
*/
#include <iostream>

using namespace std;

struct node
{
    int seq;
    node *next;
};
typedef struct node NODE;

void test_Josephus()
{
    /*假设共有n人，从第s个人开始数数，每数到m该人出列，后面的人重新开始数，知道全部人出列*/
    int n,s,m;
    NODE *head,*last,*current,*prev;
    cout << "Input the n,s,m(separate with space):";
    cin >> n >> s >> m;

    for(int i=1;i<=n;i++) //建立循环链表
    {
        current = new NODE;
        current->seq = i;
        current->next = head;
        if(i == 1)
        {
            head = current;
            last = current;
        }
        else
        {
            last->next = current;
            last = last->next;
        }
    }
    current = head; //遍历循环链表，输出序列
    do
    {
        cout << current->seq << " ";
        current = current->next;
    }while(current!=head);

    current = head; //将current置于第s个位置
    for(int i=1;i<s;i++)
    {
        current = current->next;
    }
    cout << endl;

    for(int i=1;i<=n;i++) //共循环n轮，得到一个整体的输出序列
    {
        for(int j=1;j<m;j++)
        {
            prev = current;
            current = current->next;
        }
        cout << current->seq << " ";
        prev->next = current->next;
        delete current;
        current = prev->next;
    }
}
```