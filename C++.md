
<!-- vim-markdown-toc GFM -->

* [1. 范围for](#1-范围for)
* [2. bool](#2-bool)
* [3. new - delete](#3-new---delete)
* [4. 指针](#4-指针)
* [5. 函数重载](#5-函数重载)
* [6. 函数默认参数](#6-函数默认参数)
* [7. 引用](#7-引用)
* [8. 函数参数的传递方式](#8-函数参数的传递方式)
* [9. 构造函数](#9-构造函数)
* [10. 析构函数](#10-析构函数)
* [11. List类](#11-list类)
* [12. 设计原则](#12-设计原则)
* [13. this](#13-this)
* [14. static](#14-static)
* [15. const](#15-const)
* [16. 初始化列表](#16-初始化列表)
* [17. 类之间的关系](#17-类之间的关系)
* [18. 继承](#18-继承)
* [19. 多态](#19-多态)
* [20. 虚析构](#20-虚析构)

<!-- vim-markdown-toc -->
#### 1. 范围for
````c++
int arr[10] = {1,2,3,4,5,6,7,8,9,0}; 
//自动遍历arr这个数组，把 arr[i]值 赋值 给 nVal 
for(int nVal:arr) 
{ 
    cout << nVal << " "; 
} 
    cout << endl; 
````
````c++
//auto类型 自动识别 
for(auto nVal:arr) 
{ 
    cout << nVal << " "; 
} 
    cout << endl; 
````
#### 2. bool
````c++
int main() 
{ 
    bool bflag = false; 
    bflag = true; 
} 
````

#### 3. new - delete
````c++
int* p = (int*)malloc(sizeof(int)); 
free(p); 
````
````c++
创建-----》指针变量 = new 数据类型 
释放-----》delete 指针 
int* p = new int; 
cin >> *p; 
cout << *p <<endl; 
delete p; 
p = 0; 
//new 也是在堆区分配空间 
````
````c++
int* arr = new int[3]; 
delete[] arr; //删除数组 
arr = 0; 
````
````c++
new 整形指针
    int* (*p) = new int*;  delete p; p = 0; 
new 整形指针数组
    int* (*p) = new int*[3]; delete[] p; p = 0; 
new 整形二维数组
    int (*p)[] = new int[2][3]; delete[] p; p =0; 
new 结构体
    struct Node 
    { 
        int nVal; 
        char c; 
    }; 
    Node* pNode = new Node; 
    pNode->c = 'a'; 
    pNode->nVal = 100; 
    delete pNode; 
    pNode = 0; 
````
#### 4. 指针
指针的作用？<br> 
&#8195; 1.装地址<br> 
&#8195; 2.间接操作空间<br>
````c++
正常数组
int arr[3] = {};
int *p = arr == int *p = &arr[0]; 
int (*p)[3] = &arr;
````
````c++
指针数组
int* arr[3] = {};
int* (*p) = arr; 
int* (*p)[3] = &arr
````
````c++
二维数组
int arr[2][3] = {};
int (*p)[] = arr; 
int (*p)[2][3] = &arr;
````
#### 5. 函数重载
在同一作用域，名字一样，参数列表不同（参数的个数或者参数的类型） 
````c++
void AA(int r) 
{ 
    cout << r+r << endl; 
} 
void AA(char* psz) 
{ 
    cout <<psz <<endl; 
} 
````
````c++
int main()
{ 
    AA(123); 
    AA("adfa"); 
} 
````
#### 6. 函数默认参数
定义函数时，可以给参数默认值,调用的时候 可以 不传参数 <br>
- 1. 函数的默认参数 是要 后面 不能空  <br>
- 2. 函数的调用参数 是要 前面 不能 <br>
````c++
void Show(int a = 1, int b = 2, int c =3, int d =4); 
int main() 
{ 
    Show(); 
    Show(10); 
    Show(10,20); 
    Show(10,20,30); 
    Show(10,20,30,40); 
} 
````
#### 7. 引用
- 是什么 <br>
被声明为引用类型的变量名则是实际变量的别名 
- 做什么 <br>
使用两个以上的变量名，指向同一地址空间 
- 指针 和 引用 的区别 <br>
-- 1.使用两个以上的变量名，指向同一地址空间 <br>
-- 2.引用初始化后不能再重新引用其他的空间 <br>
-- 3.引用不占内存 <br>
-- 4.引用的是一个合法的存储单元 <br>
```c++
int main()
{
    int a = 100;
    int& k = a; //引用必须初始化
    k++;
    cout<<k<<endl;  // k == a
    cout<<a<<endl;
}
```
#### 8. 函数参数的传递方式 
- 值传递 <br>
-- 函数参数的传递方式 
- 地址传递 <br>
-- new 一个新的空间
- 引用传递 <br>
-- 栈区的变量
```c++
int main() 
{ 
    int a = 100; 
    int b = 200; 
//交换a b 值 
} 
方法一---------------------->地址传递 
void Swap(int *x, int *y) 
{ 
    int temp = *x; 
    *x = *y; 
    *y = temp; 
} 
Swap(&a,&b); 
方法二---------------------->引用传递 
void Swap(int &x, int &y) 
{ 
    int temp = x; 
    x = y; 
    y = temp; 
} 
Swap(a,b); 
方法三---------------------->主函数中异或 
int main() 
{ 
    a = a * b; 
    b = a * b; 
    a = a * b; 
} 
```
#### 9. 构造函数
和类名一样，没有返回值，可以带参数<br>
在创建对象的时候，自动调用构造函数，只要创建对象，就一定会调用构造函数<br>
用来给类成员初始化<br>
构造函数可以有多个，但是一个对象只能有一个<br>
如果类中没有写构造，会有一个默认的无参数的构造
```c++
class CPerson
{
public:
    CPerson()
    {
    }
};
```
#### 10. 析构函数
当一个对象的生命周期结束时，其所占有的内存空间就要被回收<br>
这个工作由析构来完成<br>
没有返回值，不允许带参数，一个类中只有一个

```c++
class CPerson
{
public:
    int * arr;
public:
    CPerson()
    {
        arr = new int(100);
    }
    ~CPerson()
    {
        delete arr;
    }
};
```
#### 11. List类
```c++
class CList
{
private:
    typedef struct Node
    {
        int nVal;
        Node* pNext;
    }NODE;
    NODE *m_pHead;
    NODE *m_pEnd;
    int m_Size;
public:
    CList()
    {
        m_Size = 0;
        m_pHead = 0;
        m_pEnd = 0;
    }
    ~CList()
    {
        NODE *pDel = 0;
        while(m_pHead != NULL)
        {
            pDel = m_pHead;
            m_pHead = m_pHead->pNext;
            delete pDel;
            pDel = 0;
        }
    }
public:
    void Push_Back(int nVal)
    {
        NODE* pNode = new NODE;
        pNode->nVal = nVal;
        pNode->pNext = NULL;

        if(m_pHead == NULL)
        {
            m_pHead = pNode;
            m_pEnd = pNode;
        }
        else
        {
            m_pEnd->pNext = pNode;
            m_pEnd = pNode;
        }
        m_Size++;
    }
    void Show()
    {
        NODE *pTemp = m_pHead;
        while(pTemp)
        {
            cout<<pTemp->nVal<<" ";
            pTemp = pTemp->pNext;
        }
        cout<<endl;
        cout<<"size:"<<m_Size<<endl;
    }
    void Del(int nNum)
    {
        NODE *pDel = m_pHead;
        NODE *pTemp = m_pHead;
        while(nNum-1 != 1)
        {
            pTemp = pTemp->pNext;
            nNum--;
        }
        pDel = pTemp->pNext;
        pTemp->pNext = pDel->pNext;
        delete pDel;
        pDel = NULL;
        pTemp = NULL;
        m_Size--;
    }
};

int main()
{
    CList lst;
    lst.Show();
    lst.Push_Back(1);
    lst.Push_Back(2);
    lst.Push_Back(3);
    lst.Push_Back(4);
    lst.Push_Back(5);
    lst.Show();
    lst.Del(2);
    lst.Show();
    return 0;
}
```

#### 12. 设计原则
- 单一职责<br>
一个类承担的职责越少，复用性就越好
- 开闭原则<br>
对扩展是开放，对修改是关闭的

#### 13. this
- 空类的大小是 一个字节 占位<br>
- 加了变量的类的大小就是成员变量的大小<br>
- 类中的成员变量是在创建对象的时候存在的，每个对象都有一份自己的成员变量<br>
- 类中的成员函数是在编译期的时候存在的，所有的对象共用一个成员函数<br>
- this -> 当前这个类的指针
- 类中的非静态的成员函数都以一个隐藏的参数 -> this
- this 用来区分在函数中不同对象的成员,完成了封装
#### 14. static
静态成员变量
- 静态成员变量是在编译期存在的，不创建对象就能用
- 普通成员变量是在创建对象的时候存在的
- 静态成员变量 直接通过 类名::变量名 调用
- 静态变量只有一份，是所有对象共享的
- 静态成员变量 一定要在 .cpp 中初始化
````c++
CPerson.h
class CPerson
{
public:
    static int m_nAge;
};
````
````c++
CPerson.cpp
int CPerson::m_nAge = 1;
````
静态成员函数<br>
- 静态成员函数 直接通过 类名::函数名 调用
- 静态成员函数 只能用静态成员变量，不能用非静态成员，因为这个函数中没有this指针
#### 15. const
const 成员变量
- const 成员变量，必须在初始化列表中初始化
- const 成员变量， 初始化后不允许修改
```c++
CPerson.h
class CPerson
{
public:
    const int m_nAge;
}
```
```c++
CPerson.cpp
CPerson::CPerson():m_nAge(/*初始化的值*/123 )
{}
```
```c++
main.cpp
int main()
{
    CPerson ps;
    cout<<ps.m_nAge<<endl;
    return  0;
}
```
const 成员函数
- const 成员函数 不能修改类中的成员变量，因为this已经变成cosnt this 
```c++
CPerson.h
class CPerson
{
public:
    const int m_nAge;
public:
    void Show() const;
}
```
```c++
CPerson.cpp
CPerson::CPerson():m_nAge(/*初始化的值*/123 )
{}
void CPerson::Show() const
{}
```
cosnt 对象
- const 只能用const 函数，普通函数不能用
```c++
int main
{
    const CPerson ps;
    return 0;
}
```
#### 16. 初始化列表
- const 成员变量，必须在初始化列表中初始化
- 当一个类包含另一个类的对象时，执行指定的构造函数也需要在初始化列表中初始化
- 初始化列表的执行顺序，是根据变量定义的顺序执行的
#### 17. 类之间的关系
- 组合（复合）<br>
-- A is part of B<br>
-- 部分与整体的关系
-- 代码的表现形式 -> 在类中直接定义对象<br>
```c++
class CPerson
{
private:
    CHand hand;
    CHead head;
public:
    void say();
    void move();
};
class CHead
{
public:
    void say();
}
class CHand
{
public:
    void move();
}
```
- 依赖<br>
-- A use B<br>
-- 某个对象的功能依赖于另外的某个对象，而被依赖的对象只是作为一种工具在使用<br>
-- 代码的表现形式 -> 传参数，在函数里定义变量<br>
```c++
class CPerson
{
public:
    void code(CComputer& cp);
};
class CComputer
{
public:
    void coding();
};
```
- 关联<br>
-- A has B<br>
-- 二者之间是平等的，没有任何强制性约束<br>
-- 代码的表现形式 -> 指针 <br>
```c++
class CPerson
{
public:
    CFriend *m_pFriend;
public:
    CPerson()
    {
        m_pFriend = NULL;
    }
};
class CFriend
{
public:
};
```
- 聚合<br>
-- A owns B<br>
-- 一对多的所属关系<br>
-- 代码的变现形式 -> 指针数组
```c++
class CFamily
public:
    CPerson *arr[10];
public:
    void AllCoding();
};
class CPerson
{
public:
};
```
- 他们之间的强弱关系；依赖 < 关联 < 聚合 < 组合<br>
**总结** <br>
- 依赖，关联<br>
-- 没有生命期
- 组合，聚合<br>
-- 有生命期，要在析构里写销毁
#### 18. 继承
```c++
class CFather
{};
class CSon : public CFather
{};
```
- 继承的优点<br>
-- 提高了代码的复用性<br>
- 基类 和 派生类 构造 析构 的执行顺序<br>
-- 基类构造 - 派生类构造 - 派生类析构 - 基类析构
- 继承的方式 - 对派生类的对象的访问的影响（派生类对象在main()中的使用）<br>
-- **public 继承**<br>
--- public - 不变 protected - 不变 private - 在派生类中不可访问<br>
-- **protected 继承**<br>
--- public - 变成 protected protected - 不变 private - 在派生类中不可访问<br>
-- **private 继承**<br>
--- public - 变成 private protected - 变成 private private - 在派生类中不可访问<br>
- 父类指针 指向 子类对象<br>
```c++
int main()
{
    CFather *pFather = new CSon;
    return 0;
}
```
通过父类的指针只能拿到父类的成员变量，拿不到子类的，除非强转<br>
- 缺点：<br>
只能用父类的，不能用子类的 -> 解决方法：虚函数实现的多态
- 优点：<br>
统一类型，提高复用性
#### 19. 多态
- 在父类的函数前加virtual 变成虚函数，使得父类指针可以调用子类的<br>
- 虚函数，通过父类的指针调用实际的子类的成员函数
- 前提是，子类中需要重写这个函数
- 优点：<br>
提高复用性和扩展性<br>
- 缺点：<br>
空间，效率，安全性
```c++
class CWater
{
public:
   virtual void Show()
    {
        cout<<"Water"<<endl;
    }
};

class CMilk : public CWater
{
public:
    void Show()
    {
        cout<<"milk"<<endl;
    }
};

class CBeer : public CWater
{
public:
    void Show()
    {
        cout<<"beer"<<endl;
    }
};

class CCoco : public CWater
{
public:
    void Show()
    {
        cout<<"coco"<<endl;
    }
};

void Bottle(CWater *p)
{
    p->Show();
}


int main()
{
    CCoco *coco =  new CCoco;
    CBeer *beer = new CBeer;
    CMilk *milk = new CMilk;
    
    Bottle(beer);
    Bottle(coco);
    Bottle(milk);
    return 0;
}
```
#### 20. 虚析构
- 通过父类的指针去完整删除一个子类的对象，防止内存泄漏
