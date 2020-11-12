```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-1 Cow.h header file
    date: 2020-11-12
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/
#ifndef COW_H_
#define COW_H_

class Cow{
    char name[20];
    char *hobby;
    double weight;
public:
    Cow();
    Cow(const char *nm, const char *ho, double wt);
    Cow(const Cow& c);
    ~Cow();
    Cow &operator=(const Cow &c);
    void ShowCow() const; // display all data
};


#endif

```