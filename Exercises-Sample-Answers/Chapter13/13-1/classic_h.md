```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-1 classic.h header file
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

#ifndef _Classic_H_
#define _Classic_H_
#include "Cd.h"
// base class
class Classic: public Cd{ // represents a CD disk
private:
    char works[50];
public:
    Classic(char* wk, char *s1, char *s2, int n, double x);
    Classic(const Classic& cls);
    Classic();
    void Report() const; // reports all CD data
    //Classic &operator=(const Classic &cls);
};

#endif

```