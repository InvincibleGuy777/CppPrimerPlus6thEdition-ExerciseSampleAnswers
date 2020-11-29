```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-1 Cd.cpp function definition
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

Cd::Cd(char *s1, char *s2, int n, double x){
    std::strncpy(performers, s1, 50);
    std::strncpy(label, s2, 20);
    selections = n > 0 ? n : 0;
    playtime = x >= 0 ? x : 0;
}

Cd::Cd(const Cd& d){
    std::strcpy(performers, d.performers);
    std::strcpy(label, d.label);
    selections = d.selections;
    playtime = d.playtime;
}

Cd::Cd(){
    std::strcpy(performers, "null");
    std::strcpy(label, "null");
    selections = 0;
    playtime = 0.0;
}

void Cd::Report() const{
    cout << "Performers: " << performers << endl;
    cout << "     Label: " << label << endl;
    cout << "Selections: " << selections << endl;
    cout << "    Playtime: " << playtime << endl;
}

```