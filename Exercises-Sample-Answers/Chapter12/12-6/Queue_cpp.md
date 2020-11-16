```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-6 Queue.cpp function definition
    date-created: 2020-11-16
    date-updated: 2020-11-16
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/
#include "Queue.h"
#include <cstdlib>
#include <iostream>

Queue::Queue(int qs):qsize(qs){
    front = rear = NULL;
    items = 0;
}
Queue::~Queue(){
    Node *temp;
    while (front != NULL){
        temp = front;
        front = front->next;
        delete temp;
    }
}
bool Queue::isempty() const{
    return items == 0;
}
bool Queue::isfull() const{
    return items == qsize;
}
int Queue::queuecount() const{
    return items;
}
// add item to end
bool Queue::enqueue(const Item &item){
    if(isfull())
        return false;
    Node *add = new Node;
    // on failure, new throws std::bad_alloc exception
    add->item = item;
    add->next = NULL;
    items++;
    if(front == NULL)
        front = add;
    else
        rear->next = add;
    rear = add;
    return true;
}
// remove item from front
bool Queue::dequeue(Item &item){
    if(front == NULL)
        return false;
    item = front->item;
    items--;
    Node *temp = front;
    front = front->next;
    delete temp;
    if(items == 0)
        rear = NULL;
    return true;
} 

void Customer::set(long when){
    processtime = std::rand() % 3 + 1;
    arrive = when;
}


```