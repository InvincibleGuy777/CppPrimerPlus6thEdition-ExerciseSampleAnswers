```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-2 useClassic.cpp use of class Cd and derived class Classic (DynamicMemoryAllocation version)
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

#include <iostream>
using namespace std;
#include "classic.h" 

void Bravo(const Cd &disk);

int main(){
    {
    Cd c1("Beatles", "Capitol", 14, 35.5);
    Classic c2("Piano Sonata in B flat, Fantasia in C", 
        "Alfred Brendel", "Philips", 2, 57.17);

    Cd *pcd = &c1;
    cout << "Using object directly:\n";
    c1.Report();
    c2.Report();

    cout << "\nUsing type cd* pointer to objects:\n";
    pcd->Report();
    pcd = &c2;
    pcd->Report();

    cout << "\nCalling a function with a Cd reference argument:\n";
    Bravo(c1);
    Bravo(c2);

    cout << "\nTesting assignment: \n";
    Classic copy;
    copy = c2;
    copy.Report();
    }
    std::cin.get();
    return 0;
}

void Bravo(const Cd& disk){
    disk.Report();
}

```