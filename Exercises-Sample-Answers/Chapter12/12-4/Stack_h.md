```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-4 Stack.h header file
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

// Stack.h -- class declaration for the stack ADT
#ifndef STACK_H_
#define STACK_H_
typedef unsigned long Item;

class Stack{
private:
    enum{MAX = 10};
    Item *pitems;
    int size;
    int top;
public:
    Stack(int n = MAX); // create stack with n elements
    Stack(const Stack &st);
    ~Stack();
    bool isempty() const;
    bool isfull() const;
    // push() returns false if stack already is full, true otherwise
    bool push(const Item &item); // add item to stack
    // pop() returns false if stack already is empty, true otherwise
    bool pop(Item &item); // pop top into item
    Stack &operator=(const Stack &st);
};
#endif

```