```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-4 usePort.cpp -> use of class Port and VintagePort
    date-created: 2020-11-30
    date-updated: 2020-11-30
    Editor: VS Code 
    Compiler: g++
    Debugger: gdb
    Version : C++11
    author: InvincibleGuy777  (Chenchen Xu)
    github url:  https://github.com/InvincibleGuy777/CppPrimerPlus6thEdition-LearningNotes
    e-mail: 2540588513@qq.com  / a2540588513@stu.xjtu.edu.cn
    csdn blog url: https://me.csdn.net/weixin_42430021
*/

#include "port.h"
#include <iostream>
#include <cctype>
#include <cstring>
const int NUM_PORT = 4;

// get the lowercase of string s
const char *TOLOWERSTR(const char* s, char* out);
// get rid of the space on both side of string s
char *TRIM(char *s);

int main(){
    using std::cin;
    using std::cout;
    using std::endl;

    Port *p_ports[NUM_PORT];
    char temp[20];
    char tmp_brand[50];
    char tmp_style[20];
    int tmp_bottles;
    bool isVintage[NUM_PORT]{0};

    for (int i = 0; i<NUM_PORT; ++i){

        cout << "Enter port's brand: ";
        cin.getline(tmp_brand, 50);

        cout << "Enter port's total bottles: ";
        cin >> tmp_bottles;
        // deal with the invalid input
        while (!cin || tmp_bottles <= 0){
            if(!cin)
                cin.clear();
            while (cin.get() != '\n')
                continue;
            cout << "Invalid input, bottles must be a non-negative integer!\n";
            cout << "Enter port's total bottles: ";
            cin >> tmp_bottles;
        }

        // filter the input such as '123aaavdd'
        while (cin.get() != '\n')
            continue;

        cout << "Enter port's kind: ";
        cin.getline(tmp_style, 20);
        
        if(strcmp(TOLOWERSTR(TRIM(tmp_style), temp), "vintage") == 0){
            isVintage[i] = true;
            cout << "Enter the nickname of vintage port: ";
            char tmp_nickname[50];
            cin.getline(tmp_nickname, 50);
        
            cout << "Enter the vintage year of vintage port: ";
            int tmp_year;
            cin >> tmp_year;
            // deal with the invalid input
            while (!cin || tmp_year <= 0){
                if(!cin)
                    cin.clear();
                while (cin.get() != '\n')
                    continue;
                cout << "Invalid input, vintage year must be a positive integer!\n";
                cout << "Enter the vintage year of vintage port: ";
                cin >> tmp_year;
            }
            // filter the input such as '123aaa'
            while (cin.get() != '\n')
                continue;
            p_ports[i] = new VintagePort(tmp_brand, tmp_bottles, tmp_nickname, tmp_year);
        }
        else
            p_ports[i] = new Port(tmp_brand, tmp_style, tmp_bottles);

        cout << endl;
    }

    cout << "Use of virtual function Show(): "<<endl;
    for (int i = 0; i < NUM_PORT; ++i)
        p_ports[i]->Show();
    cout << endl;

    cout << "Use of operator<<(): " << endl;
    for (int i = 0; i < NUM_PORT; ++i)
        if(isVintage[i])
            cout <<(const VintagePort &)*p_ports[i] << endl;
        else
            cout << *p_ports[i] << endl;
        
    for (int i = 0; i < NUM_PORT; ++i)
        delete p_ports[i];

    cout << "Done.\n";

    cin.get();
    cin.get();
    return 0;
}

// get the lowercase of string s
const char *TOLOWERSTR(const char* s, char* out){
    int i;
    //cout << "len: " << strlen(s) << endl;
    for (i = 0; i < strlen(s); i++)
        out[i] = tolower(s[i]);
    out[i] = '\0';
    return out;
}

// get rid of the space on both side of string s
char *TRIM(char *s){
    int p = 0, r = strlen(s)-1;
    while (p<r && s[p] == ' ')
        p++;
    while (r>p && s[r] == ' ')
        r--;
    
    int len = s[p] == ' '? 0: r - p + 1;
    int i = 0;
    while (i < len)
        s[i++] = s[p++];
    s[len] = '\0';
    return s;
}

```