```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-6 Queue.h header file
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

// Queue.h -- interface for a queue
#ifndef QUEUE_H_
#define QUEUE_H_

// This queue will contain Customer items
class Customer
{
private:
    long arrive; // arrival time for customer
    int processtime; // processing time for customer
public:
    Customer() { arrive = processtime = 0; }

    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processtime; }
};

typedef Customer Item;

class Queue{
private:
    enum
    {
        Q_SIZE = 10
    };
    //ERR: 不能将 "Queue::Node *" 类型的值分配到 "Queue::Node *" 类型的实体
    /*
    struct Node
    {
        Item item;
        struct Node *next;
    } ;
    */
    typedef struct node // 不能缺少typedef，原因如上
    {
        Item item;
        struct node *next;
    } Node;
    //private class members
    Node *front;
    Node *rear;
    int items; // current numbers of items in Queue
    const int qsize; // maximum number of items in Queue
    // preemptive definitions to prevent public copying
    Queue(const Queue& q):qsize(0){}
    Queue &operator=(const Queue &q) { return *this; }

public:
    Queue(int qs = Q_SIZE);
    ~Queue();
    bool isempty() const;
    bool isfull() const;
    int queuecount() const;
    bool enqueue(const Item &item); // add item to end
    bool dequeue(Item &item); // remove item from front
};

#endif

```