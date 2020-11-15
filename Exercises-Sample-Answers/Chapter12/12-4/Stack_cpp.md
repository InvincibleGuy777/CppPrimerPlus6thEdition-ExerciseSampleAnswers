```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-4 Stack.cpp function definition
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

// Stack.cpp
#include "Stack.h"
#include <iostream>
using std::cout;

Stack::Stack(int n){
    if(n<0){
        cout << "Number n can't be negative! "
             << "Set n to MAX = " << MAX<<".\n";
        n = MAX;
    }
    pitems = new Item[n];
    size = n;
    top = 0;
}

Stack::Stack(const Stack& st){
    size = st.size;
    pitems = new Item[size];
    for (top = 0; top < st.top; ++top)
        pitems[top] = st.pitems[top];
}

Stack::~Stack(){
    cout << "Stack " << this << " destroyed~\n";
    delete[] pitems;
}

bool Stack::isempty() const{
    return top == 0;
}

bool Stack::isfull() const{
    return top == size;
}

bool Stack::push(const Item& item){
    if(top<size){
        pitems[top++] = item;
        return true;
    }
    else
        return false;
}

bool Stack::pop(Item& item){
    if(top > 0){
        item = pitems[--top];
        return true;
    }
    else
        return false;
}

Stack& Stack::operator=(const Stack& st){
    if(this == &st)
        return *this;
    delete[] pitems;
    size = st.size;
    pitems = new Item[size];
    for (top = 0; top < st.top; ++top)
        pitems[top] = st.pitems[top];
    return *this;
}

```