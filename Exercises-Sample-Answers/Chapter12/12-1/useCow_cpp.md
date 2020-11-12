```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-1 useCow.cpp the use of class Cow
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
#include "Cow.h"

int main(){
    using std::cout;
    using std::endl;
    {
        Cow c1;
        cout << "cow1\n";
        c1.ShowCow();
        cout << "\n"<<"cow2\n";
        Cow c2 = Cow("YoYo", "Kick ass", 34.5);
        c2.ShowCow();
        cout << "\n"<<"use copy constructor to initialize cow3\n";
        cout << "\n"<<"cow3\n";
        Cow c3(c1);
        c3.ShowCow();
        cout << "\n"<<"Now assign cow2 to cow3\n";
        c3 = c2;
        cout << "\n"<<"cow3\n";
        c3.ShowCow();
    }
    cout << "Done!\n";
    std::cin.get();
    return 0;
}
```