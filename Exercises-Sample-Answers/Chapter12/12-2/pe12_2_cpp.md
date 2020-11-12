```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-1 pe12_2.cpp test of the new class String2
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

//pe12_2.cpp
#include<iostream>
using namespace std;
#include "String2.h"

int main(){
    String s1(" and I am a C++ student.");
    String s2 = "Please enter your name: ";
    String s3;
    cout << s2; // overloaded << operator
    cin >> s3; // overloaded >> operator
    s2 = "My name is " + s3; // overloaded =, + operator
    cout << s2 << ".\n";
    s2 = s2 + s1;
    s2.stringup(); // converts string to uppercase
    cout << "The string\n"
         << s2 << "\ncontains " << s2.has('A')
         << " 'A' characters in it.\n";
    s1 = "red"; // String(const char*) 
                // then String& operator=(const String&)
    String rgb[3] = {String(s1), String("green"), String("blue")};
    cout << "Enter the name of a primary color for mixing light: ";
    String ans;
    bool success = false;
    while (cin>>ans){
        ans.stringlow(); // converts string to lowercase
        for (int i=0; i<3; ++i){
            if(ans == rgb[i]){ // overloaded == operator
                cout << "That's right.\n";
                success = true;
                break;
            }
        }
        if(success)
            break;
        else
            cout << "Try again!\n";
    }
    cout << "Bye\n";
    cin.get();
    cin.get();
    return 0;
}
```