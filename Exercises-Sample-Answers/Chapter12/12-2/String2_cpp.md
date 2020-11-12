```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-1 Cow.cpp function definition
    date-created: 2020-11-12
    date-updated: 2020-11-12
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

//String2.cpp -- String class methods
#include "String2.h"
#include<iostream>
#include<cstring>
#include<cctype>
using std::cin;
using std::cout;

// Initializing static class member

int String::num_strings = 0;

// static method
int String::HowMany(){
    return num_strings;
}

// class methods
String::String(const char* s){
    len = strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    num_strings++;
}

String::String(){ // default constructor
    len = 0;
    str = new char[1];
    str[0] = '\0';
    num_strings++;
}

String::String(const String& st){
    num_strings++;
    len = st.len;
    str = new char[len + 1];
    std::strcpy(str, st.str);
}

String::~String(){ // destructor
    --num_strings;
    delete[] str;
}

// overloaded operator methods

String& String::operator=(const String& st){
    if(this == &st) // cannot copy itself
        return *this;
    delete[] str; // delete the previous string
    len = st.len;
    str = new char[len + 1];
    std::strcpy(str, st.str);
    return *this;
}

String& String::operator=(const char* s){
    delete[] str; // delete the previous string
    len = std::strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    return *this;
}

// read-write char access for non-const String
// not available for (const char) as it may update the char
char& String::operator[](int i){
    return str[i];
}

// read-only char access for const String
const char& String::operator[](int i) const{
    return str[i];
}

//overloaded operator friends

bool operator<(const String& st1, const String& st2){
    return (std::strcmp(st1.str, st2.str) < 0);
}
bool operator>(const String& st1, const String& st2){
    return st2 < st1;
}
bool operator==(const String& st1, const String& st2){
    return (std::strcmp(st1.str, st2.str) == 0);
}

// simple String output
std::ostream& operator<<
(std::ostream& os, const String& st)
{
    os << st.str;
    return os;
}
// quick and dirty String input
istream& operator>>(istream& is, String& st){
    char temp[String::CINLIM];
    is.get(temp, String::CINLIM);
    if(is)
        st = temp;
    while (is && is.get() != '\n')
        continue;
    return is;
}

// new 12-2 definition

String String::operator+(const String & st){
    // 不要用 strcat()直接连接，在此前一定要new[]一下，
    //否则执行析构函数时由于delete[] 和 new[]不成对而引发异常
    String ret;
    ret.len = len + st.len;
    ret.str = new char[ret.len + 1];
    std::strcpy(ret.str, str);
    std::strcat(ret.str, st.str);
    return ret;
}

String operator+(const char *s, const String &st){
    return String(s) + st;
}

void String::stringlow(){
    for (int i = 0; i < len; ++i)
        if(isupper(str[i]))
            str[i] += 32;
}

void String::stringup(){
    for (int i = 0; i < len; ++i)
        if(islower(str[i]))
            str[i] -= 32;
}

int String::has(char c){
    int count = 0;
    for (int i = 0; i < len; ++i)
        if(c == str[i])
            ++count;
    return count;
}

```