```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-2 String2.h header file
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
//String2.h -- fixed and augmented String class definition
#ifndef STRING2_H_
#define STRING2_H_

#include<iostream>
using std::istream;
using std::ostream;

class String
{
private:
    char *str; // pointer to string
    int len; // length of string
    static int num_strings; // number of objects
    static const int CINLIM = 80; // cin input limit
public:
    String(const char* s); // constructer
    String(); // default constructer
    String(const String &); //copy constructor
    ~String(); // destructer
    int length() const { return len; }
    void stringlow(); // new 12-2  get every letter to the lower case
    void stringup(); // new 12-2  get every letter to the upper case
    int has(char c); // new 12-2 count the number of char c in the String
    // overloaded operator methods
    String &operator=(const String &);
    String operator+(const String &); // new 12-2 cannot return String&
    String &operator=(const char *);
    char &operator[](int i);
    const char &operator[](int i) const;
    // overloaded operator friends
    friend String operator+(const char *s, const String &st); // new 12-2 cannot return String&
    friend bool operator<(const String &st1, const String &st2);
    friend bool operator>(const String &st1, const String &st2);
    friend bool operator==(const String &st1, const String &st2);
    friend ostream &operator<<
        (ostream &os, const String &st);
    friend istream &operator>>(istream &is, String &st);
    // static function
    static int HowMany();
};
#endif
```