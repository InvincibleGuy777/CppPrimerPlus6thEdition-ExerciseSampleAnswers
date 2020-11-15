```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-3 Stock.h header file
    date-created: 2020-11-15
    date-updated: 2020-11-15
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

// Stock.h augmented version
#ifndef STOCK_H_
#define STOCK_H_
#include<iostream>
class Stock{
private:
    char *company;
    int shares;
    double share_val;
    double total_val;
    void set_tot() { total_val = shares * share_val; }
public:
    Stock();
    Stock(const char *co, long n = 0, double pr = 0.0);
    Stock(const Stock &s); // new copy constructor
    ~Stock();
    void buy(long num, double price);
    void sell(long num, double price);
    void update(double price);
    const Stock &topval(const Stock& s) const;
    Stock& operator=(const Stock &s); // new loaded operator = 
    //Stock& operator=(const char *str); // new loaded operator =

    friend std::ostream &
    operator<<(std::ostream &os, const Stock &s); // new output to replace show()
};


#endif
```