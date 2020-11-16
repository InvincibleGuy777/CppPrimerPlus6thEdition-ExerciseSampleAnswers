```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-6 bankATM02.cpp
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

/* TARGET
    改进 程序清单 12-12 bank.cpp，包含两个队列，满足：
    - 当第一队人数少于第二队时，客户将排在第一队，否则第二队
    - 找出使平均等候时间为1分钟时，每小时到达的客户数为多少?
*/
// bankATM02.cpp -- using the Queue interface
// compile with queue.cpp
#include<iostream>
#include<cstdlib> // for rand() and srand() and RAND_MAX = Max(rand())
#include<ctime> // for time() and clock()
#include<cmath> // for fabs()
#include<string>
#include "Queue.h"
const int MIN_PER_HR = 60;

bool newcustomer(double x); // is there a new customer?

template<typename T> 
    void invalidInputHandle(T& a, std::string enterText, 
        std::string errorText);
int main(){
    using std::cin;
    using std::cout;
    using std::endl;
    using std::ios_base;
    // setting things up
    std::srand(std::time(0));

    cout << "Case Study: Bank of Heather Automatic Teller\n";
    cout << "Enter maximum size of queue: ";
    int qs;
    cin >> qs;
    // invalid input process
    invalidInputHandle<int>(qs, "Enter maximum size of queue: ",
        "qs must be a positive integer!");

    Queue line1(qs); // line1 queue holds up to qs people
    Queue line2(qs); // line2 queue holds up to qs people

    cout << "Enter the number of simulation hours: ";
    int hours; // hours of simulation
    cin >> hours;
    // invalid input process
    invalidInputHandle<int>(hours, 
        "Enter the number of simulation hours: ",
        "hours must be a positive integer!");
    //simulation will run 1 cycle per minute
    long cyclelimit = MIN_PER_HR * hours; // number of cycles

    clock_t time_start = clock();
    clock_t time_end;
    cout << "Simulation start! (With Two ATMs)\n";
    double perhour = 0.1; // average number of arrival per hour
    double step = perhour / 100;
    double min_per_cust; // average time between arrivals

    while (perhour < 1000){

        min_per_cust = MIN_PER_HR / perhour;

        Item temp; // new customer data
        long turnaways = 0; // turned away by full queue
        long customers = 0; // join the queue
        long served = 0; // served during the simulation
        long sum_line = 0; // cumulative line1 length
        int wait_time_line1 = 0; // time until autoteller #1 is free
        int wait_time_line2 = 0; // time until autoteller #2 is free
        
        long line_wait = 0; // cumulative time in line1

        // running the simulation
        for (int cycle = 0; cycle < cyclelimit; ++cycle){
            if(newcustomer(min_per_cust)){
                if(line1.isfull() && line2.isfull())
                    turnaways++;
                else{
                    customers++;
                    temp.set(cycle); // cycle = time of arrival
                    if(line1.queuecount() <= line2.queuecount())
                        line1.enqueue(temp); // add newcomer to line1
                    else
                        line2.enqueue(temp); // add newcomer to line2
                }
            }
            if(wait_time_line1 <= 0 && !line1.isempty()){
                line1.dequeue(temp); // attend next customer
                wait_time_line1 = temp.ptime(); // for wait_time_line1 minutes
                line_wait += cycle - temp.when();
                served++;
            }
            if(wait_time_line2 <= 0 && !line2.isempty()){
                line2.dequeue(temp); // attend next customer
                wait_time_line2 = temp.ptime(); // for wait_time_line1 minutes
                line_wait += cycle - temp.when();
                served++;
            }
            if(wait_time_line1>0)
                wait_time_line1--;
            if(wait_time_line2>0)
                wait_time_line2--; 
            sum_line += line1.queuecount() + line2.queuecount();
        }
        double avgwaittime = (double)line_wait / served;
        
        const double ERR = 1.0e-3;
        if(std::fabs(avgwaittime-1.0) >= ERR){
            perhour += step;
            continue;
        }
        cout << "Iteration success.\n";
        // reporting results
        if(customers > 0){
            cout << "customers accepted: " << customers << endl;
            cout << "  customers served: " << served << endl;
            cout << "         turnaways: " << turnaways << endl;
            cout << "average queue size: ";
            cout.precision(2);
            cout.setf(ios_base::fixed, ios_base::floatfield);
            cout << (double)sum_line / cyclelimit << endl;
            cout << " average number of customers per hour(Answer): "
                 << perhour << endl;
            cout << " average wait time: "
                << (double)line_wait / served << " minutes\n";
            cout << "Done!\n";
            time_end = clock();
            cout << "Total time cost: "
                 << (time_end - time_start) / CLOCKS_PER_SEC << " s\n";
            cin.get();
            cin.get();
            return 0;
        }
        else{
            cout << "No customers!\n";
            cout << "Done!\n";
            time_end = clock();
            cout << "Total time cost: "
                 << (time_end - time_start) / CLOCKS_PER_SEC << " s\n";
            cin.get();
            cin.get();
            return 0;
        }
            
    }
    cout << "Iteration Failed!\n";

    cin.get(); // filter the ENTER
    cin.get(); // hold the console
    return 0;
}

// x = average time, in minutes, between customers
// return value is true if customer shows up this minute
bool newcustomer(double x){
    return x*std::rand()/RAND_MAX < 1;
}

template<typename T>
void invalidInputHandle(T& a, std::string enterText, 
    std::string errorText){
    using namespace std;
    while (!cin || a<=0){
        if(!cin){
            cin.clear();
        }
        // 过滤剩余字节流
        while (cin.get() != '\n')
            continue;
        cout << "Error input, "<<errorText<<"\n";
        cout << enterText;
        cin >> a;
    }
}

```