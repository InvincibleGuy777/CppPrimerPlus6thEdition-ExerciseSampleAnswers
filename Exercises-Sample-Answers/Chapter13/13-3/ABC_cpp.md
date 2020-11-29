```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-3 ABC.cpp function definition
    date-created: 2020-11-29
    date-updated: 2020-11-29
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

#include "ABC.h"
#include <iostream>
#include <cstring>
using std::cout;
using std::endl;
using std::strlen;
using std::strcpy;

ABC::ABC(const char *lbl, int rt){
    cout << "ABC(...) object " << this << " created~\n";
    label = new char[strlen(lbl) + 1];
    strcpy(label, lbl);
    rating = rt;
}

ABC::ABC(const ABC& abc){
    cout << "ABC(const&) object " << this << " created~\n";
    label = new char[strlen(abc.label) + 1];
    strcpy(label, abc.label);
    rating = abc.rating;
}

ABC::~ABC(){
    cout << "ABC object " << this << " destroyed~\n";
    delete[] label;
}

ABC &ABC::operator=(const ABC &abc){
    if(this == &abc)
        return *this;
    delete[] label;
    label = new char[strlen(abc.label) + 1];
    strcpy(label, abc.label);
    rating = abc.rating;
    return *this;
}

/* 
It's not appropriate to use friend function here
because if we use a ABC pointer, the output order 
such as 'cout<<*abc;' cannot get a correct output 
when we point it to a derived class!!
/*
/*
std::ostream &operator<<(std::ostream &os, const ABC &abc){
    os << "Label: " << abc.label << endl;
    os << "Rating: " << abc.rating << endl;
    return os;
}
*/

```