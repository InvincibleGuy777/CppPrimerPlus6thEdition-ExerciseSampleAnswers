```cpp
/*
    content: Chapter 12 Coding Exercise Solution 12-3 Stock.cpp function definition
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

// Stock.cpp
#include "Stock.h"
#include<iostream>
#include<cstring>
using std::cout;
using std::endl;

Stock::Stock(){
    company = new char[1];
    company[0] = '\0';
    shares = 0;
    share_val = 0;
    total_val = 0;
}

Stock::Stock(const char* co, long n, double pr){
    company = new char[std::strlen(co)+1];
    std::strcpy(company, co);
    if(n<0){
        cout << "Number of shares can't be negative; "
             << company << " shares set to 0.\n";
        shares = 0;
    }
    else
        shares = n;
    share_val = pr;
    set_tot();
}

Stock::~Stock(){
    cout << company << " object destroyed~\n";
    delete[] company;
}

void Stock::buy(long num, double price){
    if(num<0){
        cout << "Number of shares purchased can't be negative. "
             << "Transaction is aborted.\n";       
    }
    else{
        shares += num;
        share_val = price;
        set_tot();
    }
}

void Stock::sell(long num, double price){
    if(num<0){
        cout << "Number of shares sold can't be negative. "
             << "Transaction is aborted.\n";       
    }
    else if(num > shares){
        cout << "You can't sell more than you have! "
             << "Transaction is aborted.\n";
    }
    else{
        shares -= num;
        share_val = price;
        set_tot();
    }
}

void Stock::update(double price){
    share_val = price;
    set_tot();
}

const Stock& Stock::topval(const Stock& s) const{
    if(s.total_val > total_val)
        return s;
    else
        return *this;
}

// new add-in
Stock::Stock(const Stock &s){
    int len = std::strlen(s.company);
    company = new char[len + 1];
    std::strcpy(company, s.company);
    shares = s.shares;
    share_val = s.share_val;
    set_tot();
}

Stock& Stock::operator=(const Stock& s){
    if(this == &s)
        return *this;
    delete[] company;
    int len = std::strlen(s.company);
    company = new char[len + 1];
    shares = s.shares;
    share_val = s.share_val;
    set_tot();
    return *this;
}
/*
// 公司改名
Stock& Stock::operator=(const char* str){
    delete[] company;
    int len = std::strlen(str);
    company = new char[len + 1];
    return *this;
}
*/
std::ostream& operator<<
(std::ostream &os, const Stock &s){
    using std::ios_base;
    //set format to #.###
    ios_base::fmtflags orig =
        os.setf(ios_base::fixed, ios_base::floatfield);
    std::streamsize prec = cout.precision(3);

    os << "Company: " << s.company
         << " Shares: " << s.shares << '\n';
    os << " Shares Price: $" << s.share_val;
    //set format to #.##
    os.precision(2);
    os << " Total Worth: $" << s.total_val << '\n';

    //restore original format
    os.setf(orig, ios_base::floatfield);
    os.precision(prec);
    return os;
}
```