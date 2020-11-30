```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-4 port.cpp function definition
    date-created: 2020-11-30
    date-updated: 2020-11-30
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

#include "port.h"
#include <iostream> // using namespace std;
#include <cstring>


/*function definitions for class Port*/

Port::Port(const char* br, const char* st, int b){
    brand = new char[strlen(br) + 1];
    strcpy(brand, br);
    strcpy(style, st);
    bottles = b;
}

Port::Port(const Port &p){
    brand = new char[strlen(p.brand) + 1];
    strcpy(brand, p.brand);
    strcpy(style, p.style);
    bottles = p.bottles;
}

Port &Port::operator=(const Port &p){
    if(this == &p)
        return *this;
    delete[] brand;
    brand = new char[strlen(p.brand) + 1];
    strcpy(brand, p.brand);
    strcpy(style, p.style);
    bottles = p.bottles;
    return *this;
}

Port &Port::operator+=(int b){
    bottles += b;
    return *this;
}

Port &Port::operator-=(int b){
    if(bottles < b)
        cout << "No enough available bottles!" << endl;
    else
        bottles -= b;
    return *this;
}

void Port::Show() const{
    cout << "  Brand: " << brand << endl;
    cout << "   Kind: " << style << endl;
    cout << "Bottles: " << bottles << endl;
}

ostream &operator<<(ostream &os, const Port &p){
    os << p.brand << ", ";
    os << p.style << ", ";
    os << p.bottles;
    return os;
}


/*function definitions for class VintagePort*/

VintagePort::VintagePort(): Port(){
    nickname = new char[5];
    strcpy(nickname, "null");
    year = 0;
}

VintagePort::VintagePort(const char *br, int b, 
const char *nn, int y): Port(br, "vintage", b){
    nickname = new char[strlen(nn) + 1];
    strcpy(nickname, nn);
    year = y;
}

VintagePort::VintagePort(const VintagePort &vp): Port(vp){
    nickname = new char[strlen(vp.nickname) + 1];
    strcpy(nickname, vp.nickname);
    year = vp.year;
}

VintagePort &VintagePort::operator=(const VintagePort &vp){
    if(this == &vp)
        return *this;
    delete[] nickname;
    nickname = new char[strlen(vp.nickname) + 1];
    strcpy(nickname, vp.nickname);
    year = vp.year;
    Port::operator=(vp);
    return *this;
}

void VintagePort::Show() const{
    Port::Show();
    cout << "NickName: " << nickname << endl;
    cout << "    Year: " << year << endl;
}

ostream &operator<<(ostream &os, const VintagePort &vp){
    os << (const Port &) vp;
    os << ", " << vp.nickname << ", " << vp.year;
    return os;
}

```