```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-3 ABC.h header file -> Abstract Base Class
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

#ifndef _ABC_H_
#define _ABC_H_

#include <iostream>

// Abstract Base Class
class ABC
{
private:
    char *label;
    int rating;

protected:
    char *Label() const { return label; }
    int Rating() const { return rating; }
public:
    ABC(const char *lbl = "null", int rt = -1);
    ABC(const ABC& abc);
    virtual ~ABC();

    virtual void View() const = 0; // pure virtual function
    ABC &operator=(const ABC &abc);
    //friend std::ostream &operator<<(std::ostream &os, const ABC &abc); // no longer needed!!
};

#endif

```