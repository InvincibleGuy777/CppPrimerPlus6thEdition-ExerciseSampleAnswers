```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-2 Cd.cpp function definition (DMA version)
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

#include "Cd.h"
#include <iostream>
#include <cstring>
using std::cout;
using std::endl;
using std::strlen;

Cd::Cd(char *s1, char *s2, int n, double x){
    performers = new char[strlen(s1) + 1];
    label = new char[strlen(s2) + 1];
    std::strcpy(performers, s1);
    std::strcpy(label, s2);
    selections = n > 0 ? n : 0;
    playtime = x >= 0 ? x : 0;
    cout << "Cd(...) Object " << this << " created~" << endl;
}

Cd::Cd(const Cd& d){
    performers = new char[strlen(d.performers) + 1];
    label = new char[strlen(d.label) + 1];
    std::strcpy(performers, d.performers);
    std::strcpy(label, d.label);
    selections = d.selections;
    playtime = d.playtime;
    cout << "Cd(const&) Object " << this << " created~" << endl;
}

Cd::Cd(){
    performers = new char[5];
    label = new char[5];
    std::strcpy(performers, "null");
    std::strcpy(label, "null");
    selections = 0;
    playtime = 0.0;
    cout << "Cd() Object " << this << " created~" << endl;
}

Cd::~Cd(){
    cout << "Cd Object " << this << " destroying~" << endl;
    delete[] performers;
    delete[] label;
}

void Cd::Report() const{
    cout << "Performers: " << performers << endl;
    cout << "     Label: " << label << endl;
    cout << "Selections: " << selections << endl;
    cout << "    Playtime: " << playtime << endl;
}

Cd& Cd::operator=(const Cd& d){
    if(this == &d)
        return *this;
    delete[] performers;
    delete[] label;
    performers = new char[strlen(d.performers) + 1];
    label = new char[strlen(d.label) + 1];
    std::strcpy(performers, d.performers);
    std::strcpy(label, d.label);
    selections = d.selections;
    playtime = d.playtime;
    return *this;
}

```