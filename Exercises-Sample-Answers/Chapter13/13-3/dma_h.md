```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-3 dma.h header file -> dynamic memory allocation
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

#ifndef _DMA_H_
#define _DMA_H_

#include "ABC.h"
#include <iostream>

class baseDMA: public ABC
{
public:
    baseDMA(const char *lbl = "null", int rt = -1);
    ~baseDMA();
    
    void View() const;
};

class lacksDMA : public ABC
{
private:
    enum {COL_LEN = 40};
    char color[COL_LEN];
public:
    lacksDMA(const char* c = "black", 
        const char *lbl = "null", int rt = -1);
    lacksDMA(const char *c, const ABC &abc);
    ~lacksDMA();
    void View() const;
};

class hasDMA : public ABC
{
private:
    char *style;
public:
    hasDMA(const char* s = "none",
        const char *lbl = "null", int rt = -1);
    hasDMA(const char *s, const ABC &abc);
    hasDMA(const hasDMA &hs);
    ~hasDMA();
    hasDMA &operator=(const hasDMA &hs);
    void View() const;
};

#endif

```