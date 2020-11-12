```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-1 Cow.cpp function definition
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
#include<iostream>
#include<cstring>
#include "Cow.h"
using std::cout;
using std::endl;
using std::strcpy;
using std::strlen;
using std::strncpy;

Cow::Cow(){
    strcpy(name, "Default");
    hobby = new char[1];
    hobby[0] = '\0';
    weight = 0;
}

Cow::Cow(const char* nm, const char* ho, double wt){
    int len = strlen(ho);
    hobby = new char[len + 1];
    strncpy(name, nm, 20);
    strcpy(hobby, ho);
    weight = wt;
}

Cow::Cow(const Cow& c){
    strcpy(name, c.name);
    int len = strlen(c.hobby);
    hobby = new char[len + 1];
    strcpy(hobby, c.hobby);
    weight = c.weight;
}

Cow::~Cow(){
    delete[] hobby;
    hobby = nullptr;
    cout << "Cow " << name << " destroyed~\n";
}

Cow& Cow::operator=(const Cow& c){
    if(this == &c)
        return *this;
    delete[] hobby;
    int len = strlen(c.hobby);
    hobby = new char[len + 1];
    strcpy(name, c.name);
    strcpy(hobby, c.hobby);
    weight = c.weight;
    return *this;
}

void Cow::ShowCow() const{
    cout << "name: " << name << endl;
    cout << "hobby: " << hobby << endl;
    cout << "weight: " << weight << endl;
}
```