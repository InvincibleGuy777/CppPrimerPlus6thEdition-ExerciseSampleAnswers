```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-4 port.h header file
    date-created: 2020-11-30
    date-updated: 2020-11-30
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

#ifndef _PORT_H_
#define _PORT_H_

#include <iostream>
using namespace std;

class Port{

private:
    char *brand;
    char style[20]; // i.e., tawny, ruby, vintage
    int bottles;
public:
    Port(const char* br = "none", const char* st = "none", int b = 0);
    Port(const Port &p);
    virtual ~Port() { delete[] brand; }
    Port &operator=(const Port &p);
    Port &operator+=(int b); // add b to bottles
    Port &operator-=(int b); // subtracts b from bottles, if available
    int BottleCount() const { return bottles; }
    virtual void Show() const;
    friend ostream &operator<<(ostream &os, const Port &p);
};

class VintagePort: public Port{
private:
    char *nickname; // i.e., "The Noble" or "Old Velvet", etc.
    int year; // vintage year
public:
    VintagePort();
    VintagePort(const char *br, int b, const char *nn, int y);
    VintagePort(const VintagePort &vp);
    ~VintagePort() { delete[] nickname; }
    VintagePort &operator=(const VintagePort &vp);
    void Show() const;
    friend ostream &operator<<(ostream &os, const VintagePort &vp);
};

#endif

/*
 Answers for b. "为什么有的方法被重新定义了，而有些没有重新定义？": 
 重新定义的方法即用virtual修饰的方法（除了析构函数外），即`void Show() const;`，它被重新定义
 是因为对于不同的类，输出这个行为应有所不同，因此需要重新定义；而其余方法中，构造函数、运算符和
 友元无法重新定义，因为不同的类其特征标一定不同。

 Answers for c. "为何没有将`operator=()`和`operator<<()`声明为虚的？": 
 其一，声明为虚函数，就意味着设计者想利用多态性，即同一个函数调用对于不同类对象具有不同的行为，
 这就要求虚函数以及它的重定义函数需要具有相同的特征标，然而这两个运算符函数的参数列表对于不同类
 而言会有所不同；其二，如果基类的赋值运算符被声明为虚的，那么派生类的重定义行为会隐藏基类的相应
 函数——因为它们的特征标不一致，而对于`operator<<()`这种友元函数，它不属于成员函数，而虚函数必
 须是成员函数。因此，两个运算符函数没有被声明为虚的。
*/

```