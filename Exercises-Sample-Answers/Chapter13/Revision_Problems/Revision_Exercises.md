### Exercises for REVISION

> 1、派生类从基类那里继承了什么?

- 类成员 (public、protected、private修饰的字段和成员函数)



> 2、派生类不能从基类那里继承什么?

- 构造函数
- 析构函数
- 赋值运算符
- 友元


> 3、假设 `baseDMA ::operator=()`函数的返回类型为 `void`，而不是 `baseDMA&`，这将有什么后果? 如果返回类型为 `baseDMA`，而不是 `baseDMA&`，又将有什么后果?

- 情况1的后果仍可以使用单个赋值，但不能使用连锁赋值：

    ```cpp
    baseDMA magazine("Pandering to Glitz", 1);
    baseDMA gift1, gift2, gift3;
    gift1 = magazine; // ok
    gift2 = gift3 = gift1; // no longer valid
    ```
    此时最后一句等效为：`gift2.operator=(gift3.operator=(gift1)->void)`，显然不合法。

- 情况2的后果是：返回的对象是 `*this` 的一份拷贝，如果复制构造函数定义合适的话，顶多使得效率降低，不会有其他后果。

> 4、创建和删除派生类对象时，构造函数和析构函数调用的顺序是怎样的?

- 构造函数自基类起向派生类层层调用。
- 析构函数自派生类起向基类层层调用，与构造函数的调用顺序相反。

> 5、如果派生类没有添加任何数据成员，它是否需要构造函数?
- 需要，每个类都必须有自己的构造函数。如果派生类没有添加新成员，则构造函数可以为空，但必须存在。

> 6、如果基类和派生类定义了同名的方法，当派生类对象调用该方法时，被调用的将是哪个方法?
- 派生类方法。

> 7、在什么情况下，派生类应定义赋值运算符?
- 派生类新增了需要动态内存分配的成员时，与此同时还需定义复制构造函数。

> 8、可以将派生类对象的地址赋给基类指针吗？可以将可以将基类对象赋给派生类指针吗？
- 可以，多态性。
- 也许，只有通过显式类型转换，才可以将基类对象的地址赋给派生类指针（向下转换），而使用这样的指针不一定安全。

> 9、可以将派生类对象赋值给基类对象吗？可以将基类对象赋给派生类对象吗？

- 可以，但程序将使用基类的赋值运算符。
- 也许，仅当派生类定义了转换运算符（即包含将基类引用作为唯一参数的构造函数）或使用基类为参数的赋值运算符时，相反方向的赋值才是可能的。

> 10、假设定义了一个函数，它将基类对象的引用作为参数。为什么该函数也可以将派生类对象作为参数?

- 因为符合C++的向上强制转换机制。从理解层面来说，基类是派生类的一个子集，基类的所有特性派生类都有，因此用基类对象引用没有不妥的地方，它只会访问派生类中的基类特性。

> 11、假设定义了一个函数，它将基类对象作为参数（即函数按值传递基类对象）。为什么该函数也可以将派生类对象作为参数?

- 它与 10 中相比，多了如下过程，即执行复制构造函数将派生类对象转化为基类对象后，作为参数传递给函数。

    ```cpp
    // ClassAB b; where ClassAB inherits ClassA 
    a = ClassA(const ClassA& b);
    fun(a);  // fun(ClassA)
    ```

> 12、为什么通常按引用传递对象比按值传递对象的效率更高？
- 按引用传递对象可以确保函数从虚函数受益
- 按引用传递对象可以节省内存和时间，尤其对于大型对象。
- 按值传递对象的优点是保护原始数据，但可以通过将引用作为 `const` 类型传递来达到同样的目的。

> 13、假设 `Corporation` 是基类， `PublicCorporation` 是派生类。再假设这两个类都定义了 `head` 函数， `ph` 是指向 `Corporation` 类型的指针，且被赋给了一个 `PublicCorporation`对象的地址。如果基类将 `head()` 定义为：\
a. 常规非虚方法； \
b. 虚方法；\
则 `ph->head()` 将被如何执行？

- 情况 a 下被解释为 `ph->Corporation::head()`
- 情况 b 下被解释为 `ph->PublicCorporation::head()`

> 14、下述代码有什么问题？
```cpp
class Kitchen
{
private:
    double kit_sq_ft;
public:
    Kitchen(){kit_sq_ft = 0.0;}
    virtual double area() const{return kit_sq_ft * kit_sq_ft;}
};

class House: public Kitchen
{
private:
    double all_sq_ft;
public:
    House(){all_sq_ft += kit_sq_ft;}
    double area(const char* s) const{cout<<s; return all_sq_ft;}
};
```
- 从设计层面而言：`House` 和 `Kitchen` 不符合 `is-a` 关系，而更符合 `has-a` 关系，因此公有继承不适用。
- 从语法上：派生类和基类的函数 `area()` 的特征标不一致，造成意外的重定义，这将导致基类的虚函数被隐藏，变为不可用。