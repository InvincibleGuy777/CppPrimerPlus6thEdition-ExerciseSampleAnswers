```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-5 bankATM.cpp function definition
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

// bankATM.cpp -- using the Queue interface
// compile with queue.cpp
#include<iostream>
#include<cstdlib> // for rand() and srand() and RAND_MAX = Max(rand())
#include<ctime> // for time()
#include<cmath>
#include<string>
#include "Queue.h"
const int MIN_PER_HR = 60;

bool newcustomer(double x); // is there a new customer?

template<typename T>  // to deal with invalid input
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

    Queue line(qs); // line queue holds up to qs people

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
    cout << "Simulation start!\n";
    double perhour = 0.1; // average number of arrival per hour
    double step = perhour / 100;
    double min_per_cust; // average time between arrivals

    while (perhour < 1000){

        min_per_cust = MIN_PER_HR / perhour;

        Item temp; // new customer data
        long turnaways = 0; // turned away by full queue
        long customers = 0; // join the queue
        long served = 0; // served during the simulation
        long sum_line = 0; // cumulative line length
        int wait_time = 0; // time until autoteller is free
        long line_wait = 0; // cumulative time in line

        // running the simulation
        for (int cycle = 0; cycle < cyclelimit; ++cycle){
            if(newcustomer(min_per_cust)){
                if(line.isfull())
                    turnaways++;
                else{
                    customers++;
                    temp.set(cycle); // cycle = time of arrival
                    line.enqueue(temp); // add newcomer to line
                }
            }
            if(wait_time <= 0 && !line.isempty()){
                line.dequeue(temp); // attend next customer
                wait_time = temp.ptime(); // for wait_time minutes
                line_wait += cycle - temp.when();
                served++;
            }
            if(wait_time>0)
                wait_time--;
            sum_line += line.queuecount();
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