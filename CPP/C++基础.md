[TOC]

## C++ 关键字

|            |              |                  |             |          |
| ---------- | ------------ | ---------------- | ----------- | -------- |
| asm        | do           | if               | return      | typedef  |
| auto       | double       | inline           | short       | typeid   |
| bool       | dynamic_cast | int              | signed      | typename |
| break      | else         | long             | sizeof      | union    |
| case       | enum         | mutable          | static      | unsigned |
| catch      | explicit     | namespace        | static_cast | using    |
| char       | export       | new              | struct      | virtual  |
| class      | extern       | operator         | switch      | void     |
| const      | false        | private          | template    | volatile |
| const_cast | float        | protected        | this        | wchar_t  |
| continue   | for          | public           | throw       | while    |
| default    | friend       | register         | true        |          |
| delete     | goto         | reinterpret_cast | try         |          |

> 在定义标识符时不要使用这些关键字。

## const 关键字

### 定义常量

定义常量有两种方式，一种是宏定义，另外一种是使用 `const` 关键字，定义格式如下：

```cpp
const 数据类型 常量名 = 常量值;
```

### 指针与 const

const 修饰指针有三种情况

1. `const int * p = &a;`：常量指针，指针指向可以改变，指针指向的值不可以更改变。
2. `int const * p = &a;`：指针常量，指针指向不可以改变，指针指向的值可以更改变。
3. `const int const * p = &a;`

## 数据类型

### sizeof 关键字

`sizeof` 关键字可以统计数据类型所占内存大小。使用方式如下：

```cpp
sizeof(数据类型/变量);
```

### 整型

C++ 中有 4 中整型类型，如下表所示。

|  数据类型   |                           占用空间                           |        取值范围         |
| :---------: | :----------------------------------------------------------: | :---------------------: |
|   `short`   |                            2 字节                            | $-2^{15} \sim 2^{15}-1$ |
|    `int`    |                            4 字节                            | $-2^{31} \sim 2^{31}-1$ |
|   `long`    | Windows 为 4 字节，Linux 为 4 字节（32 位），8 字节（64 位） | $-2^{31} \sim 2^{31}-1$ |
| `long long` |                            8 字节                            | $-2^{63} \sim 2^{63}-1$ |

> 整型占用空间大小：short < int <= long <= long long

### 实型（浮点型）

C++ 中有两种实型：`float` 和 `double`

| 数据类型 | 占用空间 |    有效数字范围     |
| :------: | :------: | :-----------------: |
| `float`  |  4 字节  |    7 位有效数字     |
| `double` |  8 字节  | 15 ～ 16 位有效数字 |

> C++ 中的浮点数字面量默认是 double 类型，想要表示 float 类似的字面量应该这样表示：`3.14f`。
> C++ 中的浮点数还可以使用科学计数法，例如：`3e2` 表示 $3 \times 10 ^ {2}$，`3e-2` 表示 $3 \times 10 ^ {-2}$。

### 字符型

语法：`char ch = 'a';`

> 注意 1：在显示字符型变量时，用单引号将字符括起来，不要用双引号。
> 注意 2：单引号内只能有一个字符，不可以是多个字符。

-   C 和 C++ 中字符型变量只占用 1 个字节。
-   字符型变量并不是把字符本身放到内存中存储，而是将对应的 ASCII 编码放入到存储单元。

示例：

```cpp
int main() {

	char ch = 'a';
	cout << ch << endl;
	cout << sizeof(char) << endl;

	cout << (int)ch << endl;  //查看字符a对应的ASCII码
	ch = 97; //可以直接用ASCII给字符型变量赋值
	cout << ch << endl;

	return 0;
}
```

ASCII 码表格：

| ASCII 值 | 控制字符 | ASCII 值 |  字符   | ASCII 值 | 字符 | ASCII 值 | 字符 |
| :------: | :------: | :------: | :-----: | :------: | :--: | :------: | :--: |
|    0     |   NUT    |    32    | (space) |    64    |  @   |    96    |  、  |
|    1     |   SOH    |    33    |    !    |    65    |  A   |    97    |  a   |
|    2     |   STX    |    34    |    "    |    66    |  B   |    98    |  b   |
|    3     |   ETX    |    35    |    #    |    67    |  C   |    99    |  c   |
|    4     |   EOT    |    36    |    $    |    68    |  D   |   100    |  d   |
|    5     |   ENQ    |    37    |    %    |    69    |  E   |   101    |  e   |
|    6     |   ACK    |    38    |    &    |    70    |  F   |   102    |  f   |
|    7     |   BEL    |    39    |    ,    |    71    |  G   |   103    |  g   |
|    8     |    BS    |    40    |    (    |    72    |  H   |   104    |  h   |
|    9     |    HT    |    41    |    )    |    73    |  I   |   105    |  i   |
|    10    |    LF    |    42    |   \*    |    74    |  J   |   106    |  j   |
|    11    |    VT    |    43    |    +    |    75    |  K   |   107    |  k   |
|    12    |    FF    |    44    |    ,    |    76    |  L   |   108    |  l   |
|    13    |    CR    |    45    |    -    |    77    |  M   |   109    |  m   |
|    14    |    SO    |    46    |    .    |    78    |  N   |   110    |  n   |
|    15    |    SI    |    47    |    /    |    79    |  O   |   111    |  o   |
|    16    |   DLE    |    48    |    0    |    80    |  P   |   112    |  p   |
|    17    |   DCI    |    49    |    1    |    81    |  Q   |   113    |  q   |
|    18    |   DC2    |    50    |    2    |    82    |  R   |   114    |  r   |
|    19    |   DC3    |    51    |    3    |    83    |  S   |   115    |  s   |
|    20    |   DC4    |    52    |    4    |    84    |  T   |   116    |  t   |
|    21    |   NAK    |    53    |    5    |    85    |  U   |   117    |  u   |
|    22    |   SYN    |    54    |    6    |    86    |  V   |   118    |  v   |
|    23    |    TB    |    55    |    7    |    87    |  W   |   119    |  w   |
|    24    |   CAN    |    56    |    8    |    88    |  X   |   120    |  x   |
|    25    |    EM    |    57    |    9    |    89    |  Y   |   121    |  y   |
|    26    |   SUB    |    58    |    :    |    90    |  Z   |   122    |  z   |
|    27    |   ESC    |    59    |    ;    |    91    |  [   |   123    |  {   |
|    28    |    FS    |    60    |    <    |    92    |  /   |   124    |  \|  |
|    29    |    GS    |    61    |    =    |    93    |  ]   |   125    |  }   |
|    30    |    RS    |    62    |    >    |    94    |  ^   |   126    |  \`  |
|    31    |    US    |    63    |    ?    |    95    |  \_  |   127    | DEL  |

ASCII 码大致由以\*两部分组成：

-   ASCII 非打印控制字符：ASCII 表上的数字 0-31 分配给了控制字符，用于控制像打印机等一些外围设备。
-   ASCII 打印字符：数字 32-126 分配给了能在键盘上找到的字符，当查看或打印文档时就会出现。

#### 转义字符

通过转义字符可以表示一些不能显示出来的 ASCII 字符，例如：`'\n'`、`'\\'`，`'\t'`。

| 转义字符 |                   含义                   | ASCII 码值（十进制） |
| :------: | :--------------------------------------: | :------------------: |
|    \a    |                   警报                   |         007          |
|    \b    |    退格（BS） ，将当前位置移到前一列     |         008          |
|    \f    |    换页（FF），将当前位置移到下页开头    |         012          |
|    \n    |   换行（LF），将当前位置移到下一行开头   |         010          |
|    \r    |   回车（CR） ，将当前位置移到本行开头    |         013          |
|    \t    |   水平制表（HT，跳到下一个 TAB 位置）    |         009          |
|    \v    |              垂直制表（VT)               |         011          |
|   \\\\   |        代表一个反斜线字符（`\`）         |         092          |
|    \'    |        代表一个单引号（撇号）字符        |         039          |
|    \"    |            代表一个双引号字符            |         034          |
|    \?    |               代表一个问号               |         063          |
|    \0    |                  数字 0                  |         000          |
|   \ddd   |       8 进制转义字符，d 范围 0\~7        |     3 位 8 进制      |
|   \xhh   | 16 进制转义字符，h 范围 0\~9，a\~f，A\~F |     3 位 16 进制     |

### 字符串型

在 C++中可以使用两种风格的字符串，一种是像 C 语言中那样使用字符数组来表示字符串，还有一种是使用 C++ STL 中的 `string`。

-   C 风格字符串：`char 变量名[] = "字符串值";`
-   C++ 风格字符串：`string 变量名 = "字符串值";`

> 字符串字面量要用双引号括起来。
> C++风格字符串，需要加入头文件 `#include<string>`。

### 布尔类型 bool

C++ 中引入的一种新的数据类型，表示真假，只有两个值：`true` 和 `false`，true 本质是 1，false 本质是 0。在 C++ 中，依然可以使用 0 表示 fasle，非 0 表示 true。

> bool 类型占 1 个字节大小

## 数组

### 一维数组

一维数组定义的三种方式：

1. `数据类型 数组名[数组长度];`
2. `数据类型 数组名[数组长度] = { 值1，值2 ...};`
3. `数据类型 数组名[] = { 值1，值2 ...};`

一维数组名称一方面表示数组在内存中的首地址，另外一方面可以通过一维数组名称统计整个数组在内存中的长度，方式为：`sizeof(arr) / sizeof(arr[0])`。

> 注意：数组名是常量，不可以赋值。
> 将数组名作为函数参数传递时，数组会退化成指向第一个元素的指针，实际上，很多时候我们都可以将数组名视为指向数组中第一个元素的指针。

### 二维数组

二维数组定义的四种方式：

1. `数据类型 数组名[行数][列数];`
2. `数据类型 数组名[行数 [列数] = { {数据1，数据2 } ，{数据3，数据4 } };`
3. `数据类型 数组名[行数][列数] = { 数据1，数据2，数据3，数据4};`
4. ` 数据类型 数组名[][列 ] = { 数据1，数据2，数据3，数据4};`

## 结构体

结构体的定义：`struct 结构体名 { 结构体成员列表 };`

通过结构体创建变量的方式有三种：

-   `struct 结构体名 变量名;`
-   `struct 结构体名 变量名 = { 成员 1 值 ， 成员 2 值...};`
-   定义结构体时顺便创建变量。

## 内存分区模型

C++程序在执行时，将内存大方向划分为 4 个区域：

-   代码区：存放函数体的二进制代码，由操作系统进行管理的。
-   全局区：存放全局变量和静态变量以及常量。
-   栈区：由编译器自动分配释放, 存放函数的参数值,局部变量等。
-   堆区：由程序员分配和释放,若程序员不释放,程序结束时由操作系统回收（`new` 出来的东西都在堆区）。

> 不同区域存放的数据，赋予不同的生命周期, 给我们更大的灵活编程。

### 程序运行前

在程序编译后，生成了 exe 可执行程序，未执行该程序前分为两个区域：

-   代码区：
    -   存放 CPU 执行的机器指令。
    -   代码区是共享的，共享的目的是对于频繁被执行的程序，只需要在内存中有一份代码即可。
    -   代码区是只读的，使其只读的原因是防止程序意外地修改了它的指令。
-   全局区：
    -   全局变量和静态变量存放在此。
    -   全局区还包含了常量区, 字符串常量和其他常量也存放在此。
    -   该区域的数据在程序结束后由操作系统释放。

示例：

```cpp
//全局变量
int g_a = 10;
int g_b = 10;

//全局常量
const int c_g_a = 10;
const int c_g_b = 10;

int main() {

	//局部变量
	int a = 10;
	int b = 10;

	//打印地址
	cout << "局部变量a地址为： " << (int)&a << endl;
	cout << "局部变量b地址为： " << (int)&b << endl;

	cout << "全局变量g_a地址为： " <<  (int)&g_a << endl;
	cout << "全局变量g_b地址为： " <<  (int)&g_b << endl;

	//静态变量
	static int s_a = 10;
	static int s_b = 10;

	cout << "静态变量s_a地址为： " << (int)&s_a << endl;
	cout << "静态变量s_b地址为： " << (int)&s_b << endl;

	cout << "字符串常量地址为： " << (int)&"hello world" << endl;
	cout << "字符串常量地址为： " << (int)&"hello world1" << endl;

	cout << "全局常量c_g_a地址为： " << (int)&c_g_a << endl;
	cout << "全局常量c_g_b地址为： " << (int)&c_g_b << endl;

	const int c_l_a = 10;
	const int c_l_b = 10;
	cout << "局部常量c_l_a地址为： " << (int)&c_l_a << endl;
	cout << "局部常量c_l_b地址为： " << (int)&c_l_b << endl;

	return 0;
}
```

打印结果：

![1545017602518](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/1545017602518.png)

### 程序运行后

-   栈区
    -   由编译器自动分配释放，存放函数的参数值，局部变量。
    -   等注意事项：不要返回局部变量的地址，栈区开辟的数据由编译器自动释放。
-   堆区：
    -   由程序员分配释放，若程序员不释放，程序结束时由操作系统回收。
    -   在 C++ 中主要利用 new 在堆区开辟内存。

### new 操作符

C++中利用 new 操作符在堆区开辟数据。

堆区开辟的数据，由程序员手动开辟，手动释放，释放利用操作符 delete。

语法：`new 数据类型`。

利用 new 创建的数据，会返回该数据对应的类型的指针

示例 1：

```cpp
int* func()
{
	int* a = new int(10);
	return a;
}

int main() {

	int *p = func();

	cout << *p << endl;
	cout << *p << endl;

	//利用delete释放堆区数据
	delete p;

	//cout << *p << endl; //报错，释放的空间不可访问

	system("pause");

	return 0;
}
```

示例 2：开辟数组

```cpp
//堆区开辟数组
int main() {

	int* arr = new int[10];

	for (int i = 0; i < 10; i++)
	{
		arr[i] = i + 100;
	}

	for (int i = 0; i < 10; i++)
	{
		cout << arr[i] << endl;
	}
	//释放数组 delete 后加 []
	delete[] arr;

	system("pause");

	return 0;
}

```

## 引用

### 2.1 引用的基本使用

语法：`数据类型 &别名 = 原名;`

> 引用必须初始化。
>
> 引用在初始化后，指向不可改变。
>
> 引用的本质在 C++ 内部实现是一个指针常量。

## 函数

### 指针与函数

利用指针作函数参数，可以修改实参的值。

示例：

```cpp
//值传递
void swap1(int a ,int b)
{
	int temp = a;
	a = b;
	b = temp;
}

//地址传递
void swap2(int * p1, int *p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}

int main() {

	int a = 10;
	int b = 20;
	swap1(a, b); // 值传递不会改变实参

	swap2(&a, &b); //地址传递会改变实参

	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	system("pause");
	return 0;
}
```

> 总结：如果不想修改实参，就用值传递，如果想修改实参，就用地址传递。

### 引用与函数

引用做函数参数：函数传参时，可以利用引用的技术让形参修饰实参。

引用做函数返回值：引用是可以作为函数的返回值。

> 通过引用参数产生的效果同按地址传递是一样的。引用的语法更清楚简单。
>
> 不要返回局部变量引用。
>
> 返回引用的函数可以作为左值。
>
> 函数声明引用参数时，可以加上 `const` 关键字，这样在函数内部只有对该变量的读权限，没有写权限。

### 函数默认参数

在 C++ 中，函数的形参列表中的形参是可以有默认值的。

语法：` 返回值类型 函数名(参数= 默认值) {}`

1. 如果某个位置参数有默认值，那么从这个位置往后，从左向右，必须都要有默认值。
2. 如果函数声明有默认值，函数实现的时候就不能有默认参数。

### 函数占位参数

C++ 中函数的形参列表里可以有占位参数，用来做占位，调用函数时必须填补该位置。

语法：`返回值类型 函数名(数据类型 ){}`

示例：

```cpp
// 函数占位参数 ，占位参数也可以有默认参数
void func(int a, int) {
	cout << "this is func" << endl;
}

int main() {

	func(10,10); //占位参数必须填补

	system("pause");
	return 0;
}
```

### 函数重载

函数名可以相同，提高复用性。

函数重载满足条件：

-   同一个作用域下；
-   函数名称相同；
-   函数参数类型不同或者个数不同或者顺序不同。

> 函数的返回值不可以作为函数重载的条件。

#### 函数重载注意事项

-   引用作为重载条件，字面量会优先调用参数带 `const` 关键字的函数，变量会优先调用参数无 `const` 关键字的函数。
-   函数重载碰到函数默认参数时会参数歧义，请避免这种用法。

## 类和对象

C++ 面向对象的三大特性为：封装、继承、多态。

声明一个类的语法：`class 类名{ 访问权限： 属性 / 行为 };`

类在设计时，可以把属性和行为放在不同的权限下，加以控制。

访问权限有三种：

1. `public`：公共权限。
2. `protected`：保护权限。
3. `private`：私有权限。

### struct 和 class 区别

在 C++ 中 struct 和 class 唯一的区别就在于：默认的访问权限不同。

区别：

-   struct 默认权限为公共；
-   class 默认权限为私有。

### 对象的初始化和清理

#### 构造函数和析构函数

对象的初始化和清理工作是编译器强制要我们做的事情，因此如果**我们不提供构造函数和析构函数，编译器会提供**。编译器提供的构造函数和析构函数是空实现。

-   构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数由编译器自动调用，无须手动调用。
-   析构函数：主要作用在于对象**销毁前**系统自动调用，执行一些清理工作。

构造函数语法：`类名(){}`

1. 构造函数，没有返回值也不写 void。
2. 函数名称与类名相同。
3. 构造函数可以有参数，因此可以发生重载。
4. 程序在调用对象时候会自动调用构造，无须手动调用,而且只会调用一次。

析构函数语法：`~类名(){}`

1. 析构函数，没有返回值也不写 void
2. 函数名称与类名相同，在名称前加上符号 ~
3. 析构函数不可以有参数，因此不可以发生重载。
4. 程序在对象销毁前会自动调用析构，无须手动调用,而且只会调用一次。

#### 构造函数的分类及调用

两种分类方式：

按参数分为： 有参构造和无参构造

按类型分为： 普通构造和拷贝构造

三种调用方式：

括号法

显示法

隐式转换法

**示例：**

```C++
//1、构造函数分类
// 按照参数分类分为 有参和无参构造   无参又称为默认构造函数
// 按照类型分类分为 普通构造和拷贝构造

class Person {
public:
	//无参（默认）构造函数
	Person() {
		cout << "无参构造函数!" << endl;
	}
	//有参构造函数
	Person(int a) {
		age = a;
		cout << "有参构造函数!" << endl;
	}
	//拷贝构造函数
	Person(const Person& p) {
		age = p.age;
		cout << "拷贝构造函数!" << endl;
	}
	//析构函数
	~Person() {
		cout << "析构函数!" << endl;
	}
public:
	int age;
};

//2、构造函数的调用
//调用无参构造函数
void test01() {
	Person p; //调用无参构造函数
}

//调用有参的构造函数
void test02() {

	//2.1  括号法，常用
	Person p1(10);
	//注意1：调用无参构造函数不能加括号，如果加了编译器认为这是一个函数声明
	//Person p2();

	//2.2 显式法
	Person p2 = Person(10);
	Person p3 = Person(p2);
	//Person(10)单独写就是匿名对象  当前行结束之后，马上析构

	//2.3 隐式转换法
	Person p4 = 10; // Person p4 = Person(10);
	Person p5 = p4; // Person p5 = Person(p4);

	//注意2：不能利用 拷贝构造函数 初始化匿名对象 编译器认为是对象声明
	//Person p5(p4);
}

int main() {

	test01();
	//test02();

	system("pause");

	return 0;
}
```

#### 4.2.3 拷贝构造函数调用时机

C++中拷贝构造函数调用时机通常有三种情况

-   使用一个已经创建完毕的对象来初始化一个新对象
-   值传递的方式给函数参数传值
-   以值方式返回局部对象

**示例：**

```C++
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
	Person(const Person& p) {
		cout << "拷贝构造函数!" << endl;
		mAge = p.mAge;
	}
	//析构函数在释放内存之前调用
	~Person() {
		cout << "析构函数!" << endl;
	}
public:
	int mAge;
};

//1. 使用一个已经创建完毕的对象来初始化一个新对象
void test01() {

	Person man(100); //p对象已经创建完毕
	Person newman(man); //调用拷贝构造函数
	Person newman2 = man; //拷贝构造

	//Person newman3;
	//newman3 = man; //不是调用拷贝构造函数，赋值操作
}

//2. 值传递的方式给函数参数传值
//相当于Person p1 = p;
void doWork(Person p1) {}
void test02() {
	Person p; //无参构造函数
	doWork(p);
}

//3. 以值方式返回局部对象
Person doWork2()
{
	Person p1;
	cout << (int *)&p1 << endl;
	return p1;
}

void test03()
{
	Person p = doWork2();
	cout << (int *)&p << endl;
}


int main() {

	//test01();
	//test02();
	test03();

	system("pause");

	return 0;
}
```

#### 4.2.4 构造函数调用规则

默认情况下，c++编译器至少给一个类添加 3 个函数

1．默认构造函数(无参，函数体为空)

2．默认析构函数(无参，函数体为空)

3．默认拷贝构造函数，对属性进行值拷贝

构造函数调用规则如下：

-   如果用户定义有参构造函数，c++不在提供默认无参构造，但是会提供默认拷贝构造

-   如果用户定义拷贝构造函数，c++不会再提供其他构造函数

示例：

```C++
class Person {
public:
	//无参（默认）构造函数
	Person() {
		cout << "无参构造函数!" << endl;
	}
	//有参构造函数
	Person(int a) {
		age = a;
		cout << "有参构造函数!" << endl;
	}
	//拷贝构造函数
	Person(const Person& p) {
		age = p.age;
		cout << "拷贝构造函数!" << endl;
	}
	//析构函数
	~Person() {
		cout << "析构函数!" << endl;
	}
public:
	int age;
};

void test01()
{
	Person p1(18);
	//如果不写拷贝构造，编译器会自动添加拷贝构造，并且做浅拷贝操作
	Person p2(p1);

	cout << "p2的年龄为： " << p2.age << endl;
}

void test02()
{
	//如果用户提供有参构造，编译器不会提供默认构造，会提供拷贝构造
	Person p1; //此时如果用户自己没有提供默认构造，会出错
	Person p2(10); //用户提供的有参
	Person p3(p2); //此时如果用户没有提供拷贝构造，编译器会提供

	//如果用户提供拷贝构造，编译器不会提供其他构造函数
	Person p4; //此时如果用户自己没有提供默认构造，会出错
	Person p5(10); //此时如果用户自己没有提供有参，会出错
	Person p6(p5); //用户自己提供拷贝构造
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.2.5 深拷贝与浅拷贝

深浅拷贝是面试经典问题，也是常见的一个坑

浅拷贝：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作

**示例：**

```C++
class Person {
public:
	//无参（默认）构造函数
	Person() {
		cout << "无参构造函数!" << endl;
	}
	//有参构造函数
	Person(int age ,int height) {

		cout << "有参构造函数!" << endl;

		m_age = age;
		m_height = new int(height);

	}
	//拷贝构造函数
	Person(const Person& p) {
		cout << "拷贝构造函数!" << endl;
		//如果不利用深拷贝在堆区创建新内存，会导致浅拷贝带来的重复释放堆区问题
		m_age = p.m_age;
		m_height = new int(*p.m_height);

	}

	//析构函数
	~Person() {
		cout << "析构函数!" << endl;
		if (m_height != NULL)
		{
			delete m_height;
		}
	}
public:
	int m_age;
	int* m_height;
};

void test01()
{
	Person p1(18, 180);

	Person p2(p1);

	cout << "p1的年龄： " << p1.m_age << " 身高： " << *p1.m_height << endl;

	cout << "p2的年龄： " << p2.m_age << " 身高： " << *p2.m_height << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

> 总结：如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题

#### 4.2.6 初始化列表

**作用：**

C++提供了初始化列表语法，用来初始化属性

**语法：**`构造函数()：属性1(值1),属性2（值2）... {}`

**示例：**

```C++
class Person {
public:

	////传统方式初始化
	//Person(int a, int b, int c) {
	//	m_A = a;
	//	m_B = b;
	//	m_C = c;
	//}

	//初始化列表方式初始化
	Person(int a, int b, int c) :m_A(a), m_B(b), m_C(c) {}
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


	system("pause");

	return 0;
}
```

#### 4.2.7 类对象作为类成员

C++类中的成员可以是另一个类的对象，我们称该成员为 对象成员

例如：

```C++
class A {}
class B
{
    A a；
}
```

B 类中有对象 A 作为成员，A 为对象成员

那么当创建 B 对象时，A 与 B 的构造和析构的顺序是谁先谁后？

**示例：**

```C++
class Phone
{
public:
	Phone(string name)
	{
		m_PhoneName = name;
		cout << "Phone构造" << endl;
	}

	~Phone()
	{
		cout << "Phone析构" << endl;
	}

	string m_PhoneName;

};


class Person
{
public:

	//初始化列表可以告诉编译器调用哪一个构造函数
	Person(string name, string pName) :m_Name(name), m_Phone(pName)
	{
		cout << "Person构造" << endl;
	}

	~Person()
	{
		cout << "Person析构" << endl;
	}

	void playGame()
	{
		cout << m_Name << " 使用" << m_Phone.m_PhoneName << " 牌手机! " << endl;
	}

	string m_Name;
	Phone m_Phone;

};
void test01()
{
	//当类中成员是其他类对象时，我们称该成员为 对象成员
	//构造的顺序是 ：先调用对象成员的构造，再调用本类构造
	//析构顺序与构造相反
	Person p("张三" , "苹果X");
	p.playGame();

}


int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.2.8 静态成员

静态成员就是在成员变量和成员函数前加上关键字 static，称为静态成员

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
class Person
{

public:

	static int m_A; //静态成员变量

	//静态成员变量特点：
	//1 在编译阶段分配内存
	//2 类内声明，类外初始化
	//3 所有对象共享同一份数据

private:
	static int m_B; //静态成员变量也是有访问权限的
};
int Person::m_A = 10;
int Person::m_B = 10;

void test01()
{
	//静态成员变量两种访问方式

	//1、通过对象
	Person p1;
	p1.m_A = 100;
	cout << "p1.m_A = " << p1.m_A << endl;

	Person p2;
	p2.m_A = 200;
	cout << "p1.m_A = " << p1.m_A << endl; //共享同一份数据
	cout << "p2.m_A = " << p2.m_A << endl;

	//2、通过类名
	cout << "m_A = " << Person::m_A << endl;


	//cout << "m_B = " << Person::m_B << endl; //私有权限访问不到
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**示例 2：**静态成员函数

```C++
class Person
{

public:

	//静态成员函数特点：
	//1 程序共享一个函数
	//2 静态成员函数只能访问静态成员变量

	static void func()
	{
		cout << "func调用" << endl;
		m_A = 100;
		//m_B = 100; //错误，不可以访问非静态成员变量
	}

	static int m_A; //静态成员变量
	int m_B; //
private:

	//静态成员函数也是有访问权限的
	static void func2()
	{
		cout << "func2调用" << endl;
	}
};
int Person::m_A = 10;


void test01()
{
	//静态成员变量两种访问方式

	//1、通过对象
	Person p1;
	p1.func();

	//2、通过类名
	Person::func();


	//Person::func2(); //私有权限访问不到
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.3 C++对象模型和 this 指针

#### 4.3.1 成员变量和成员函数分开存储

在 C++中，类内的成员变量和成员函数分开存储

只有非静态成员变量才属于类的对象上

```C++
class Person {
public:
	Person() {
		mA = 0;
	}
	//非静态成员变量占对象空间
	int mA;
	//静态成员变量不占对象空间
	static int mB;
	//函数也不占对象空间，所有函数共享一个函数实例
	void func() {
		cout << "mA:" << this->mA << endl;
	}
	//静态成员函数也不占对象空间
	static void sfunc() {
	}
};

int main() {

	cout << sizeof(Person) << endl;

	system("pause");

	return 0;
}
```

#### 4.3.2 this 指针概念

通过 4.3.1 我们知道在 C++中成员变量和成员函数是分开存储的

每一个非静态成员函数只会诞生一份函数实例，也就是说多个同类型的对象会共用一块代码

那么问题是：这一块代码是如何区分那个对象调用自己的呢？

c++通过提供特殊的对象指针，this 指针，解决上述问题。**this 指针指向被调用的成员函数所属的对象**

this 指针是隐含每一个非静态成员函数内的一种指针

this 指针不需要定义，直接使用即可

this 指针的用途：

-   当形参和成员变量同名时，可用 this 指针来区分
-   在类的非静态成员函数中返回对象本身，可使用 return \*this

```C++
class Person
{
public:

	Person(int age)
	{
		//1、当形参和成员变量同名时，可用this指针来区分
		this->age = age;
	}

	Person& PersonAddPerson(Person p)
	{
		this->age += p.age;
		//返回对象本身
		return *this;
	}

	int age;
};

void test01()
{
	Person p1(10);
	cout << "p1.age = " << p1.age << endl;

	Person p2(10);
	p2.PersonAddPerson(p1).PersonAddPerson(p1).PersonAddPerson(p1);
	cout << "p2.age = " << p2.age << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.3.3 空指针访问成员函数

C++中空指针也是可以调用成员函数的，但是也要注意有没有用到 this 指针

如果用到 this 指针，需要加以判断保证代码的健壮性

**示例：**

```C++
//空指针访问成员函数
class Person {
public:

	void ShowClassName() {
		cout << "我是Person类!" << endl;
	}

	void ShowPerson() {
		if (this == NULL) {
			return;
		}
		cout << mAge << endl;
	}

public:
	int mAge;
};

void test01()
{
	Person * p = NULL;
	p->ShowClassName(); //空指针，可以调用成员函数
	p->ShowPerson();  //但是如果成员函数中用到了this指针，就不可以了
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.3.4 const 修饰成员函数

**常函数：**

-   成员函数后加 const 后我们称为这个函数为**常函数**
-   常函数内不可以修改成员属性
-   成员属性声明时加关键字 mutable 后，在常函数中依然可以修改

**常对象：**

-   声明对象前加 const 称该对象为常对象
-   常对象只能调用常函数

**示例：**

```C++
class Person {
public:
	Person() {
		m_A = 0;
		m_B = 0;
	}

	//this指针的本质是一个指针常量，指针的指向不可修改
	//如果想让指针指向的值也不可以修改，需要声明常函数
	void ShowPerson() const {
		//const Type* const pointer;
		//this = NULL; //不能修改指针的指向 Person* const this;
		//this->mA = 100; //但是this指针指向的对象的数据是可以修改的

		//const修饰成员函数，表示指针指向的内存空间的数据不能修改，除了mutable修饰的变量
		this->m_B = 100;
	}

	void MyFunc() const {
		//mA = 10000;
	}

public:
	int m_A;
	mutable int m_B; //可修改 可变的
};


//const修饰对象  常对象
void test01() {

	const Person person; //常量对象
	cout << person.m_A << endl;
	//person.mA = 100; //常对象不能修改成员变量的值,但是可以访问
	person.m_B = 100; //但是常对象可以修改mutable修饰成员变量

	//常对象访问成员函数
	person.MyFunc(); //常对象不能调用const的函数

}

int main() {

	test01();

	system("pause");

	return 0;
}
```

### 4.4 友元

生活中你的家有客厅(Public)，有你的卧室(Private)

客厅所有来的客人都可以进去，但是你的卧室是私有的，也就是说只有你能进去

但是呢，你也可以允许你的好闺蜜好基友进去。

在程序里，有些私有属性 也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术

友元的目的就是让一个函数或者类 访问另一个类中私有成员

友元的关键字为 ==friend==

友元的三种实现

-   全局函数做友元
-   类做友元
-   成员函数做友元

#### 4.4.1 全局函数做友元

```C++
class Building
{
	//告诉编译器 goodGay全局函数 是 Building类的好朋友，可以访问类中的私有内容
	friend void goodGay(Building * building);

public:

	Building()
	{
		this->m_SittingRoom = "客厅";
		this->m_BedRoom = "卧室";
	}


public:
	string m_SittingRoom; //客厅

private:
	string m_BedRoom; //卧室
};


void goodGay(Building * building)
{
	cout << "好基友正在访问： " << building->m_SittingRoom << endl;
	cout << "好基友正在访问： " << building->m_BedRoom << endl;
}


void test01()
{
	Building b;
	goodGay(&b);
}

int main(){

	test01();

	system("pause");
	return 0;
}
```

#### 4.4.2 类做友元

```C++
class Building;
class goodGay
{
public:

	goodGay();
	void visit();

private:
	Building *building;
};


class Building
{
	//告诉编译器 goodGay类是Building类的好朋友，可以访问到Building类中私有内容
	friend class goodGay;

public:
	Building();

public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom;//卧室
};

Building::Building()
{
	this->m_SittingRoom = "客厅";
	this->m_BedRoom = "卧室";
}

goodGay::goodGay()
{
	building = new Building;
}

void goodGay::visit()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void test01()
{
	goodGay gg;
	gg.visit();

}

int main(){

	test01();

	system("pause");
	return 0;
}
```

#### 4.4.3 成员函数做友元

```C++

class Building;
class goodGay
{
public:

	goodGay();
	void visit(); //只让visit函数作为Building的好朋友，可以发访问Building中私有内容
	void visit2();

private:
	Building *building;
};


class Building
{
	//告诉编译器  goodGay类中的visit成员函数 是Building好朋友，可以访问私有内容
	friend void goodGay::visit();

public:
	Building();

public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom;//卧室
};

Building::Building()
{
	this->m_SittingRoom = "客厅";
	this->m_BedRoom = "卧室";
}

goodGay::goodGay()
{
	building = new Building;
}

void goodGay::visit()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void goodGay::visit2()
{
	cout << "好基友正在访问" << building->m_SittingRoom << endl;
	//cout << "好基友正在访问" << building->m_BedRoom << endl;
}

void test01()
{
	goodGay  gg;
	gg.visit();

}

int main(){

	test01();

	system("pause");
	return 0;
}
```



### 4.6 继承

**继承是面向对象三大特性之一**

有些类与类之间存在特殊的关系，例如下图中：

![1544861202252](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/1544861202252.png)

我们发现，定义这些类时，下级别的成员除了拥有上一级的共性，还有自己的特性。

这个时候我们就可以考虑利用继承的技术，减少重复代码

#### 4.6.1 继承的基本语法

例如我们看到很多网站中，都有公共的头部，公共的底部，甚至公共的左侧列表，只有中心内容不同

接下来我们分别利用普通写法和继承的写法来实现网页中的内容，看一下继承存在的意义以及好处

**普通实现：**

```C++
//Java页面
class Java
{
public:
	void header()
	{
		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
	}
	void footer()
	{
		cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
	}
	void left()
	{
		cout << "Java,Python,C++...(公共分类列表)" << endl;
	}
	void content()
	{
		cout << "JAVA学科视频" << endl;
	}
};
//Python页面
class Python
{
public:
	void header()
	{
		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
	}
	void footer()
	{
		cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
	}
	void left()
	{
		cout << "Java,Python,C++...(公共分类列表)" << endl;
	}
	void content()
	{
		cout << "Python学科视频" << endl;
	}
};
//C++页面
class CPP
{
public:
	void header()
	{
		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
	}
	void footer()
	{
		cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
	}
	void left()
	{
		cout << "Java,Python,C++...(公共分类列表)" << endl;
	}
	void content()
	{
		cout << "C++学科视频" << endl;
	}
};

void test01()
{
	//Java页面
	cout << "Java下载视频页面如下： " << endl;
	Java ja;
	ja.header();
	ja.footer();
	ja.left();
	ja.content();
	cout << "--------------------" << endl;

	//Python页面
	cout << "Python下载视频页面如下： " << endl;
	Python py;
	py.header();
	py.footer();
	py.left();
	py.content();
	cout << "--------------------" << endl;

	//C++页面
	cout << "C++下载视频页面如下： " << endl;
	CPP cp;
	cp.header();
	cp.footer();
	cp.left();
	cp.content();

}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**继承实现：**

```C++
//公共页面
class BasePage
{
public:
	void header()
	{
		cout << "首页、公开课、登录、注册...（公共头部）" << endl;
	}

	void footer()
	{
		cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
	}
	void left()
	{
		cout << "Java,Python,C++...(公共分类列表)" << endl;
	}

};

//Java页面
class Java : public BasePage
{
public:
	void content()
	{
		cout << "JAVA学科视频" << endl;
	}
};
//Python页面
class Python : public BasePage
{
public:
	void content()
	{
		cout << "Python学科视频" << endl;
	}
};
//C++页面
class CPP : public BasePage
{
public:
	void content()
	{
		cout << "C++学科视频" << endl;
	}
};

void test01()
{
	//Java页面
	cout << "Java下载视频页面如下： " << endl;
	Java ja;
	ja.header();
	ja.footer();
	ja.left();
	ja.content();
	cout << "--------------------" << endl;

	//Python页面
	cout << "Python下载视频页面如下： " << endl;
	Python py;
	py.header();
	py.footer();
	py.left();
	py.content();
	cout << "--------------------" << endl;

	//C++页面
	cout << "C++下载视频页面如下： " << endl;
	CPP cp;
	cp.header();
	cp.footer();
	cp.left();
	cp.content();


}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**

继承的好处：==可以减少重复的代码==

class A : public B;

A 类称为子类 或 派生类

B 类称为父类 或 基类

**派生类中的成员，包含两大部分**：

一类是从基类继承过来的，一类是自己增加的成员。

从基类继承过过来的表现其共性，而新增的成员体现了其个性。

#### 4.6.2 继承方式

继承的语法：`class 子类 : 继承方式 父类`

**继承方式一共有三种：**

-   公共继承
-   保护继承
-   私有继承

![img](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/clip_image002.png)

**示例：**

```C++
class Base1
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};

//公共继承
class Son1 :public Base1
{
public:
	void func()
	{
		m_A; //可访问 public权限
		m_B; //可访问 protected权限
		//m_C; //不可访问
	}
};

void myClass()
{
	Son1 s1;
	s1.m_A; //其他类只能访问到公共权限
}

//保护继承
class Base2
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son2:protected Base2
{
public:
	void func()
	{
		m_A; //可访问 protected权限
		m_B; //可访问 protected权限
		//m_C; //不可访问
	}
};
void myClass2()
{
	Son2 s;
	//s.m_A; //不可访问
}

//私有继承
class Base3
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};
class Son3:private Base3
{
public:
	void func()
	{
		m_A; //可访问 private权限
		m_B; //可访问 private权限
		//m_C; //不可访问
	}
};
class GrandSon3 :public Son3
{
public:
	void func()
	{
		//Son3是私有继承，所以继承Son3的属性在GrandSon3中都无法访问到
		//m_A;
		//m_B;
		//m_C;
	}
};
```

#### 4.6.3 继承中的对象模型

**问题：**从父类继承过来的成员，哪些属于子类对象中？

**示例：**

```C++
class Base
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C; //私有成员只是被隐藏了，但是还是会继承下去
};

//公共继承
class Son :public Base
{
public:
	int m_D;
};

void test01()
{
	cout << "sizeof Son = " << sizeof(Son) << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

利用工具查看：

![1545881904150](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/1545881904150.png)

打开工具窗口后，定位到当前 CPP 文件的盘符

然后输入： cl /d1 reportSingleClassLayout 查看的类名 所属文件名

效果如下图：

![1545882158050](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/1545882158050.png)

> 结论： 父类中私有成员也是被子类继承下去了，只是由编译器给隐藏后访问不到

#### 4.6.4 继承中构造和析构顺序

子类继承父类后，当创建子类对象，也会调用父类的构造函数

问题：父类和子类的构造和析构顺序是谁先谁后？

**示例：**

```C++
class Base
{
public:
	Base()
	{
		cout << "Base构造函数!" << endl;
	}
	~Base()
	{
		cout << "Base析构函数!" << endl;
	}
};

class Son : public Base
{
public:
	Son()
	{
		cout << "Son构造函数!" << endl;
	}
	~Son()
	{
		cout << "Son析构函数!" << endl;
	}

};


void test01()
{
	//继承中 先调用父类构造函数，再调用子类构造函数，析构顺序与构造相反
	Son s;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

> 总结：继承中 先调用父类构造函数，再调用子类构造函数，析构顺序与构造相反

#### 4.6.5 继承同名成员处理方式

问题：当子类与父类出现同名的成员，如何通过子类对象，访问到子类或父类中同名的数据呢？

-   访问子类同名成员 直接访问即可
-   访问父类同名成员 需要加作用域

**示例：**

```C++
class Base {
public:
	Base()
	{
		m_A = 100;
	}

	void func()
	{
		cout << "Base - func()调用" << endl;
	}

	void func(int a)
	{
		cout << "Base - func(int a)调用" << endl;
	}

public:
	int m_A;
};


class Son : public Base {
public:
	Son()
	{
		m_A = 200;
	}

	//当子类与父类拥有同名的成员函数，子类会隐藏父类中所有版本的同名成员函数
	//如果想访问父类中被隐藏的同名成员函数，需要加父类的作用域
	void func()
	{
		cout << "Son - func()调用" << endl;
	}
public:
	int m_A;
};

void test01()
{
	Son s;

	cout << "Son下的m_A = " << s.m_A << endl;
	cout << "Base下的m_A = " << s.Base::m_A << endl;

	s.func();
	s.Base::func();
	s.Base::func(10);

}
int main() {

	test01();

	system("pause");
	return EXIT_SUCCESS;
}
```

总结：

1. 子类对象可以直接访问到子类中同名成员
2. 子类对象加作用域可以访问到父类同名成员
3. 当子类与父类拥有同名的成员函数，子类会隐藏父类中同名成员函数，加作用域可以访问到父类中同名函数

#### 4.6.6 继承同名静态成员处理方式

问题：继承中同名的静态成员在子类对象上如何进行访问？

静态成员和非静态成员出现同名，处理方式一致

-   访问子类同名成员 直接访问即可
-   访问父类同名成员 需要加作用域

**示例：**

```C++
class Base {
public:
	static void func()
	{
		cout << "Base - static void func()" << endl;
	}
	static void func(int a)
	{
		cout << "Base - static void func(int a)" << endl;
	}

	static int m_A;
};

int Base::m_A = 100;

class Son : public Base {
public:
	static void func()
	{
		cout << "Son - static void func()" << endl;
	}
	static int m_A;
};

int Son::m_A = 200;

//同名成员属性
void test01()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	cout << "Son  下 m_A = " << s.m_A << endl;
	cout << "Base 下 m_A = " << s.Base::m_A << endl;

	//通过类名访问
	cout << "通过类名访问： " << endl;
	cout << "Son  下 m_A = " << Son::m_A << endl;
	cout << "Base 下 m_A = " << Son::Base::m_A << endl;
}

//同名成员函数
void test02()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	s.func();
	s.Base::func();

	cout << "通过类名访问： " << endl;
	Son::func();
	Son::Base::func();
	//出现同名，子类会隐藏掉父类中所有同名成员函数，需要加作作用域访问
	Son::Base::func(100);
}
int main() {

	//test01();
	test02();

	system("pause");

	return 0;
}
```

> 总结：同名静态成员处理方式和非静态处理方式一样，只不过有两种访问的方式（通过对象 和 通过类名）

#### 4.6.7 多继承语法

C++允许**一个类继承多个类**

语法：` class 子类 ：继承方式 父类1 ， 继承方式 父类2...`

多继承可能会引发父类中有同名成员出现，需要加作用域区分

**C++实际开发中不建议用多继承**

**示例：**

```C++
class Base1 {
public:
	Base1()
	{
		m_A = 100;
	}
public:
	int m_A;
};

class Base2 {
public:
	Base2()
	{
		m_A = 200;  //开始是m_B 不会出问题，但是改为mA就会出现不明确
	}
public:
	int m_A;
};

//语法：class 子类：继承方式 父类1 ，继承方式 父类2
class Son : public Base2, public Base1
{
public:
	Son()
	{
		m_C = 300;
		m_D = 400;
	}
public:
	int m_C;
	int m_D;
};


//多继承容易产生成员同名的情况
//通过使用类名作用域可以区分调用哪一个基类的成员
void test01()
{
	Son s;
	cout << "sizeof Son = " << sizeof(s) << endl;
	cout << s.Base1::m_A << endl;
	cout << s.Base2::m_A << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

> 总结： 多继承中如果父类中出现了同名情况，子类使用时候要加作用域

#### 4.6.8 菱形继承

**菱形继承概念：**

两个派生类继承同一个基类

又有某个类同时继承者两个派生类

这种继承被称为菱形继承，或者钻石继承

**典型的菱形继承案例：**

![IMG_256](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/clip_image002.jpg)

**菱形继承问题：**

1.                                                  羊继承了动物的数据，驼同样继承了动物的数据，当草泥马使用数据时，就会产生二义性。

2.  草泥马继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以。

**示例：**

```C++
class Animal
{
public:
	int m_Age;
};

//继承前加virtual关键字后，变为虚继承
//此时公共的父类Animal称为虚基类
class Sheep : virtual public Animal {};
class Tuo   : virtual public Animal {};
class SheepTuo : public Sheep, public Tuo {};

void test01()
{
	SheepTuo st;
	st.Sheep::m_Age = 100;
	st.Tuo::m_Age = 200;

	cout << "st.Sheep::m_Age = " << st.Sheep::m_Age << endl;
	cout << "st.Tuo::m_Age = " <<  st.Tuo::m_Age << endl;
	cout << "st.m_Age = " << st.m_Age << endl;
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：

-   菱形继承带来的主要问题是子类继承两份相同的数据，导致资源浪费以及毫无意义
-   利用虚继承可以解决菱形继承问题

### 4.7 多态

#### 4.7.1 多态的基本概念

**多态是 C++面向对象三大特性之一**

多态分为两类

-   静态多态: 函数重载 和 运算符重载属于静态多态，复用函数名
-   动态多态: 派生类和虚函数实现运行时多态

静态多态和动态多态区别：

-   静态多态的函数地址早绑定 - 编译阶段确定函数地址
-   动态多态的函数地址晚绑定 - 运行阶段确定函数地址

下面通过案例进行讲解多态

```C++
class Animal
{
public:
	//Speak函数就是虚函数
	//函数前面加上virtual关键字，变成虚函数，那么编译器在编译的时候就不能确定函数调用了。
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};

class Cat :public Animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};

class Dog :public Animal
{
public:

	void speak()
	{
		cout << "小狗在说话" << endl;
	}

};
//我们希望传入什么对象，那么就调用什么对象的函数
//如果函数地址在编译阶段就能确定，那么静态联编
//如果函数地址在运行阶段才能确定，就是动态联编

void DoSpeak(Animal & animal)
{
	animal.speak();
}
//
//多态满足条件：
//1、有继承关系
//2、子类重写父类中的虚函数
//多态使用：
//父类指针或引用指向子类对象

void test01()
{
	Cat cat;
	DoSpeak(cat);


	Dog dog;
	DoSpeak(dog);
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：

多态满足条件

-   有继承关系
-   子类重写父类中的虚函数

多态使用条件

-   父类指针或引用指向子类对象

重写：函数返回值类型 函数名 参数列表 完全一致称为重写

#### 4.7.2 多态案例一-计算器类

案例描述：

分别利用普通写法和多态技术，设计实现两个操作数进行运算的计算器类

多态的优点：

-   代码组织结构清晰
-   可读性强
-   利于前期和后期的扩展以及维护

**示例：**

```C++
//普通实现
class Calculator {
public:
	int getResult(string oper)
	{
		if (oper == "+") {
			return m_Num1 + m_Num2;
		}
		else if (oper == "-") {
			return m_Num1 - m_Num2;
		}
		else if (oper == "*") {
			return m_Num1 * m_Num2;
		}
		//如果要提供新的运算，需要修改源码
	}
public:
	int m_Num1;
	int m_Num2;
};

void test01()
{
	//普通实现测试
	Calculator c;
	c.m_Num1 = 10;
	c.m_Num2 = 10;
	cout << c.m_Num1 << " + " << c.m_Num2 << " = " << c.getResult("+") << endl;

	cout << c.m_Num1 << " - " << c.m_Num2 << " = " << c.getResult("-") << endl;

	cout << c.m_Num1 << " * " << c.m_Num2 << " = " << c.getResult("*") << endl;
}



//多态实现
//抽象计算器类
//多态优点：代码组织结构清晰，可读性强，利于前期和后期的扩展以及维护
class AbstractCalculator
{
public :

	virtual int getResult()
	{
		return 0;
	}

	int m_Num1;
	int m_Num2;
};

//加法计算器
class AddCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 + m_Num2;
	}
};

//减法计算器
class SubCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 - m_Num2;
	}
};

//乘法计算器
class MulCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 * m_Num2;
	}
};


void test02()
{
	//创建加法计算器
	AbstractCalculator *abc = new AddCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << " + " << abc->m_Num2 << " = " << abc->getResult() << endl;
	delete abc;  //用完了记得销毁

	//创建减法计算器
	abc = new SubCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << " - " << abc->m_Num2 << " = " << abc->getResult() << endl;
	delete abc;

	//创建乘法计算器
	abc = new MulCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << " * " << abc->m_Num2 << " = " << abc->getResult() << endl;
	delete abc;
}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

> 总结：C++开发提倡利用多态设计程序架构，因为多态优点很多

#### 4.7.3 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为**纯虚函数**

纯虚函数语法：`virtual 返回值类型 函数名 （参数列表）= 0 ;`

当类中有了纯虚函数，这个类也称为==抽象类==

**抽象类特点**：

-   无法实例化对象
-   子类必须重写抽象类中的纯虚函数，否则也属于抽象类

**示例：**

```C++
class Base
{
public:
	//纯虚函数
	//类中只要有一个纯虚函数就称为抽象类
	//抽象类无法实例化对象
	//子类必须重写父类中的纯虚函数，否则也属于抽象类
	virtual void func() = 0;
};

class Son :public Base
{
public:
	virtual void func()
	{
		cout << "func调用" << endl;
	};
};

void test01()
{
	Base * base = NULL;
	//base = new Base; // 错误，抽象类无法实例化对象
	base = new Son;
	base->func();
	delete base;//记得销毁
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.7.4 多态案例二-制作饮品

**案例描述：**

制作饮品的大致流程为：煮水 - 冲泡 - 倒入杯中 - 加入辅料

利用多态技术实现本案例，提供抽象制作饮品基类，提供子类制作咖啡和茶叶

![1545985945198](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/1545985945198.png)

**示例：**

```C++
//抽象制作饮品
class AbstractDrinking {
public:
	//烧水
	virtual void Boil() = 0;
	//冲泡
	virtual void Brew() = 0;
	//倒入杯中
	virtual void PourInCup() = 0;
	//加入辅料
	virtual void PutSomething() = 0;
	//规定流程
	void MakeDrink() {
		Boil();
		Brew();
		PourInCup();
		PutSomething();
	}
};

//制作咖啡
class Coffee : public AbstractDrinking {
public:
	//烧水
	virtual void Boil() {
		cout << "煮农夫山泉!" << endl;
	}
	//冲泡
	virtual void Brew() {
		cout << "冲泡咖啡!" << endl;
	}
	//倒入杯中
	virtual void PourInCup() {
		cout << "将咖啡倒入杯中!" << endl;
	}
	//加入辅料
	virtual void PutSomething() {
		cout << "加入牛奶!" << endl;
	}
};

//制作茶水
class Tea : public AbstractDrinking {
public:
	//烧水
	virtual void Boil() {
		cout << "煮自来水!" << endl;
	}
	//冲泡
	virtual void Brew() {
		cout << "冲泡茶叶!" << endl;
	}
	//倒入杯中
	virtual void PourInCup() {
		cout << "将茶水倒入杯中!" << endl;
	}
	//加入辅料
	virtual void PutSomething() {
		cout << "加入枸杞!" << endl;
	}
};

//业务函数
void DoWork(AbstractDrinking* drink) {
	drink->MakeDrink();
	delete drink;
}

void test01() {
	DoWork(new Coffee);
	cout << "--------------" << endl;
	DoWork(new Tea);
}


int main() {

	test01();

	system("pause");

	return 0;
}
```

#### 4.7.5 虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码

解决方式：将父类中的析构函数改为**虚析构**或者**纯虚析构**

虚析构和纯虚析构共性：

-   可以解决父类指针释放子类对象
-   都需要有具体的函数实现

虚析构和纯虚析构区别：

-   如果是纯虚析构，该类属于抽象类，无法实例化对象

虚析构语法：

`virtual ~类名(){}`

纯虚析构语法：

` virtual ~类名() = 0;`

`类名::~类名(){}`

**示例：**

```C++
class Animal {
public:

	Animal()
	{
		cout << "Animal 构造函数调用！" << endl;
	}
	virtual void Speak() = 0;

	//析构函数加上virtual关键字，变成虚析构函数
	//virtual ~Animal()
	//{
	//	cout << "Animal虚析构函数调用！" << endl;
	//}


	virtual ~Animal() = 0;
};

Animal::~Animal()
{
	cout << "Animal 纯虚析构函数调用！" << endl;
}

//和包含普通纯虚函数的类一样，包含了纯虚析构函数的类也是一个抽象类。不能够被实例化。

class Cat : public Animal {
public:
	Cat(string name)
	{
		cout << "Cat构造函数调用！" << endl;
		m_Name = new string(name);
	}
	virtual void Speak()
	{
		cout << *m_Name <<  "小猫在说话!" << endl;
	}
	~Cat()
	{
		cout << "Cat析构函数调用!" << endl;
		if (this->m_Name != NULL) {
			delete m_Name;
			m_Name = NULL;
		}
	}

public:
	string *m_Name;
};

void test01()
{
	Animal *animal = new Cat("Tom");
	animal->Speak();

	//通过父类指针去释放，会导致子类对象可能清理不干净，造成内存泄漏
	//怎么解决？给基类增加一个虚析构函数
	//虚析构函数就是用来解决通过父类指针释放子类对象
	delete animal;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：

1.  虚析构或纯虚析构就是用来解决通过父类指针释放子类对象

2.  如果子类中没有堆区数据，可以不写为虚析构或纯虚析构

3.  拥有纯虚析构函数的类也属于抽象类

#### 4.7.6 多态案例三-电脑组装

**案例描述：**

电脑主要组成部件为 CPU（用于计算），显卡（用于显示），内存条（用于存储）

将每个零件封装出抽象基类，并且提供不同的厂商生产不同的零件，例如 Intel 厂商和 Lenovo 厂商

创建电脑类提供让电脑工作的函数，并且调用每个零件工作的接口

测试时组装三台不同的电脑进行工作

**示例：**

```C++
#include<iostream>
using namespace std;

//抽象CPU类
class CPU
{
public:
	//抽象的计算函数
	virtual void calculate() = 0;
};

//抽象显卡类
class VideoCard
{
public:
	//抽象的显示函数
	virtual void display() = 0;
};

//抽象内存条类
class Memory
{
public:
	//抽象的存储函数
	virtual void storage() = 0;
};

//电脑类
class Computer
{
public:
	Computer(CPU * cpu, VideoCard * vc, Memory * mem)
	{
		m_cpu = cpu;
		m_vc = vc;
		m_mem = mem;
	}

	//提供工作的函数
	void work()
	{
		//让零件工作起来，调用接口
		m_cpu->calculate();

		m_vc->display();

		m_mem->storage();
	}

	//提供析构函数 释放3个电脑零件
	~Computer()
	{

		//释放CPU零件
		if (m_cpu != NULL)
		{
			delete m_cpu;
			m_cpu = NULL;
		}

		//释放显卡零件
		if (m_vc != NULL)
		{
			delete m_vc;
			m_vc = NULL;
		}

		//释放内存条零件
		if (m_mem != NULL)
		{
			delete m_mem;
			m_mem = NULL;
		}
	}

private:

	CPU * m_cpu; //CPU的零件指针
	VideoCard * m_vc; //显卡零件指针
	Memory * m_mem; //内存条零件指针
};

//具体厂商
//Intel厂商
class IntelCPU :public CPU
{
public:
	virtual void calculate()
	{
		cout << "Intel的CPU开始计算了！" << endl;
	}
};

class IntelVideoCard :public VideoCard
{
public:
	virtual void display()
	{
		cout << "Intel的显卡开始显示了！" << endl;
	}
};

class IntelMemory :public Memory
{
public:
	virtual void storage()
	{
		cout << "Intel的内存条开始存储了！" << endl;
	}
};

//Lenovo厂商
class LenovoCPU :public CPU
{
public:
	virtual void calculate()
	{
		cout << "Lenovo的CPU开始计算了！" << endl;
	}
};

class LenovoVideoCard :public VideoCard
{
public:
	virtual void display()
	{
		cout << "Lenovo的显卡开始显示了！" << endl;
	}
};

class LenovoMemory :public Memory
{
public:
	virtual void storage()
	{
		cout << "Lenovo的内存条开始存储了！" << endl;
	}
};


void test01()
{
	//第一台电脑零件
	CPU * intelCpu = new IntelCPU;
	VideoCard * intelCard = new IntelVideoCard;
	Memory * intelMem = new IntelMemory;

	cout << "第一台电脑开始工作：" << endl;
	//创建第一台电脑
	Computer * computer1 = new Computer(intelCpu, intelCard, intelMem);
	computer1->work();
	delete computer1;

	cout << "-----------------------" << endl;
	cout << "第二台电脑开始工作：" << endl;
	//第二台电脑组装
	Computer * computer2 = new Computer(new LenovoCPU, new LenovoVideoCard, new LenovoMemory);;
	computer2->work();
	delete computer2;

	cout << "-----------------------" << endl;
	cout << "第三台电脑开始工作：" << endl;
	//第三台电脑组装
	Computer * computer3 = new Computer(new LenovoCPU, new IntelVideoCard, new LenovoMemory);;
	computer3->work();
	delete computer3;

}
```



