```cpp
/*
    content: Chapter 13 Coding Exercise Solution 13-3 useABC_DMA.cpp 
                                        -> use of ABC and its derived classes
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

// example of Abstract Base Type
#include "dma.h"
#include <iostream>
#include <cstdio>
const int DMA_NUM = 4;

int main(){
    using std::cin;
    using std::cout;
    using std::endl;
    {
    ABC *p_dmas[DMA_NUM];
    char tmp_label[50];
    int tmp_rating;
    char kind;

    for (int i = 0; i<DMA_NUM; ++i){
        cout << "Enter dma's label: ";
        cin.getline(tmp_label, 50);
        cout << "Enter dma's rating: ";
        cin >> tmp_rating;
        while (!cin || tmp_rating <= 0){
            if(!cin)
                cin.clear();
            while (cin.get() != '\n')
                continue;
            cout << "Invalid input, rating must be a positive integer!\n";
            cout << "Enter dma's rating: ";
            cin >> tmp_rating;
        }
        // filter the input such as "123aasfs"
        while (cin.get() != '\n')
            continue;
        cout<<"Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: ";
        while (cin>>kind &&  // what if we input '45678'?
            (kind != '1' && kind != '2' && kind != '3')){
                // filter the input such as "123aasfs"
            while (cin.get() != '\n')
                continue;
            cout<<"Enter 1 for baseDMA or 2 for lacksDMA or 3 for hasDMA: ";
        }
            
        switch (kind)
        {
        case '1':
            p_dmas[i] = new baseDMA(tmp_label, tmp_rating);
            break;
        case '2':
            char tcolor[20];
            cout << "Enter a color: ";
            cin >> tcolor;
            p_dmas[i] = new lacksDMA(tcolor, tmp_label, tmp_rating);
            break;
        case '3':
            char tstyle[50];
            cout << "Enter a style: ";
            cin >> tstyle;
            p_dmas[i] = new hasDMA(tstyle, tmp_label, tmp_rating);
        }
        while (cin.get() != '\n')
            continue;
    }
    cout << endl;

    for (int i = 0; i < DMA_NUM; ++i)
        p_dmas[i]->View();

    for (int i = 0; i < DMA_NUM; ++i)
        delete p_dmas[i];

    cout << "Done.\n";
    }
    cin.get();
    cin.get();
    return 0;
}

```