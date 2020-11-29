```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-1 classic.cpp function definition
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

Classic::Classic(char* wk, char *s1, char *s2, int n, double x)
: Cd(s1, s2, n, x){
    std::strncpy(works, wk, 50);
}

Classic::Classic(const Classic& cls): Cd(cls){
    std::strcpy(works, cls.works);
}

Classic::Classic(): Cd(){
    std::strcpy(works, "null");
}

void Classic::Report() const{
    Cd::Report();
    cout << "Main works: " << works << endl;
}

```