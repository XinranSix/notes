![收藏量4433画师ぴっぴ作品58918055_p6](https://github.com/XinranSix/docs/assets/62458905/3746d246-4831-45c5-b3d1-d92a2b2f2cad)

[TOC]

## 模板概述

类型以参数的形式指定，这样的函数或类称为函数模板或类模板。

模板的特点：

-   模板不可以直接使用，它只是一个框架
-   模板的通用并不是万能的

## 函数模板

### 函数模板语法

语法：

```C++
template<typename T>
函数声明或定义
```

解释：

`template`：声明创建模板

`typename`：表面其后面的符号是一种数据类型，可以用 `class` 代替

`T`：通用的数据类型，名称可以替换，通常为大写字母。

示例：

```C++
#include <iostream>

using namespace std;

template<typename T>
void mySwap(T &a, T &b) {
    T temp = a;
    a = b;
    b = temp;
}

int main() {

    int a = 10;
    int b = 20;

    mySwap(a, b);
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;

    mySwap<int>(a, b);
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;

    return 0;
}
```

> - 使用函数模板有两种方式：自动类型推导、显示指定类类型。

### 普通函数与函数模板的区别

-   普通函数调用时可以发生自动类型转换
-   函数模板调用时，如果利用自动类型推导，不会发生隐式类型转换
-   如果利用显示指定类型的方式，可以发生隐式类型转换

**示例：**

```C++
#include <iostream>

using namespace std;

int myAdd01(int a, int b) { return a + b; }

template<class T>
T myAdd02(T a, T b) {
    return a + b;
}

int main() {

    int a = 10;
    int b = 20;
    char c = 'c';

    cout << myAdd01(a, c)
         << endl; // 正确，将char类型的'c'隐式转换为int类型  'c' 对应 ASCII码 99

    // myAdd02(a, c); // 报错，使用自动类型推导时，不会发生隐式类型转换

    myAdd02<int>(a, c); // 正确，如果用显示指定类型，可以发生隐式类型转换

    return 0;
}
```

### 普通函数与函数模板的调用规则

调用规则如下：

1. 如果函数模板和普通函数都可以实现，优先调用普通函数
2. 可以通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配，优先调用函数模板

**示例：**

```C++
#include <iostream>

using namespace std;

void myPrint(int a, int b) { cout << "调用的普通函数" << endl; }

template<typename T>
void myPrint(T a, T b) {
    cout << "调用的模板" << endl;
}

template<typename T>
void myPrint(T a, T b, T c) {
    cout << "调用重载的模板" << endl;
}

int main() {

    int a = 10;
    int b = 20;
    myPrint(a, b);

    myPrint<>(a, b);

    int c = 30;
    myPrint(a, b, c);

    char c1 = 'a';
    char c2 = 'b';
    myPrint(c1, c2);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/47ba3b3a-f042-419a-b52e-d78264729b1d)

> 既然提供了函数模板，最好就不要提供普通函数，否则容易出现二义性

### 模板具体化

```cpp
#include <iostream>

using namespace std;

class Person {
public:
    Person(string name, int age) {
        this->mName = name;
        this->mAge = age;
    }
    string mName;
    int mAge;
};

// 普通交换函数
template<class T>
void mySwap(T &a, T &b) {
    T temp = a;
    a = b;
    b = temp;
}

// 第三代具体化，显示具体化的原型和定意思以template<>开头，并通过名称来指出类型
// 具体化优先于常规模板
template<>
void mySwap<Person>(Person &p1, Person &p2) {
    string nameTemp;
    int ageTemp;
    nameTemp = p1.mName;
    p1.mName = p2.mName;
    p2.mName = nameTemp;

    ageTemp = p1.mAge;
    p1.mAge = p2.mAge;
    p2.mAge = ageTemp;
}

int main() {
    Person P1("Tom", 10);
    Person P2("Jerry", 20);

    cout << "P1 Name = " << P1.mName << " P1 Age = " << P1.mAge << endl;
    cout << "P2 Name = " << P2.mName << " P2 Age = " << P2.mAge << endl;
    mySwap(P1, P2);
    cout << "P1 Name = " << P1.mName << " P1 Age = " << P1.mAge << endl;
    cout << "P2 Name = " << P2.mName << " P2 Age = " << P2.mAge << endl;
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/5db85779-39da-4375-b6a0-5df97b9cb032)

## 类模板

### 类模板语法

语法：

```c++
template<typename T>
类
```

解释：

`template`：声明创建模板

`typename`：表明其后面的符号是一种数据类型，可以用 `class` 代替

`T`：通用的数据类型，名称可以替换，通常为大写字母。

### 类模板与函数模板区别

类模板与函数模板区别主要有两点：

1. 类模板没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数

### 类模板中成员函数创建时机

类模板中成员函数和普通类中成员函数创建时机是有区别的：

-   普通类中的成员函数一开始就可以创建
-   类模板中的成员函数在调用时才创建

### 类模板对象做函数参数

一共有三种传入方式：

1. 指定传入的类型：直接显示对象的数据类型
2. 参数模板化：将对象中的参数变为模板进行传递
3. 整个类模板化：将这个对象类型 模板化进行传递

示例：

```C++
#include <iostream>
#include <string>

using namespace std;

// 类模板
template<class NameType, class AgeType = int>
class Person {
public:
    Person(NameType name, AgeType age) {
        this->mName = name;
        this->mAge = age;
    }
    void showPerson() {
        cout << "name: " << this->mName << " age: " << this->mAge << endl;
    }

public:
    NameType mName;
    AgeType mAge;
};

// 1、指定传入的类型
void printPerson1(Person<string, int> &p) { p.showPerson(); }
void test01() {
    Person<string, int> p("孙悟空", 100);
    printPerson1(p);
}

// 2、参数模板化
template<class T1, class T2>
void printPerson2(Person<T1, T2> &p) {
    p.showPerson();
    cout << "T1的类型为： " << typeid(T1).name() << endl;
    cout << "T2的类型为： " << typeid(T2).name() << endl;
}
void test02() {
    Person<string, int> p("猪八戒", 90);
    printPerson2(p);
}

// 3、整个类模板化
template<class T>
void printPerson3(T &p) {
    cout << "T的类型为： " << typeid(T).name() << endl;
    p.showPerson();
}
void test03() {
    Person<string, int> p("唐僧", 30);
    printPerson3(p);
}

int main() {

    test01();
    test02();
    test03();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/f5a28448-c050-4ebc-95da-e91de12db7d2)

### 类模板与继承

当类模板碰到继承时，需要注意一下几点：

-   当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中 T 的类型
-   如果不指定，编译器无法给子类分配内存
-   如果想灵活指定出父类中 T 的类型，子类也需变为类模板。

示例：

```C++
#include <iostream>
using namespace std;

template<class T>
class Base {
    T m;
};

class Son : public Base<int> {};
void test01() { Son c; }

template<class T1, class T2>
class Son2 : public Base<T2> {
public:
    Son2() {
        cout << typeid(T1).name() << endl;
        cout << typeid(T2).name() << endl;
    }
};

void test02() { Son2<int, char> child1; }

int main() {

    test01();
    test02();

    return 0;
}
```

### 类模板成员函数类外实现

> 类模板中成员函数类外实现时，需要加上模板参数列表。

示例：

```C++
#include <iostream>
using namespace std;

#include <string>

template<class T1, class T2>
class Person {
public:
    Person(T1 name, T2 age);
    void showPerson();

public:
    T1 m_Name;
    T2 m_Age;
};

template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age) {
    this->m_Name = name;
    this->m_Age = age;
}

template<class T1, class T2>
void Person<T1, T2>::showPerson() {
    cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}

int main() {

    Person<string, int> p("Tom", 20);
    p.showPerson();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/520be2b7-fcd8-4fb8-9f36-0a6bd19607d3)

### 类模板分文件编写

问题：

-   类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到

解决：

-   解决方式 1：直接包含 `.cpp` 源文件
-   解决方式 2：将声明和实现写到同一个文件中，并更改后缀名为 `.hpp`，`hpp` 是约定的名称，并不是强制。

### 类模板与友元

全局函数类内实现：直接在类内声明友元即可

全局函数类外实现：需要提前让编译器知道全局函数的存在

> 建议全局函数做类内实现，用法简单，而且编译器可以直接识别。

示例：

```C++
#include <iostream>
#include <string>

using namespace std;

template<class T1, class T2>
class Person;

template<class T1, class T2>
void printPerson2(Person<T1, T2> &p) {
    cout << "类外实现 ---- 姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
}

template<class T1, class T2>
class Person {
    friend void printPerson(Person<T1, T2> &p) {
        cout << "姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
    }

    friend void printPerson2<>(Person<T1, T2> &p);

public:
    Person(T1 name, T2 age) {
        this->m_Name = name;
        this->m_Age = age;
    }

private:
    T1 m_Name;
    T2 m_Age;
};

// 1、全局函数在类内实现
void test01() {
    Person<string, int> p("Tom", 20);
    printPerson(p);
}

// 2、全局函数在类外实现
void test02() {
    Person<string, int> p("Jerry", 30);
    printPerson2(p);
}

int main() {

    // test01();
    test02();

    return 0;
}
```



