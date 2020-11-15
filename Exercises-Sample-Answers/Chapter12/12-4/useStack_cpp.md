```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-4 useStack.cpp use of class Stack
    date-created: 2020-11-15
    date-updated: 2020-11-15
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

// useStack.cpp -- use the new class Stack
#include<iostream>
#include "Stack.h"
using std::cin;
using std::cout;
using std::endl;


int main(){
    {  // local scope to see the destructor performance 
    Stack st1(4);
    Stack st2;
    Item item;
    int cnt = 0;
    cout << "Enter an item to push into the stack (#"<<cnt+1<<"): ";
    cin >> item;  
    while (cnt<5){
        while(!cin){
            cin.clear();
            while (cin.get() != '\n')
                continue;
            cout << "Invalid input! Item must be a long integer!\n";
            cout << "Enter an item to push into the stack (#"<<cnt+1<<"): ";
            cin >> item;
        }
        // filter the remnant char
        // eg: "123aa" is valid for the current input, but invalid for the next
        while (cin.get() != '\n') 
            continue;
        bool flag = st1.push(item);
        if(!flag){
            cout << "stack #1 is full now.\n push fail~ Loop exit.\n";
            break;
        }
        else
            cout << "item " << item << " push success.\n";
        ++cnt;
        if(cnt == 5)
            break;
        cout << "Enter an item to push into the stack (#"<<cnt+1<<"): ";
        cin >> item;
    }
    cout << "copy stack #1 to stack #3:\n";
    Stack st3(st1);
    cout << "pop stack #3 until it's empty:\n";
    cnt = 0;
    while (st3.pop(item)){
        cout << "stack #3 pop out item #" 
            <<cnt+1<<": "<< item << endl;
        cnt++;
    }
    cout << "stack #3 has " << cnt << " " 
         << (cnt > 1 ? "elements" : "element") << " in total.\n";

    cout << "\nPop out one element in stack #1\n";
    st1.pop(item);

    cout << "\nAssign stack #1 to stack #2:\n";
    st2 = st1;

    cout << "pop stack #2 until it's empty:\n";
    cnt = 0;
    while (st2.pop(item)){
        cout << "stack #2 pop out item #" 
            <<cnt+1<<": "<< item << endl;
        cnt++;
    }
    cout << "stack #2 has " << cnt << " " 
         << (cnt > 1 ? "elements" : "element") << " in total.\n";

    cout << "Done!\n";
    cout << "\n"
         << "Before stacks destroy: ";
    cout << "Stack #1 ADDR: " << &st1<<endl;
    cout << "Stack #2 ADDR: " << &st2<<endl;
    cout << "Stack #3 ADDR: " << &st3<<endl;
    cout << "Now destructors executing:\n";
    }
    cin.get();
    cin.get();
    return 0;
}
```