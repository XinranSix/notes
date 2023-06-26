![收藏量3696画师画师JW作品80336320_p0](https://github.com/XinranSix/docs/assets/62458905/c8878e22-2c99-471c-91cc-75258aff1118)

[TOC]

## 类和对象

OOP 的三大特性：封装、继承、多态。

`struct` 和 `class` 区别：

在 C++ 中 `struct` 和 `class` 唯一的区别就在于：默认的访问权限不同，`struct` 默认权限为公共，`class` 默认权限为私有。

相较于 C 中的 `struct`，C++ 中的 `struct` 和 `class` 都可以定义自己的成员函数。

**C++ 中的成员权限和继承：**

|     继承方式     | 基类的 `public` 成员  | 基类的 `protected` 成员 | 基类的 `private` 成员 |
| :--------------: | :-------------------: | :---------------------: | :-------------------: |
|  `public` 继承   |  仍为 `public` 成员   |  仍为 `protected` 成员  |        不可见         |
| `protected` 继承 | 变为 `protected` 成员 |  变为 `protected` 成员  |        不可见         |
|  `private` 继承  |  变为 `private` 成员  |   变为 `private` 成员   |        不可见         |

## 对象的初始化和清理

### 构造函数和析构函数

对象的初始化和清理工作是编译器强制要我们做的事情，因此如果**我们不提供构造函数和析构函数，编译器会提供**。编译器提供的构造函数和析构函数是空实现。

-   构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数由编译器自动调用，无须手动调用。
-   析构函数：主要作用在于对象**销毁前**系统自动调用，执行一些清理工作。

构造函数语法：`类名() {}`

1. 构造函数，没有返回值也不写 `void`
2. 函数名称与类名相同
3. 构造函数可以有参数，因此可以发生重载
4. 程序在调用对象时候会自动调用构造，无须手动调用,而且只会调用一次

析构函数语法：`~类名() {}`

1. 析构函数，没有返回值也不写 `void`
2. 函数名称与类名相同，在名称前加上符号  `~`
3. 析构函数不可以有参数，因此不可以发生重载
4. 程序在对象销毁前会自动调用析构，无须手动调用,而且只会调用一次

### 构造函数的分类及调用

**两种分类方式：**

- 按参数分为： 有参构造和无参构造

- 按类型分为： 普通构造和拷贝构造

> 注意：
>
> 1. 如果不提供任何函数，编译器会提供至少 4 个函数：默认构造函数、拷贝构造函数、析构函数、`operator=()`.
> 2. 如果自定义了一个构造函数，编译器不在提供默认构造函数。
> 3. 如果自定义了一个拷贝构造函数，编译器不在提供默认的拷贝构造函数。
> 4. 默认的拷贝构造函数是浅拷贝。

**三种调用方式：**

- 括号法
- 显示法
- 隐式转换法

**示例：**

```C++
#include <iostream>

using namespace std;

class Person {
public:
    Person() { cout << "无参构造函数!" << endl; }

    Person(int a) {
        age = a;
        cout << "有参构造函数!" << endl;
    }

    Person(const Person &p) {
        age = p.age;
        cout << "拷贝构造函数!" << endl;
    }

    ~Person() { cout << "析构函数!" << endl; }

public:
    int age;
};

int main() {

    // 调用无参构造函数
    Person p;

    // 括号法，常用
    Person p1(10);

    // 注意：调用无参构造函数不能加括号，如果加了编译器认为这是一个函数声明
    // Person p2();

    // 显式法
    Person p2 = Person(10);
    Person p3 = Person(p2);

    // Person(10)单独写是匿名对象  当前行结束之后，马上析构

    // 隐式转换法
    Person p4 = 10; // Person p4 = Person(10);
    Person p5 = p4; // Person p5 = Person(p4);

    // 注：不能利用 拷贝构造函数 初始化匿名对象 编译器认为是对象声明
    // Person p5(p4);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/a01c48d7-61f0-4343-a6ff-f8a637c4d55d)

### 拷贝构造函数调用时机

C++ 中拷贝构造函数调用时机通常有三种情况

-   使用一个已经创建完毕的对象来初始化一个新对象。
-   值传递的方式给函数参数传值。
-   以值方式返回局部对象。

> 即：旧对象初始化新对象。
>
> 以值传递返回局部对象在 GCC 中会有优化，可能看到不同的结果。

**示例：**

```C++
#include <iostream>

using namespace std;

class Person {
public:
    Person() {
        cout << "无参构造函数!" << endl;
        mAge = 0;
    }
    Person(int age) {
        cout << "有参构造函数!" << endl;
        mAge = age;
    }
    Person(const Person &p) {
        cout << "拷贝构造函数!" << endl;
        mAge = p.mAge;
    }

    ~Person() { cout << "析构函数!" << endl; }

public:
    int mAge;
};

void test01() {

    Person man(100);
    Person newman(man);
    Person newman2 = man;

    // Person newman3;
    // newman3 = man; //不是调用拷贝构造函数，赋值操作
}

void doWork(Person p1) {}
void test02() {
    Person p;
    doWork(p);
}

Person doWork2() {
    Person p1;
    cout << (int *)&p1 << endl;
    return p1;
}

void test03() {
    Person p = doWork2();
    cout << (int *)&p << endl;
}

int main() {

    test01();
    test02();
    test03();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/6291335b-6b3b-4eaa-b1be-e8a95717e6d5)

###  C++ 默认增加的函数

默认情况下，C++ 编译器至少给一个类添加 3 个函数：

1．默认构造函数

2．默认析构函数

3．默认拷贝构造函数，对属性进行值拷贝

构造函数调用规则如下：

-   如果用户定义有参构造函数，C++ 不在提供默认无参构造，但是会提供默认拷贝构造。

-   如果用户定义拷贝构造函数，C++ 不会再提供其他构造函数。

### 深拷贝与浅拷贝

浅拷贝：简单的赋值拷贝操作。

深拷贝：在堆区重新申请空间，进行拷贝操作。

**示例：**

```C++
#include <iostream>

using namespace std;

class Person {
public:
    Person() { cout << "无参构造函数!" << endl; }

    Person(int age, int height) {

        cout << "有参构造函数!" << endl;

        m_age = age;
        m_height = new int(height);
    }

    Person(const Person &p) {
        cout << "拷贝构造函数!" << endl;
        m_age = p.m_age;
        m_height = new int(*p.m_height);
    }

    ~Person() {
        cout << "析构函数!" << endl;
        if (m_height != nullptr) {
            delete m_height;
        }
    }

public:
    int m_age;
    int *m_height;
};

int main() {

    Person p1(18, 180);

    Person p2(p1);

    cout << "p1的年龄： " << p1.m_age << " 身高： " << *p1.m_height << endl;

    cout << "p2的年龄： " << p2.m_age << " 身高： " << *p2.m_height << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/24dbcb6b-8bf2-4091-b3c2-7ad1a254a7b3)

> 如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题。

### 初始化列表

**语法：**

```c++
构造函数(): 属性1(值1),属性2(值2)...{}
```

> 注意：
>
> 1. 初始化列表是先声明，在调用构造函数时定义并初始化，定义初始化的顺序和声明的顺序一致。
> 2. 普通的构造函数是先定义，在赋值。

**示例：**

```C++
#include <iostream>

using namespace std;

class Person {
public:
    Person(int a, int b, int c) : m_A(a), m_B(b), m_C(c) {}

    void PrintPerson() {
        cout << "mA:" << m_A << endl;
        cout << "mB:" << m_B << endl;
        cout << "mC:" << m_C << endl;
    }

private:
    int m_A;
    int m_B;
    int m_C;
};

int main() {

    Person p(1, 2, 3);
    p.PrintPerson();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/04c95237-ea87-4a09-a521-71b63a5527c5)

### 类对象作为类成员

> - 类中有多个对象时，构造的顺序是先构造里面的对象，再构造外面的对象。
> - 类中有多个对象时，析构时顺序是先析构外面的对象，再析构里面的对象。

**示例：**

```C++
#include <iostream>

using namespace std;

class Phone {
public:
    Phone(string name) {
        m_PhoneName = name;
        cout << "Phone构造" << endl;
    }

    ~Phone() { cout << "Phone析构" << endl; }

    string m_PhoneName;
};

class Person {
public:
    Person(string name, string pName) : m_Name(name), m_Phone(pName) {
        cout << "Person构造" << endl;
    }

    ~Person() { cout << "Person析构" << endl; }

    void playGame() {
        cout << m_Name << " 使用" << m_Phone.m_PhoneName << " 牌手机! " << endl;
    }

    string m_Name;
    Phone m_Phone;
};

int main() {

    Person p("张三", "苹果X");
    p.playGame();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/885cb689-998e-4a26-9819-f934feeb7f43)

### 静态成员

静态成员就是在成员变量和成员函数前加上关键字 `static`.

静态成员分为：

-   静态成员变量
    -   所有对象共享同一份数据
    -   在编译阶段分配内存
    -   类内声明，类外初始化
-   静态成员函数
    -   所有对象共享同一个函数
    -   静态成员函数只能访问静态成员变量

**示例 1 ：**静态成员变量

```C++
#include <iostream>

using namespace std;

class Person {
public:
    static int m_A;

private:
    static int m_B;
};

int Person::m_A = 10;
int Person::m_B = 10;

int main() {

    // 1、通过对象
    Person p1;
    p1.m_A = 100;
    cout << "p1.m_A = " << p1.m_A << endl;

    Person p2;
    p2.m_A = 200;
    cout << "p1.m_A = " << p1.m_A << endl; // 共享同一份数据
    cout << "p2.m_A = " << p2.m_A << endl;

    // 2、通过类名
    cout << "m_A = " << Person::m_A << endl;
    // cout << "m_B = " << Person::m_B << endl; //私有权限访问不到

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/9c1bb88d-dc1b-4ab3-849f-dd2194512563)

**示例 2：**静态成员函数

```C++
#include <iostream>

using namespace std;

class Person {

public:
    // 静态成员函数特点：
    // 1 程序共享一个函数
    // 2 静态成员函数只能访问静态成员变量

    static void func() {
        cout << "func调用" << endl;
        m_A = 100;
        // m_B = 100; //错误，不可以访问非静态成员变量
    }

    static int m_A; // 静态成员变量
    int m_B;

private:
    // 静态成员函数也是有访问权限的
    static void func2() { cout << "func2调用" << endl; }
};

int Person::m_A = 10;

int main() {

    // 静态成员变量两种访问方式

    // 1、通过对象
    Person p1;
    p1.func();

    // 2、通过类名
    Person::func();

    // Person::func2(); //私有权限访问不到

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/e55aee64-5cfc-4e38-9f26-20a53bfbb223)

### `explicit`

`explicit` 修饰的构造函数不能在隐式转换中使用。

## C++对象模型

### 动态对象创建

使用 `malloc` 和 `free` 函数去动态申请对象和释放申请的对象，不会调用构造函数和析构函数。

在 C++ 中建议使用 `new` 运算符和 `delete` 运算符进行动态对象的申请和释放。

语法：

```cpp
类型 *p = new 构造器;
delete p;

// 数组
类型 *p = new 类型[size];
delete []p;
```

> 不要 `delete` 万能指针（`void *`）

### `const` 修饰的静态成员变量

- `const` 修饰的静态成员变量保存在常量区，只读的，在内存中只有一份
- `const` 修饰的静态成员变量可以在类内定义且初始化
- `const` 修饰的静态成员变量可以通过类的作用域访问
- `const` 修饰的静态成员变量可以通过对象访问
- 静态成员函数可以访问 `const` 修饰的静态成员变量

### 成员变量和成员函数分开存储

- 普通成员变量占用对象空间大小
- 静态成员变量不占用对象空间大小
- 普通成员函数不占用对象空间大小
- 静态成员函数不占用对象空间大小

> 在 C++ 中，类内的成员变量和成员函数分开存储，只有非静态成员变量才属于类的对象上

```C++
#include <iostream>

using namespace std;

class Person {
public:
    Person() { mA = 0; }

    int mA;

    static int mB;

    void func() { cout << "mA:" << this->mA << endl; }

    static void sfunc() {}
};

int main() {

    cout << sizeof(Person) << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/aadab981-0981-487a-88b1-340ec574b261)

> 一个对象至少占 1 个字节，要不然获取不到其地址。

### `this` 指针

`this` 指针是一个指向对象自己的指针。

### 空指针访问成员函数

C++ 中空指针也是可以调用成员函数的，但是也要注意有没有用到 `this` 指针。

**示例：**

```C++
#include <iostream>

using namespace std;

class Person {
public:
    void ShowClassName() { cout << "我是Person类!" << endl; }

    void ShowPerson() {
        if (this == nullptr) {
            return;
        }
        cout << mAge << endl;
    }

public:
    int mAge;
};

int main() {

    Person *p = nullptr;
    p->ShowClassName();
    p->ShowPerson();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/abd55810-bb6d-489d-a4bd-624fc10a4f19)

### `const` 修饰成员函数

- 在函数后面加上 `const`，这个是一个常函数
- 常函数内不可以修改成员属性
- 成员属性声明时加关键字 `mutable` 后，在常函数中依然可以修改

> 上述规则对于非成员函数和成员变量也适用。

## 友元

友元可以让一个函数、类或者一个类的成员函数访问另外一个类的私有成员。

有 3 种友元：

-   全局函数做友元
-   类做友元
-   成员函数做友元

### 全局函数做友元

```C++
#include <iostream>

using namespace std;

class Building {
    friend void goodGay(Building *building);

public:
    Building() {
        this->m_SittingRoom = "客厅";
        this->m_BedRoom = "卧室";
    }

public:
    string m_SittingRoom;

private:
    string m_BedRoom;
};

void goodGay(Building *building) {
    cout << "好基友正在访问：" << building->m_SittingRoom << endl;
    cout << "好基友正在访问：" << building->m_BedRoom << endl;
}

int main() {

    Building b;
    goodGay(&b);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/0fda622a-9f93-4072-8152-18f3e277150a)

### 类做友元

```C++
#include <iostream>

using namespace std;

class Building;

class goodGay {
public:
    goodGay();
    void visit();

private:
    Building *building;
};

class Building {

    friend class goodGay;

public:
    Building();

public:
    string m_SittingRoom;

private:
    string m_BedRoom;
};

Building::Building() {
    this->m_SittingRoom = "客厅";
    this->m_BedRoom = "卧室";
}

goodGay::goodGay() { building = new Building; }

void goodGay::visit() {
    cout << "好基友正在访问：" << building->m_SittingRoom << endl;
    cout << "好基友正在访问：" << building->m_BedRoom << endl;
}

int main() {

    goodGay gg;
    gg.visit();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/93e20484-9d59-4566-9c63-30e4e770c3a9)

### 成员函数做友元

```C++
#include <iostream>

using namespace std;

class Building;

class goodGay {
public:
    goodGay();
    void visit();
    void visit2();

private:
    Building *building;
};

class Building {
    friend void goodGay::visit();

public:
    Building();

public:
    string m_SittingRoom;
private:
    string m_BedRoom;
};

Building::Building() {
    this->m_SittingRoom = "客厅";
    this->m_BedRoom = "卧室";
}

goodGay::goodGay() { building = new Building; }

void goodGay::visit() {
    cout << "好基友正在访问" << building->m_SittingRoom << endl;
    cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void goodGay::visit2() {
    cout << "好基友正在访问" << building->m_SittingRoom << endl;
}

int main() {

    goodGay gg;
    gg.visit();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/55166aa2-fa3e-4ba6-b7c2-372e51a1e577)

## 继承

通过继承机制可以利用已有的数据类型来定义新的数据类型，新的类不仅拥有旧类的成员，还拥有新定义的成员。

一个 B 类继承于 A 类，或称从类 A 派生类 B。这样的话，类 A 成为基类， 类 B 成为派生类

派生类中的成员，包含两大部分：一类是从基类继承过来的，一类是自己增加的成员。从基类继承过过来的表现其共性，而新增的成员体现了其个性。

### 继承的语法

```cpp
class 派生类 : 继承方式 基类 {}
```

**C++ 中的成员权限和继承方式：**

|     继承方式     | 基类的 `public` 成员  | 基类的 `protected` 成员 | 基类的 `private` 成员 |
| :--------------: | :-------------------: | :---------------------: | :-------------------: |
|  `public` 继承   |  仍为 `public` 成员   |  仍为 `protected` 成员  |        不可见         |
| `protected` 继承 | 变为 `protected` 成员 |  变为 `protected` 成员  |        不可见         |
|  `private` 继承  |  变为 `private` 成员  |   变为 `private` 成员   |        不可见         |

示例：

```C++
#include <iostream>

using namespace std;

class Animal {
public:
    int age;
    
    void print() { cout << age << endl; }
};

class Dog : public Animal {
public:
    int tail_len;
};

int main() {
    Dog d;
    return 0;
}
```

### 继承中的对象模型

在 C++ 编译器的内部可以理解为结构体，子类是由父类成员叠加子类新成员而成。

```cpp
#include <iostream>

using namespace std;

class Aclass {
public:
    int mA;
    int mB;
};

class Bclass : public Aclass {
public:
    int mC;
};

class Cclass : public Bclass {
public:
    int mD;
};

int main() {
    
    cout << "A size:" << sizeof(Aclass) << endl; // 8
    cout << "B size:" << sizeof(Bclass) << endl; // 12
    cout << "C size:" << sizeof(Cclass) << endl; // 16
    
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/e2072c43-3580-4473-b2e0-2ac533b5e38e)

### 非自动继承的函数

子类不会继承父类的构造函数 、析构函数和 `operator=` 函数。

### 继承中构造和析构顺序

子类对象在创建时会首先调用父类的构造函数，父类构造函数执行完毕后，才会调用子类的构造函数。

当父类构造函数有参数时，需要在子类初始化列表中显示调用父类构造函数。

析构函数调用顺序和构造函数相反。

示例：

```C++
#include <iostream>

using namespace std;

class Base {
public:
    Base() { cout << "Base构造函数!" << endl; }
    ~Base() { cout << "Base析构函数!" << endl; }
};

class Son : public Base {
public:
    Son() { cout << "Son构造函数!" << endl; }
    ~Son() { cout << "Son析构函数!" << endl; }
};

int main() {

    Son s;

    return 0;
}

```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/564d4c31-3b73-4e47-9383-96fac5b9c26f)

### 继承同名成员处理方式

如果子类和父类有同名的成员变量和成员函数，继承时，父类的成员变量和成员函数会被隐藏

-   访问子类同名成员，直接访问即可
-   访问父类同名成员，需要加作用域

示例：

```C++
#include <iostream>

using namespace std;

class Base {
public:
    Base() { m_A = 100; }

    void func() { cout << "Base - func()调用" << endl; }

    void func(int a) { cout << "Base - func(int a)调用" << endl; }

public:
    int m_A;
};

class Son : public Base {
public:
    Son() { m_A = 200; }

    void func() { cout << "Son - func()调用" << endl; }

public:
    int m_A;
};

int main() {

    Son s;

    cout << "Son下的m_A = " << s.m_A << endl;
    cout << "Base下的m_A = " << s.Base::m_A << endl;

    s.func();
    s.Base::func();
    s.Base::func(10);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/410da135-a8cc-4c9b-92fe-00482ee9a60c)

### 继承同名静态成员处理方式

继承时，子类和父类有同名的静态成员函数或静态成员变量，父类中的静态成员函数或静态成员变量会被隐藏。

-   访问子类同名成员，直接访问即可
-   访问父类同名成员，需要加作用域

示例：

```C++
#include <iostream>

using namespace std;

class Base {
public:
    static void func() { cout << "Base - static void func()" << endl; }
    static void func(int a) {
        cout << "Base - static void func(int a)" << endl;
    }

    static int m_A;
};

int Base::m_A = 100;

class Son : public Base {
public:
    static void func() { cout << "Son - static void func()" << endl; }
    static int m_A;
};

int Son::m_A = 200;

int main() {
    
    cout << "通过对象访问：" << endl;
    Son s;
    s.func();
    s.Base::func();

    cout << "通过类名访问：" << endl;
    Son::func();
    Son::Base::func();

    Son::Base::func(100);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/cb7f86e7-b6be-48ad-a9ea-8347a6cd2f3e)

### 多继承

C++ 允许**一个类继承多个类**

语法：

```cpp
class 子类 : 继承方式 父类1, 继承方式 父类2...
```

多继承可能会引发父类中有同名成员出现，需要加作用域区分。

> 实际开发中不建议使用多继承

示例：

```C++
#include <iostream>

using namespace std;

class Base1 {
public:
    Base1() { m_A = 100; }

public:
    int m_A;
};

class Base2 {
public:
    Base2() { m_A = 200; }

public:
    int m_A;
};

class Son : public Base2, public Base1 {
public:
    Son() {
        m_C = 300;
        m_D = 400;
    }

public:
    int m_C;
    int m_D;
};

void test01() {}

int main() {

    Son s;
    cout << "sizeof Son = " << sizeof(s) << endl;
    cout << s.Base1::m_A << endl;
    cout << s.Base2::m_A << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/1f762a21-da8b-409f-a31f-c0d139e57c6c)

### 菱形继承

菱形继承：两个派生类继承同一个基类，又有某个类同时继承者两个派生类，这种继承被称为菱形继承，或者钻石继承。

示例：

```C++
#include <iostream>

using namespace std;

class Animal {
public:
    int m_Age;
};

class Sheep : virtual public Animal {};
class Tuo : virtual public Animal {};

class SheepTuo : public Sheep, public Tuo {};

int main() {

    SheepTuo st;
    st.Sheep::m_Age = 100;
    st.Tuo::m_Age = 200;

    cout << "st.Sheep::m_Age = " << st.Sheep::m_Age << endl;
    cout << "st.Tuo::m_Age = " << st.Tuo::m_Age << endl;
    cout << "st.m_Age = " << st.m_Age << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/ce265823-5977-4432-b125-0e3ca2d8247a)

**虚继承的实现原理：**

![image](https://github.com/XinranSix/docs/assets/62458905/2d2be114-5ca3-40c2-ae80-bce2ca22c92d)

## 多态

### 多态的基本概念

多态分为两类：

-   静态多态：函数重载和运算符重载属于静态多态，复用函数名
-   动态多态：派生类和虚函数实现运行时多态

静态多态和动态多态区别：

-   静态多态的函数地址早绑定：编译阶段确定函数地址
-   动态多态的函数地址晚绑定：运行阶段确定函数地址

多态满足条件：

-   有继承关系
-   子类重写父类中的虚函数

多态使用条件：

-   父类指针或引用指向子类对象

重写：函数返回值类型、函数名、参数列表完全一致称为重写。

### 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为**纯虚函数**

纯虚函数语法：

```cpp
virtual 返回值类型 函数名 （参数列表）= 0;
```

当类中有了纯虚函数，这个类也称为抽象类。

**抽象类特点**：

-   无法实例化对象。
-   子类必须重写抽象类中的纯虚函数，否则也属于抽象类。

### 虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码

解决方式：将父类中的析构函数改为**虚析构**或者**纯虚析构**

虚析构和纯虚析构共性：

-   可以解决父类指针释放子类对象
-   都需要有具体的函数实现

虚析构和纯虚析构区别：

-   如果是纯虚析构，该类属于抽象类，无法实例化对象

虚析构语法：

```cpp
virtual ~类名(){};
```

> 1. 虚析构或纯虚析构用来解决通过父类指针释放子类对象。
> 2. 如果子类中没有堆区数据，可以不写为虚析构或纯虚析构。
> 3. 拥有纯虚析构函数的类也属于抽象类。

### 







