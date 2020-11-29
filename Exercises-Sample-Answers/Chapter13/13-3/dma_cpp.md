```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-3 dma.cpp function definition
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

#include "dma.h"
#include <iostream>
#include <cstring>

using std::cout;
using std::endl;
using std::strcpy;
using std::strlen;


baseDMA::baseDMA(const char *lbl, int rt): ABC(lbl, rt){
    cout << "baseDMA(...) object " << this << " created~\n";
}

baseDMA::~baseDMA(){
    cout << "baseDMA object " << this << " destroyed~" << endl;
}

void baseDMA::View() const{
    cout << "\nbaseDMA View(): " << endl;
    cout << " Label: "<<Label() << endl;
    cout << "Rating:"<<Rating() << endl;
}

lacksDMA::lacksDMA(const char* c, const char *lbl, 
int rt): ABC(lbl, rt){
    cout << "lacksDMA(...) object " << this << " created~\n";
    std::strncpy(color, c, COL_LEN);
}

lacksDMA::lacksDMA(const char *c, const ABC &abc): ABC(abc){
    cout << "lacksDMA(..., const&) object " << this << " created~\n";
    std::strncpy(color, c, COL_LEN);
}

lacksDMA::~lacksDMA(){
    cout << "lacksDMA object " << this << " destroyed~" << endl;
}

void lacksDMA::View() const{
    cout << "\nlacksDMA View(): " << endl;
    cout << " Label: "<<Label() << endl;
    cout << "Rating:"<<Rating() << endl;
    cout << " Color: " << color << endl;
}



hasDMA::hasDMA(const char* s, const char *lbl,
 int rt): ABC(lbl, rt){
    cout << "hasDMA(...) object " << this << " created~\n";
    style = new char[strlen(s) + 1];
    strcpy(style, s);
}
hasDMA::hasDMA(const char *s, const ABC &abc): ABC(abc){
    cout << "hasDMA(..., const&) object " << this << " created~\n";
    style = new char[strlen(s) + 1];
    strcpy(style, s);
}

hasDMA::hasDMA(const hasDMA &hs): ABC(hs){
    cout << "hasDMA(const&) object " << this << " created~\n";
    style = new char[strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
}

hasDMA::~hasDMA(){
    cout << "hasDMA object " << this << " destroyed~" << endl;
    delete[] style;
}

hasDMA &hasDMA::operator=(const hasDMA &hs){
    if(this == &hs)
        return *this;
    ABC::operator=(hs);
    delete[] style;
    style = new char[strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
    return *this;
}

void hasDMA::View() const{
    cout << "\nhasDMA View(): " << endl;
    cout << " Label: "<<Label() << endl;
    cout << "Rating:"<<Rating() << endl;
    cout << " Style: " << style << endl;
}

```