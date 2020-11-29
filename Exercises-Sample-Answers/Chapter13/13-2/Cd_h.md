```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-2 Cd.h header file (DMA version)
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

#ifndef _Cd_H_
#define _Cd_H_

// base class
class Cd{ // represents a CD disk
private:
    char *performers;
    char* label;
    int selections; // number of selections
    double playtime; // playing time in minutes
public:
    Cd(char *s1, char *s2, int n, double x);
    Cd(const Cd& d);
    Cd();
    virtual ~Cd();
    virtual void Report() const; // reports all CD data
    Cd &operator=(const Cd &d);
};

#endif

```