``` cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-3 Stock.cpp function definition
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

// useStock.cpp --using the Stock class
// compile with Stock.cpp
#include<iostream>
#include "Stock.h"

const int STKS = 4;
int main(){
    using std::cout;
    // create an array of initialized objects
    Stock stocks[STKS] = {
        Stock("NanoSmart", 12, 20.0),
        Stock("Boffo Objects", 200, 2.0),
        Stock("Monolithic Obelisks", 130, 3.25),
        Stock("Fleep Enterprises", 60, 6.5)
    };
    cout << "Stock holdings:\n";
    int st;
    for (st = 0; st < STKS; st++)
        cout << stocks[st];
    // set pointer to first element
    const Stock *top = &stocks[0];
    for (st = 1; st < STKS; st++)
        top = &top->topval(stocks[st]);
    // now top points to the most valuable holding
    cout << "\nMost valuable holding:\n";
    cout << *top;
    std::cin.get();
    return 0;
}

```