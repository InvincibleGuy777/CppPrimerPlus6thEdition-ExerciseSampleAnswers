```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-2 classic.cpp function definition (DMA version)
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

#include "classic.h"
#include <iostream>
#include <cstring>

using std::cout;
using std::endl;
using std::strlen;

Classic::Classic(char* wk, char *s1, char *s2, int n, double x)
: Cd(s1, s2, n, x){
    works = new char[strlen(wk) + 1];
    std::strcpy(works, wk);
    cout << "Classic(...) Object " << this << " created~" << endl;
}

Classic::Classic(const Classic& cls): Cd(cls){
    works = new char[strlen(cls.works) + 1];
    std::strcpy(works, cls.works);
    cout << "Classic(const&) Object " << this << " created~" << endl;
}

Classic::Classic(): Cd(){
    works = new char[5];
    std::strcpy(works, "null");
    cout << "Classic() Object " << this << " created~" << endl;
}

Classic::~Classic(){
    cout << "Classic Object " << this << " destroying~" << endl;
    delete[] works;
}

void Classic::Report() const{
    Cd::Report();
    cout << "Main works: " << works << endl;
}

Classic& Classic::operator=(const Classic& cls){
    if(this == &cls)
        return *this;
    Cd::operator=(cls);
    delete[] works;
    works = new char[strlen(cls.works) + 1];
    std::strcpy(works, cls.works);
    return *this;
}

```