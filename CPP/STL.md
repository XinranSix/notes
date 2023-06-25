[TOC]

## STL 概述

-   STL（Standard Template Library，**标准模板库**）
-   STL 从广义上分为：**容器、算法、迭代器**
-   **容器**和**算法**之间通过**迭代器**进行无缝连接
-   STL 几乎所有的代码都采用了模板类或者模板函数

STL 六大组件：

|    名字    |            别名            |                             说明                             |
| :--------: | :------------------------: | :----------------------------------------------------------: |
|    容器    |         containers         | 各种数据结构，如 `vector`、`list`、`deque`、`set`、`map` 等数据结构 |
|    算法    |     演算法、algorithms     |   各种常用算法，如：`sort`、`search`、`cpoy`、`erase` 等。   |
|   迭代器   |         iterators          |                 扮演了容器与算法之间的胶合剂                 |
|   仿函数   | 仿函式、函数对象、functors |              行为类似函数，可作为算法的某种策略              |
|   适配器   |      配接器、adapters      |         一种用来修饰容器或者仿函数或迭代器接口的东西         |
| 空间配置器 |     配置器、allocators     |                     负责空间的配置与管理                     |

### STL 中容器、算法、迭代器

>  **容器：**置物之所也。

STL **容器**就是将运用**最广泛的一些数据结构**实现出来。

常用的数据结构：array，list，tree，stack，queue，set，map 等。

这些容器分为**序列式容器**和**关联式容器**两种：

 **序列式容器**：强调值的排序，序列式容器中的每个元素均有固定的位置。
​ **关联式容器**：二叉树结构，各元素之间没有严格的物理上的顺序关系。

> **算法：**问题之解法也。

不多说，不知道什么叫算法请 remake.

算法分为：**质变算法**和**非质变算法**。

质变算法：是指运算过程中会更改区间内的元素的内容，如拷贝，替换，删除等等。

非质变算法：是指运算过程中不会更改区间内的元素内容，如查找、计数、遍历、寻找极值等等。

> **迭代器：**容器和算法之间粘合剂。

提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

每个容器都有自己专属的迭代器。

迭代器在使用上非常像指针。

迭代器种分类：

|      种类      |                           功能                           |                         支持运算                         |
| :------------: | :------------------------------------------------------: | :------------------------------------------------------: |
|   输入迭代器   |                     对数据的只读访问                     |               只读，支持 `++`、`==`、`!=`                |
|   输出迭代器   |                     对数据的只写访问                     |                     只写，支持 `++`                      |
|   前向迭代器   |               读写操作，并能向前推进迭代器               |               读写，支持 `++`、`==`、`!=`                |
|   双向迭代器   |               读写操作，并能向前和向后操作               |                  读写，支持 `++`、`--`                   |
| 随机访问迭代器 | 读写操作，可以以跳跃的方式访问任意数据，功能最强的迭代器 | 读写，支持 `++`、`--`、`[n]`、`-n`、`<`、`<=`、`>`、`>=` |

常用的容器中迭代器种类为双向迭代器，和随机访问迭代器。

## 常用容器

### `string` 容器

`char *` 是 C++ 风格的字符串，而 `string` 本质上是一个类。

**`string` 和 `char *` 的区别：**

-   char \* 是一个指针
-   string 是一个类，类内部封装了 char\*，管理这个字符串，是一个 char\*型的容器。

**特点：**

- `string` 类内部封装了很多成员方法，例如：查找 `find`，拷贝 `copy`，删除 `delete` 替换 `replace`，插入 `insert`.
- `string` 管理 `char *` 所分配的内存，不用担心复制越界和取值越界等，由类内部进行负责。

`string` 容器的内置函数。

**构造函数：**

|           函数原型           |                       说明                       |     示例      |
| :--------------------------: | :----------------------------------------------: | :-----------: |
|         `string();`          |                创建一个空的字符串                | `string str;` |
|   `string(const char* s);`   |               使用字符串 s 初始化                |               |
| `string(const string& str);` | 使用一个 `string` 对象初始化另一个 `string` 对象 |               |
|   `string(int n, char c);`   |              使用 n 个字符 c 初始化              |               |

`string` 的多种构造方式没有可比性，灵活使用即可。

**string 赋值操作：**

|                       函数原型                       |                   说明                   | 示例 |
| :--------------------------------------------------: | :--------------------------------------: | :--: |
|         `string& operator=(const char* s);`          |   `char *` 类型字符串赋值给当前字符串    |      |
|        `string& operator=(const string &s);`         |        把字符串 s 赋给当前字符串         |      |
|             `string& operator=(char c);`             |          字符赋值给当前的字符串          |      |
|           `string& assign(const char *s);`           |       把字符串 s 赋给当前的字符串        |      |
|       `string& assign(const char *s, int n);`        | 把字符串 s 的前 n 个字符赋给当前的字符串 |      |
|          `string& assign(const string &s);`          |        把字符串 s 赋给当前字符串         |      |
|           `string& assign(int n, char c);`           |       用 n 个字符 c 赋给当前字符串       |      |
| `string& assign(const string &s, int start, int n);` | 将 s 从 start 开始 n 个字符赋值给字符串  |      |

> `string` 的赋值方式很多，`operator=`  这种方式是比较实用的。

**string 拼接操作：**

|                      函数原型                      |                       说明                        | 示例 |
| :------------------------------------------------: | :-----------------------------------------------: | :--: |
|       `string& operator+=(const char* str);`       |                 重载 `+=` 运算符                  |      |
|        `string& operator+=(const char c);`         |                 重载 `+=` 运算符                  |      |
|      `string& operator+=(const string& str);`      |                 重载 `+=` 运算符                  |      |
|          `string& append(const char *s);`          |          把字符串 s 连接到当前字符串结尾          |      |
|      `string& append(const char *s, int n);`       |   把字符串 s 的前 n 个字符连接到当前字符串结尾    |      |
|         `string& append(const string &s);`         |        同 `operator+=(const string& str)`         |      |
| `string& append(const string &s, int pos, int n);` | 字符串 s 中从 pos 开始的 n 个字符连接到字符串结尾 |      |
|          `string& append(int n, char c);`          |          在当前字符串结尾添加 n 个字符 c          |      |

**string 存取字符操作：**

|          函数原型          |           说明           | 示例 |
| :------------------------: | :----------------------: | :--: |
| `char& operator[](int n);` |   通过 `[]` 方式取字符   |      |
|     `char& at(int n);`     | 通过 `at()` 函数获取字符 |      |

**string 查找和替换：**

|                       函数原型                        |                   说明                    | 示例 |
| :---------------------------------------------------: | :---------------------------------------: | :--: |
|   `int find(const string& str, int pos = 0) const;`   | 查找 str 第一次出现位置，从 pos 开始查找  |      |
|     `int find(const char* s, int pos = 0) const;`     |   查找 s 第一次出现位置,从 pos 开始查找   |      |
|   `int find(const char* s, int pos, int n) const;`    | 从 pos 位置查找 s 的前 n 个字符第一次位置 |      |
|     `int find(const char c, int pos = 0) const;`      |         查找字符 c 第一次出现位置         |      |
| `int rfind(const string& str, int pos = npos) const;` |  查找 str 最后一次位置，从 pos 开始查找   |      |
|   `int rfind(const char* s, int pos = npos) const;`   | 查找 s 最后一次出现位置，从 pos 开始查找  |      |
|   `int rfind(const char* s, int pos, int n) const;`   |  从 pos 查找 s 的前 n 个字符最后一次位置  |      |
|     `int rfind(const char c, int pos = 0) const;`     |        查找字符 c 最后一次出现位置        |      |
| `string& replace(int pos, int n, const string& str);` |   替换从 pos 开始 n 个字符为字符串 str    |      |
|   `string& replace(int pos, int n, const char* s);`   |   替换从 pos 开始的 n 个字符为字符串 s    |      |

> - `find` 查找是从左往后，`rfind` 从右往左
> - find 找到字符串后返回查找的第一个字符位置，找不到返回 -1
> - replace 在替换时，要指定从哪个位置起，多少个字符，替换成什么样的字符串

**string 比较：**

|               函数原型                |      说明       | 示例 |
| :-----------------------------------: | :-------------: | :--: |
| `int compare(const string &s) const;` | 与字符串 s 比较 |      |
|  `int compare(const char *s) const;`  | 与字符串 s 比较 |      |

> 字符串比较是按字符的 ASCII 码进行对比：
>
> - = 返回 0
>- \> 返回 1
> - < 返回 -1
> 

**string 插入和删除：**

|                   函数原型                    |            说明            | 示例 |
| :-------------------------------------------: | :------------------------: | :--: |
|   `string& insert(int pos, const char* s);`   |         插入字符串         |      |
| `string& insert(int pos, const string& str);` |         插入字符串         |      |
|   `string& insert(int pos, int n, char c);`   | 在指定位置插入 n 个字符 c  |      |
|    `string& erase(int pos, int n = npos);`    | 删除从 Pos 开始的 n 个字符 |      |

**string 子串：**

|                     函数原型                      |                  说明                  | 示例 |
| :-----------------------------------------------: | :------------------------------------: | :--: |
| `string substr(int pos = 0, int n = npos) const;` | 返回从 pos 开始的 n 个字符组成的字符串 |      |

**string 和 c-style 字符串转换：**

```cpp
//string 转 char*
string str = "lxr";
const char* cstr = str.c_str();

//char* 转 string
char* s = "itcast";
string str(s);
```

> 在 c++中存在 `const char *` 到 `string` 的隐式类型转换，不存在从 `string` 对象到 `c-string` 的自动类型转换。对于 `string` 类型的字符串，可以通过 `c_str()` 成员函数，返回 `string` 对象对应的 `c-string`.
>
> 为了修改 `string` 字符串的内容，可以使用下标操作符 [] 或 at，它们都会返回字符的引用，但当字符串的内存被重新分配之后，可能发生错误。

### `vector` 容器

vector 数据结构和**数组非常相似**。

**vector 与普通数组区别：**不同之处在于数组是静态空间，而 `vector` 可以**动态扩容**。

**动态扩展：**并不是在原空间之后续接新空间，而是找更大的内存空间，然后将原数据拷贝新空间，释放原空间。

`vector` 容器的迭代器是支持随机访问的迭代器。

![image](https://github.com/XinranSix/docs/assets/62458905/8a08605d-92ee-417a-915f-b16622df34f4)

**vector 构造函数：**

|             函数              |                     说明                      | 示例 |
| :---------------------------: | :-------------------------------------------: | :--: |
|        `vector<T> v;`         |       采用模板实现类实现，默认构造函数        |      |
| `vector(v.begin(), v.end());` | 将 `v[begin(), end())` 区间中的元素拷贝给本身 |      |
|      `vector(n, elem);`       |        构造函数将 n 个 elem 拷贝给本身        |      |
| `vector(const vector &vec);`  |                 拷贝构造函数                  |      |

**vector 赋值操作：**

|                  函数                   |                    说明                    | 示例 |
| :-------------------------------------: | :----------------------------------------: | :--: |
| `vector& operator=(const vector &vec);` |               重载等号操作符               |      |
|           `assign(beg, end);`           | 将 `[beg, end)` 区间中的数据拷贝赋值给本身 |      |
|           `assign(n, elem);`            |        将 n 个 elem 拷贝赋值给本身         |      |

v**ector 容量和大小：**

|           函数           |                             说明                             | 示例 |
| :----------------------: | :----------------------------------------------------------: | :--: |
|        `size();`         |                     返回容器中元素的个数                     |      |
|        `empty();`        |                       判断容器是否为空                       |      |
|      `capacity();`       |                          容器的容量                          |      |
|    `resize(int num);`    | 重新指定容器的长度为 num，若容器变长，则以默认值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |
| `resize(int num, elem);` | 重新指定容器的长度为 num，若容器变长，则以 elem 值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |

**vector 数据存取操作：**

|      函数      |            说明            | 示例 |
| :------------: | :------------------------: | :--: |
| `at(int idx);` |  返回索引 idx 所指的数据   |      |
| `operator[];`  |  返回索引 idx 所指的数据   |      |
|   `front();`   |  返回容器中第一个数据元素  |      |
|   `back();`    | 返回容器中最后一个数据元素 |      |

**vector 插入和删除：**

|                        函数                        |                   说明                   | 示例 |
| :------------------------------------------------: | :--------------------------------------: | :--: |
|                 `push_back(ele);`                  |             尾部插入元素 ele             |      |
|                   `pop_back();`                    |             删除最后一个元素             |      |
|         `insert(const_iterator pos, ele);`         |     迭代器指向位置 pos 插入元素 ele      |      |
|   `insert(const_iterator pos, int count, ele);`    | 迭代器指向位置 pos 插入 count 个元素 ele |      |
|            `erase(const_iterator pos);`            |           删除迭代器指向的元素           |      |
| `erase(const_iterator start, const_iterator end);` |   删除迭代器从 start 到 end 之间的元素   |      |
|                     `clear();`                     |            删除容器中所有元素            |      |

**vector 互换容器：**

|     函数     |          说明           | 示例 |
| :----------: | :---------------------: | :--: |
| `swap(vec);` | 将 vec 与本身的元素互换 |      |

> swap 可以使两个容器互换，可以达到收缩内存的效果。

**vector 预留空间：**

|        函数         |                           说明                            | 示例 |
| :-----------------: | :-------------------------------------------------------: | :--: |
| `reserve(int len);` | 容器预留 len 个元素长度，预留位置不初始化，元素不可访问。 |      |

> 如果数据量较大，可以一开始利用 reserve 预留空间。

### `deque` 容器

双端数组，可以对头端进行插入删除操作

**deque 与 vector 区别：**

-   `vector` 对于头部的插入删除效率低，数据量越大，效率越低
-   `deque` 相对而言，对头部的插入删除速度回比 vector 快
-   `vector` 访问元素时的速度会比 deque 快，这和两者内部实现有关

![image](https://github.com/XinranSix/docs/assets/62458905/4a454687-deac-4040-8c49-beb1a395e681)

`deque` 内部工作原理:

`deque` 内部有个**中控器**，维护每段缓冲区中的内容，缓冲区中存放真实数据，中控器维护的是每个缓冲区的地址，使得使用 `deque` 时像一片连续的内存空间。

![image](https://github.com/XinranSix/docs/assets/62458905/ced135ee-5483-4f88-97be-3c4d3b530d54)

`deque` 容器的迭代器也是支持随机访问的。

**deque 构造函数：**

|            函数            |                      说明                      | 示例 |
| :------------------------: | :--------------------------------------------: | :--: |
|         `deque<T>`         |                  默认构造形式                  |      |
|     `deque(beg, end);`     | 构造函数将 `[beg, end)` 区间中的元素拷贝给本身 |      |
|     `deque(n, elem);`      |        构造函数将 n 个 elem 拷贝给本身         |      |
| `deque(const deque &deq);` |                  拷贝构造函数                  |      |

**deque 赋值操作：**

|                 函数                  |                    说明                    | 示例 |
| :-----------------------------------: | :----------------------------------------: | :--: |
| `deque& operator=(const deque &deq);` |               重载等号操作符               |      |
|          `assign(beg, end);`          | 将 `[beg, end)` 区间中的数据拷贝赋值给本身 |      |
|          `assign(n, elem);`           |        将 n 个 elem 拷贝赋值给本身         |      |

**deque 互换容器：**

|     函数     |          说明           | 示例 |
| :----------: | :---------------------: | :--: |
| `swap(deq);` | 将 deq 与本身的元素互换 |      |

**deque 大小操作：**

|            函数            |                             说明                             | 示例 |
| :------------------------: | :----------------------------------------------------------: | ---- |
|      `deque.empty();`      |                       判断容器是否为空                       |      |
|      `deque.size();`       |                     返回容器中元素的个数                     |      |
|    `deque.resize(num);`    | 重新指定容器的长度为 num，若容器变长，则以默认值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |
| `deque.resize(num, elem);` | 重新指定容器的长度为 num，若容器变长，则以 elem 值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |

**deque 双端插入和删除操作：**

|        函数         |          说明          | 示例 |
| :-----------------: | :--------------------: | :--: |
| `push_back(elem);`  | 在容器尾部添加一个数据 |      |
| `push_front(elem);` | 在容器头部插入一个数据 |      |
|    `pop_back();`    |  删除容器最后一个数据  |      |
|   `pop_front();`    |   删除容器第一个数据   |      |

**deque 插入和删除操作：**

|          函数          |                         说明                          | 示例 |
| :--------------------: | :---------------------------------------------------: | :--: |
|  `insert(pos,elem);`   | 在 pos 位置插入一个 elem 元素的拷贝，返回新数据的位置 |      |
| `insert(pos, n,elem);` |       在 pos 位置插入 n 个 elem 数据，无返回值        |      |
| `insert(pos,beg,end);` |   在 pos 位置插入 `[beg,end)` 区间的数据，无返回值    |      |
|       `clear();`       |                  清空容器的所有数据                   |      |
|   `erase(beg,end);`    |   删除 `[beg,end)` 区间的数据，返回下一个数据的位置   |      |
|     `erase(pos);`      |      删除 pos 位置的数据，返回下一个数据的位置。      |      |

**deque 数据存取：**

|      函数      |            说明            | 示例 |
| :------------: | :------------------------: | :--: |
| `at(int idx);` |  返回索引 idx 所指的数据   |      |
| `operator[];`  |  返回索引 idx 所指的数据   |      |
|   `front();`   |  返回容器中第一个数据元素  |      |
|   `back();`    | 返回容器中最后一个数据元素 |      |

### `stack` 容器

不知道什么是 stack 的请自重。

`stack` 没有迭代器。

**stack 构造器：**

|            函数            |                      说明                       | 示例 |
| :------------------------: | :---------------------------------------------: | :--: |
|      `stack<T> stk;`       | stack 采用模板类实现， stack 对象的默认构造形式 |      |
| `stack(const stack &stk);` |                  拷贝构造函数                   |      |

**stack 赋值操作：**

|                 函数                  |      说明      | 示例 |
| :-----------------------------------: | :------------: | :--: |
| `stack& operator=(const stack &stk);` | 重载等号操作符 |      |

**stack 数据存取：**

|     函数      |         说明         | 示例 |
| :-----------: | :------------------: | :--: |
| `push(elem);` |    向栈顶添加元素    |      |
|   `pop();`    | 从栈顶移除第一个元素 |      |
|   `top();`    |     返回栈顶元素     |      |

**stack 大小操作：**

|    函数    |      说明      | 示例 |
| :--------: | :------------: | :--: |
| `empty();` | 判断栈是否为空 |      |
| `size();`  |   回栈的大小   |      |

### `queue` 容器

#### 3.6.1 queue 基本概念

**概念：**队列是一种 FIFO 的数据结构。

![image](https://github.com/XinranSix/docs/assets/62458905/10400176-5ec1-48c4-abd6-56ba7ada0ee7)

队列容器允许从一端新增元素，从另一端移除元素。

队列中只有队头和队尾才可以被外界使用，因此队列没有迭代器。

**queue 构造函数：**

|            函数            |                      说明                      | 示例 |
| :------------------------: | :--------------------------------------------: | :--: |
|      `queue<T> que;`       | queue 采用模板类实现，queue 对象的默认构造形式 |      |
| `queue(const queue &que);` |                  拷贝构造函数                  |      |

**queue 赋值操作：**

|                 函数                  |      说明      | 示例 |
| :-----------------------------------: | :------------: | :--: |
| `queue& operator=(const queue &que);` | 重载等号操作符 |      |

**queue 数据存取：**

|     函数      |         说明         | 示例 |
| :-----------: | :------------------: | :--: |
| `push(elem);` |    往队尾添加元素    |      |
|   `pop();`    | 从队头移除第一个元素 |      |
|   `back();`   |   返回最后一个元素   |      |
|  `front();`   |    返回第一个元素    |      |

**queue 大小操作：**

|    函数    |       说明       | 示例 |
| :--------: | :--------------: | :--: |
| `empty();` | 判断堆栈是否为空 |      |
| `size();`  |   返回栈的大小   |      |

### list 容器

#### 3.7.1 list 基本概念

**功能：**将数据进行链式存储

**链表**（list）是一种物理存储单元上非连续的存储结构，数据元素的逻辑顺序是通过链表中的指针链接实现的

链表的组成：链表由一系列**结点**组成

结点的组成：一个是存储数据元素的**数据域**，另一个是存储下一个结点地址的**指针域**

STL 中的链表是一个双向循环链表

![说明: 2015-11-15_225145](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/8919/clip_image002-1547608564071.jpg)

由于链表的存储方式并不是连续的内存空间，因此链表 list 中的迭代器只支持前移和后移，属于**双向迭代器**

list 的优点：

-   采用动态存储分配，不会造成内存浪费和溢出
-   链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素

list 的缺点：

-   链表灵活，但是空间(指针域) 和 时间（遍历）额外耗费较大

List 有一个重要的性质，插入操作和删除操作都不会造成原有 list 迭代器的失效，这在 vector 是不成立的。

总结：STL 中**List 和 vector 是两个最常被使用的容器**，各有优缺点

#### 3.7.2 list 构造函数

**功能描述：**

-   创建 list 容器

**函数原型：**

-   `list<T> lst;` //list 采用采用模板类实现,对象的默认构造形式：
-   `list(beg,end);` //构造函数将[beg, end)区间中的元素拷贝给本身。
-   `list(n,elem);` //构造函数将 n 个 elem 拷贝给本身。
-   `list(const list &lst);` //拷贝构造函数。

**示例：**

```C++

```

总结：list 构造方式同其他几个 STL 常用容器，熟练掌握即可

#### 3.7.3 list 赋值和交换

**功能描述：**

-   给 list 容器进行赋值，以及交换 list 容器

**函数原型：**

-   `assign(beg, end);` //将[beg, end)区间中的数据拷贝赋值给本身。
-   `assign(n, elem);` //将 n 个 elem 拷贝赋值给本身。
-   `list& operator=(const list &lst);` //重载等号操作符
-   `swap(lst);` //将 lst 与本身的元素互换。

**示例：**

```C++

```

总结：list 赋值和交换操作能够灵活运用即可

#### 3.7.4 list 大小操作

**功能描述：**

-   对 list 容器的大小进行操作

**函数原型：**

- `size(); ` //返回容器中元素的个数

- `empty(); ` //判断容器是否为空

- `resize(num);` //重新指定容器的长度为 num，若容器变长，则以默认值填充新位置。

   //如果容器变短，则末尾超出容器长度的元素被删除。

- `resize(num, elem); ` //重新指定容器的长度为 num，若容器变长，则以 elem 值填充新位置。

  //如果容器变短，则末尾超出容器长度的元素被删除。

**示例：**

```C++

```

总结：

-   判断是否为空 --- empty
-   返回元素个数 --- size
-   重新指定个数 --- resize

#### 3.7.5 list 插入和删除

**功能描述：**

-   对 list 容器进行数据的插入和删除

**函数原型：**

-   push_back(elem);//在容器尾部加入一个元素
-   pop_back();//删除容器中最后一个元素
-   push_front(elem);//在容器开头插入一个元素
-   pop_front();//从容器开头移除第一个元素
-   insert(pos,elem);//在 pos 位置插 elem 元素的拷贝，返回新数据的位置。
-   insert(pos,n,elem);//在 pos 位置插入 n 个 elem 数据，无返回值。
-   insert(pos,beg,end);//在 pos 位置插入[beg,end)区间的数据，无返回值。
-   clear();//移除容器的所有数据
-   erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。
-   erase(pos);//删除 pos 位置的数据，返回下一个数据的位置。
-   remove(elem);//删除容器中所有与 elem 值匹配的元素。

**示例：**

```C++

```

总结：

-   尾插 --- push_back
-   尾删 --- pop_back
-   头插 --- push_front
-   头删 --- pop_front
-   插入 --- insert
-   删除 --- erase
-   移除 --- remove
-   清空 --- clear

#### 3.7.6 list 数据存取

**功能描述：**

-   对 list 容器中数据进行存取

**函数原型：**

-   `front();` //返回第一个元素。
-   `back();` //返回最后一个元素。

**示例：**

```C++

```

总结：

-   list 容器中不可以通过[]或者 at 方式访问数据
-   返回第一个元素 --- front
-   返回最后一个元素 --- back

#### 3.7.7 list 反转和排序

**功能描述：**

-   将容器中的元素反转，以及将容器中的数据进行排序

**函数原型：**

-   `reverse();` //反转链表
-   `sort();` //链表排序

**示例：**

```C++

```

总结：

-   反转 --- reverse
-   排序 --- sort （成员函数）

#### 3.7.8 排序案例

案例描述：将 Person 自定义数据类型进行排序，Person 中属性有姓名、年龄、身高

排序规则：按照年龄进行升序，如果年龄相同按照身高进行降序

**示例：**

```C++

```

总结：

-   对于自定义数据类型，必须要指定排序规则，否则编译器不知道如何进行排序

-   高级排序只是在排序规则上再进行一次逻辑规则制定，并不复杂

### set/ multiset 容器

#### 3.8.1 set 基本概念

**简介：**

-   所有元素都会在插入时自动被排序

**本质：**

-   set/multiset 属于**关联式容器**，底层结构是用**二叉树**实现。

**set 和 multiset 区别**：

-   set 不允许容器中有重复的元素
-   multiset 允许容器中有重复的元素

#### 3.8.2 set 构造和赋值

功能描述：创建 set 容器以及赋值

构造：

-   `set<T> st;` //默认构造函数：
-   `set(const set &st);` //拷贝构造函数

赋值：

-   `set& operator=(const set &st);` //重载等号操作符

**示例：**

```C++

```

总结：

-   set 容器插入数据时用 insert
-   set 容器插入数据的数据会自动排序

#### 3.8.3 set 大小和交换

**功能描述：**

-   统计 set 容器大小以及交换 set 容器

**函数原型：**

-   `size();` //返回容器中元素的数目
-   `empty();` //判断容器是否为空
-   `swap(st);` //交换两个集合容器

**示例：**

```C++

```

总结：

-   统计大小 --- size
-   判断是否为空 --- empty
-   交换容器 --- swap

#### 3.8.4 set 插入和删除

**功能描述：**

-   set 容器进行插入数据和删除数据

**函数原型：**

-   `insert(elem);` //在容器中插入元素。
-   `clear();` //清除所有元素
-   `erase(pos);` //删除 pos 迭代器所指的元素，返回下一个元素的迭代器。
-   `erase(beg, end);` //删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
-   `erase(elem);` //删除容器中值为 elem 的元素。

**示例：**

```C++

```

总结：

-   插入 --- insert
-   删除 --- erase
-   清空 --- clear

#### 3.8.5 set 查找和统计

**功能描述：**

-   对 set 容器进行查找数据以及统计数据

**函数原型：**

-   `find(key);` //查找 key 是否存在,若存在，返回该键的元素的迭代器；若不存在，返回 set.end();
-   `count(key);` //统计 key 的元素个数

**示例：**

```C++

```

总结：

-   查找 --- find （返回的是迭代器）
-   统计 --- count （对于 set，结果为 0 或者 1）

#### 3.8.6 set 和 multiset 区别

**学习目标：**

-   掌握 set 和 multiset 的区别

**区别：**

-   set 不可以插入重复数据，而 multiset 可以
-   set 插入数据的同时会返回插入结果，表示插入是否成功
-   multiset 不会检测数据，因此可以插入重复数据

**示例：**

```C++

```

总结：

-   如果不允许插入重复数据可以利用 set
-   如果需要插入重复数据利用 multiset

#### 3.8.7 pair 对组创建

**功能描述：**

-   成对出现的数据，利用对组可以返回两个数据

**两种创建方式：**

-   `pair<type, type> p ( value1, value2 );`
-   `pair<type, type> p = make_pair( value1, value2 );`

**示例：**

```C++

```

总结：

两种方式都可以创建对组，记住一种即可

#### 3.8.8 set 容器排序

学习目标：

-   set 容器默认排序规则为从小到大，掌握如何改变排序规则

主要技术点：

-   利用仿函数，可以改变排序规则

**示例一** set 存放内置数据类型

```C++

```

总结：利用仿函数可以指定 set 容器的排序规则

**示例二** set 存放自定义数据类型

```C++

```

总结：

对于自定义数据类型，set 必须指定排序规则才可以插入数据

### map / multimap 容器

#### 3.9.1 map 基本概念

**简介：**

-   map 中所有元素都是 pair
-   pair 中第一个元素为 key（键值），起到索引作用，第二个元素为 value（实值）
-   所有元素都会根据元素的键值自动排序

**本质：**

-   map/multimap 属于**关联式容器**，底层结构是用二叉树实现。

**优点：**

-   可以根据 key 值快速找到 value 值

map 和 multimap**区别**：

-   map 不允许容器中有重复 key 值元素
-   multimap 允许容器中有重复 key 值元素

#### 3.9.2 map 构造和赋值

**功能描述：**

-   对 map 容器进行构造和赋值操作

**函数原型：**

**构造：**

-   `map<T1, T2> mp;` //map 默认构造函数:
-   `map(const map &mp);` //拷贝构造函数

**赋值：**

-   `map& operator=(const map &mp);` //重载等号操作符

**示例：**

```C++

```

总结：map 中所有元素都是成对出现，插入数据时候要使用对组

#### 3.9.3 map 大小和交换

**功能描述：**

-   统计 map 容器大小以及交换 map 容器

函数原型：

-   `size();` //返回容器中元素的数目
-   `empty();` //判断容器是否为空
-   `swap(st);` //交换两个集合容器

**示例：**

```C++

```

总结：

-   统计大小 --- size
-   判断是否为空 --- empty
-   交换容器 --- swap

#### 3.9.4 map 插入和删除

**功能描述：**

-   map 容器进行插入数据和删除数据

**函数原型：**

-   `insert(elem);` //在容器中插入元素。
-   `clear();` //清除所有元素
-   `erase(pos);` //删除 pos 迭代器所指的元素，返回下一个元素的迭代器。
-   `erase(beg, end);` //删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。
-   `erase(key);` //删除容器中值为 key 的元素。

**示例：**

```C++

```

总结：

-   map 插入方式很多，记住其一即可

*   插入 --- insert
*   删除 --- erase
*   清空 --- clear

#### 3.9.5 map 查找和统计

**功能描述：**

-   对 map 容器进行查找数据以及统计数据

**函数原型：**

-   `find(key);` //查找 key 是否存在,若存在，返回该键的元素的迭代器；若不存在，返回 set.end();
-   `count(key);` //统计 key 的元素个数

**示例：**

```C++

```

总结：

-   查找 --- find （返回的是迭代器）
-   统计 --- count （对于 map，结果为 0 或者 1）

#### 3.9.6 map 容器排序

**学习目标：**

-   map 容器默认排序规则为 按照 key 值进行 从小到大排序，掌握如何改变排序规则

**主要技术点:**

-   利用仿函数，可以改变排序规则

**示例：**

```C++

```

总结：

-   利用仿函数可以指定 map 容器的排序规则
-   对于自定义数据类型，map 必须要指定排序规则,同 set 容器

### 3.10 案例-员工分组

#### 3.10.1 案例描述

-   公司今天招聘了 10 个员工（ABCDEFGHIJ），10 名员工进入公司之后，需要指派员工在那个部门工作
-   员工信息有: 姓名 工资组成；部门分为：策划、美术、研发
-   随机给 10 名员工分配部门和工资
-   通过 multimap 进行信息的插入 key(部门编号) value(员工)
-   分部门显示员工信息

#### 3.10.2 实现步骤

1. 创建 10 名员工，放到 vector 中
2. 遍历 vector 容器，取出每个员工，进行随机分组
3. 分组后，将员工部门编号作为 key，具体员工作为 value，放入到 multimap 容器中
4. 分部门显示员工信息

**案例代码：**

```C++

```

总结：

-   当数据以键值对形式存在，可以考虑用 map 或 multimap

## 4 STL- 函数对象

### 4.1 函数对象

#### 4.1.1 函数对象概念

**概念：**

-   重载**函数调用操作符**的类，其对象常称为**函数对象**
-   **函数对象**使用重载的()时，行为类似函数调用，也叫**仿函数**

**本质：**

函数对象(仿函数)是一个**类**，不是一个函数

#### 4.1.2 函数对象使用

**特点：**

-   函数对象在使用时，可以像普通函数那样调用, 可以有参数，可以有返回值
-   函数对象超出普通函数的概念，函数对象可以有自己的状态
-   函数对象可以作为参数传递

**示例:**

```C++
#include <string>

//1、函数对象在使用时，可以像普通函数那样调用, 可以有参数，可以有返回值
class MyAdd
{
public :
	int operator()(int v1,int v2)
	{
		return v1 + v2;
	}
};

void test01()
{
	MyAdd myAdd;
	cout << myAdd(10, 10) << endl;
}

//2、函数对象可以有自己的状态
class MyPrint
{
public:
	MyPrint()
	{
		count = 0;
	}
	void operator()(string test)
	{
		cout << test << endl;
		count++; //统计使用次数
	}

	int count; //内部自己的状态
};
void test02()
{
	MyPrint myPrint;
	myPrint("hello world");
	myPrint("hello world");
	myPrint("hello world");
	cout << "myPrint调用次数为： " << myPrint.count << endl;
}

//3、函数对象可以作为参数传递
void doPrint(MyPrint &mp , string test)
{
	mp(test);
}

void test03()
{
	MyPrint myPrint;
	doPrint(myPrint, "Hello C++");
}

int main() {

	//test01();
	//test02();
	test03();

	system("pause");

	return 0;
}
```

总结：

-   仿函数写法非常灵活，可以作为参数进行传递。

### 4.2 谓词

#### 4.2.1 谓词概念

**概念：**

-   返回 bool 类型的仿函数称为**谓词**
-   如果 operator()接受一个参数，那么叫做一元谓词
-   如果 operator()接受两个参数，那么叫做二元谓词

#### 4.2.2 一元谓词

**示例：**

```C++
#include <vector>
#include <algorithm>

//1.一元谓词
struct GreaterFive{
	bool operator()(int val) {
		return val > 5;
	}
};

void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}

	vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterFive());
	if (it == v.end()) {
		cout << "没找到!" << endl;
	}
	else {
		cout << "找到:" << *it << endl;
	}

}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：参数只有一个的谓词，称为一元谓词

#### 4.2.3 二元谓词

**示例：**

```C++
#include <vector>
#include <algorithm>
//二元谓词
class MyCompare
{
public:
	bool operator()(int num1, int num2)
	{
		return num1 > num2;
	}
};

void test01()
{
	vector<int> v;
	v.push_back(10);
	v.push_back(40);
	v.push_back(20);
	v.push_back(30);
	v.push_back(50);

	//默认从小到大
	sort(v.begin(), v.end());
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
	cout << "----------------------------" << endl;

	//使用函数对象改变算法策略，排序从大到小
	sort(v.begin(), v.end(), MyCompare());
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：参数只有两个的谓词，称为二元谓词

### 4.3 内建函数对象

#### 4.3.1 内建函数对象意义

**概念：**

-   STL 内建了一些函数对象

**分类:**

-   算术仿函数

-   关系仿函数

-   逻辑仿函数

**用法：**

-   这些仿函数所产生的对象，用法和一般函数完全相同
-   使用内建函数对象，需要引入头文件 `#include<functional>`

#### 4.3.2 算术仿函数

**功能描述：**

-   实现四则运算
-   其中 negate 是一元运算，其他都是二元运算

**仿函数原型：**

-   `template<class T> T plus<T>` //加法仿函数
-   `template<class T> T minus<T>` //减法仿函数
-   `template<class T> T multiplies<T>` //乘法仿函数
-   `template<class T> T divides<T>` //除法仿函数
-   `template<class T> T modulus<T>` //取模仿函数
-   `template<class T> T negate<T>` //取反仿函数

**示例：**

```C++
#include <functional>
//negate
void test01()
{
	negate<int> n;
	cout << n(50) << endl;
}

//plus
void test02()
{
	plus<int> p;
	cout << p(10, 20) << endl;
}

int main() {

	test01();
	test02();

	system("pause");

	return 0;
}
```

总结：使用内建函数对象时，需要引入头文件 `#include <functional>`

#### 4.3.3 关系仿函数

**功能描述：**

-   实现关系对比

**仿函数原型：**

-   `template<class T> bool equal_to<T>` //等于
-   `template<class T> bool not_equal_to<T>` //不等于
-   `template<class T> bool greater<T>` //大于
-   `template<class T> bool greater_equal<T>` //大于等于
-   `template<class T> bool less<T>` //小于
-   `template<class T> bool less_equal<T>` //小于等于

**示例：**

```C++
#include <functional>
#include <vector>
#include <algorithm>

class MyCompare
{
public:
	bool operator()(int v1,int v2)
	{
		return v1 > v2;
	}
};
void test01()
{
	vector<int> v;

	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(40);
	v.push_back(20);

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;

	//自己实现仿函数
	//sort(v.begin(), v.end(), MyCompare());
	//STL内建仿函数  大于仿函数
	sort(v.begin(), v.end(), greater<int>());

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：关系仿函数中最常用的就是 greater<>大于

#### 4.3.4 逻辑仿函数

**功能描述：**

-   实现逻辑运算

**函数原型：**

-   `template<class T> bool logical_and<T>` //逻辑与
-   `template<class T> bool logical_or<T>` //逻辑或
-   `template<class T> bool logical_not<T>` //逻辑非

**示例：**

```C++
#include <vector>
#include <functional>
#include <algorithm>
void test01()
{
	vector<bool> v;
	v.push_back(true);
	v.push_back(false);
	v.push_back(true);
	v.push_back(false);

	for (vector<bool>::iterator it = v.begin();it!= v.end();it++)
	{
		cout << *it << " ";
	}
	cout << endl;

	//逻辑非  将v容器搬运到v2中，并执行逻辑非运算
	vector<bool> v2;
	v2.resize(v.size());
	transform(v.begin(), v.end(),  v2.begin(), logical_not<bool>());
	for (vector<bool>::iterator it = v2.begin(); it != v2.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：逻辑仿函数实际应用较少，了解即可

## STL- 常用算法

**概述**:

-   算法主要是由头文件`<algorithm>` `<functional>` `<numeric>`组成。

-   `<algorithm>`是所有 STL 头文件中最大的一个，范围涉及到比较、 交换、查找、遍历操作、复制、修改等等
-   `<numeric>`体积很小，只包括几个在序列上面进行简单数学运算的模板函数
-   `<functional>`定义了一些模板类,用以声明函数对象。

### 5.1 常用遍历算法

**学习目标：**

-   掌握常用的遍历算法

**算法简介：**

-   `for_each` //遍历容器
-   `transform` //搬运容器到另一个容器中

#### 5.1.1 for_each

**功能描述：**

-   实现遍历容器

**函数原型：**

- `for_each(iterator beg, iterator end, _func); `

  // 遍历算法 遍历容器元素

  // beg 开始迭代器

  // end 结束迭代器

  // \_func 函数或者函数对象

**示例：**

```C++
#include <algorithm>
#include <vector>

//普通函数
void print01(int val)
{
	cout << val << " ";
}
//函数对象
class print02
{
 public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

//for_each算法基本用法
void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}

	//遍历算法
	for_each(v.begin(), v.end(), print01);
	cout << endl;

	for_each(v.begin(), v.end(), print02());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**for_each 在实际开发中是最常用遍历算法，需要熟练掌握

#### 5.1.2 transform

**功能描述：**

-   搬运容器到另一个容器中

**函数原型：**

-   `transform(iterator beg1, iterator end1, iterator beg2, _func);`

//beg1 源容器开始迭代器

//end1 源容器结束迭代器

//beg2 目标容器开始迭代器

//\_func 函数或者函数对象

**示例：**

```C++
#include<vector>
#include<algorithm>

//常用遍历算法  搬运 transform

class TransForm
{
public:
	int operator()(int val)
	{
		return val;
	}

};

class MyPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}

	vector<int>vTarget; //目标容器

	vTarget.resize(v.size()); // 目标容器需要提前开辟空间

	transform(v.begin(), v.end(), vTarget.begin(), TransForm());

	for_each(vTarget.begin(), vTarget.end(), MyPrint());
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：** 搬运的目标容器必须要提前开辟空间，否则无法正常搬运

### 5.2 常用查找算法

学习目标：

-   掌握常用的查找算法

**算法简介：**

-   `find` //查找元素
-   `find_if` //按条件查找元素
-   `adjacent_find` //查找相邻重复元素
-   `binary_search` //二分查找法
-   `count` //统计元素个数
-   `count_if` //按条件统计元素个数

#### 5.2.1 find

**功能描述：**

-   查找指定元素，找到返回指定元素的迭代器，找不到返回结束迭代器 end()

**函数原型：**

- `find(iterator beg, iterator end, value); `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // value 查找的元素

**示例：**

```C++
#include <algorithm>
#include <vector>
#include <string>
void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++) {
		v.push_back(i + 1);
	}
	//查找容器中是否有 5 这个元素
	vector<int>::iterator it = find(v.begin(), v.end(), 5);
	if (it == v.end())
	{
		cout << "没有找到!" << endl;
	}
	else
	{
		cout << "找到:" << *it << endl;
	}
}

class Person {
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	//重载==
	bool operator==(const Person& p)
	{
		if (this->m_Name == p.m_Name && this->m_Age == p.m_Age)
		{
			return true;
		}
		return false;
	}

public:
	string m_Name;
	int m_Age;
};

void test02() {

	vector<Person> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);

	vector<Person>::iterator it = find(v.begin(), v.end(), p2);
	if (it == v.end())
	{
		cout << "没有找到!" << endl;
	}
	else
	{
		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
	}
}
```

总结： 利用 find 可以在容器中找指定的元素，返回值是**迭代器**

#### 5.2.2 find_if

**功能描述：**

-   按条件查找元素

**函数原型：**

- `find_if(iterator beg, iterator end, _Pred); `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // \_Pred 函数或者谓词（返回 bool 类型的仿函数）

**示例：**

```C++
#include <algorithm>
#include <vector>
#include <string>

//内置数据类型
class GreaterFive
{
public:
	bool operator()(int val)
	{
		return val > 5;
	}
};

void test01() {

	vector<int> v;
	for (int i = 0; i < 10; i++) {
		v.push_back(i + 1);
	}

	vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterFive());
	if (it == v.end()) {
		cout << "没有找到!" << endl;
	}
	else {
		cout << "找到大于5的数字:" << *it << endl;
	}
}

//自定义数据类型
class Person {
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
public:
	string m_Name;
	int m_Age;
};

class Greater20
{
public:
	bool operator()(Person &p)
	{
		return p.m_Age > 20;
	}

};

void test02() {

	vector<Person> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);

	vector<Person>::iterator it = find_if(v.begin(), v.end(), Greater20());
	if (it == v.end())
	{
		cout << "没有找到!" << endl;
	}
	else
	{
		cout << "找到姓名:" << it->m_Name << " 年龄: " << it->m_Age << endl;
	}
}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

总结：find_if 按条件查找使查找更加灵活，提供的仿函数可以改变不同的策略

#### 5.2.3 adjacent_find

**功能描述：**

-   查找相邻重复元素

**函数原型：**

- `adjacent_find(iterator beg, iterator end); `

  // 查找相邻重复元素,返回相邻元素的第一个位置的迭代器

  // beg 开始迭代器

  // end 结束迭代器

**示例：**

```C++
#include <algorithm>
#include <vector>

void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(5);
	v.push_back(2);
	v.push_back(4);
	v.push_back(4);
	v.push_back(3);

	//查找相邻重复元素
	vector<int>::iterator it = adjacent_find(v.begin(), v.end());
	if (it == v.end()) {
		cout << "找不到!" << endl;
	}
	else {
		cout << "找到相邻重复元素为:" << *it << endl;
	}
}
```

总结：面试题中如果出现查找相邻重复元素，记得用 STL 中的 adjacent_find 算法

#### 5.2.4 binary_search

**功能描述：**

-   查找指定元素是否存在

**函数原型：**

- `bool binary_search(iterator beg, iterator end, value); `

  // 查找指定的元素，查到 返回 true 否则 false

  // 注意: 在**无序序列中不可用**

  // beg 开始迭代器

  // end 结束迭代器

  // value 查找的元素

**示例：**

```C++
#include <algorithm>
#include <vector>

void test01()
{
	vector<int>v;

	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	//二分查找
	bool ret = binary_search(v.begin(), v.end(),2);
	if (ret)
	{
		cout << "找到了" << endl;
	}
	else
	{
		cout << "未找到" << endl;
	}
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**二分查找法查找效率很高，值得注意的是查找的容器中元素必须的有序序列

#### 5.2.5 count

**功能描述：**

-   统计元素个数

**函数原型：**

- `count(iterator beg, iterator end, value); `

  // 统计元素出现次数

  // beg 开始迭代器

  // end 结束迭代器

  // value 统计的元素

**示例：**

```C++
#include <algorithm>
#include <vector>

//内置数据类型
void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(4);
	v.push_back(5);
	v.push_back(3);
	v.push_back(4);
	v.push_back(4);

	int num = count(v.begin(), v.end(), 4);

	cout << "4的个数为： " << num << endl;
}

//自定义数据类型
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	bool operator==(const Person & p)
	{
		if (this->m_Age == p.m_Age)
		{
			return true;
		}
		else
		{
			return false;
		}
	}
	string m_Name;
	int m_Age;
};

void test02()
{
	vector<Person> v;

	Person p1("刘备", 35);
	Person p2("关羽", 35);
	Person p3("张飞", 35);
	Person p4("赵云", 30);
	Person p5("曹操", 25);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);

    Person p("诸葛亮",35);

	int num = count(v.begin(), v.end(), p);
	cout << "num = " << num << endl;
}
int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

**总结：** 统计自定义数据类型时候，需要配合重载 `operator==`

#### 5.2.6 count_if

**功能描述：**

-   按条件统计元素个数

**函数原型：**

- `count_if(iterator beg, iterator end, _Pred); `

  // 按条件统计元素出现次数

  // beg 开始迭代器

  // end 结束迭代器

  // \_Pred 谓词

**示例：**

```C++
#include <algorithm>
#include <vector>

class Greater4
{
public:
	bool operator()(int val)
	{
		return val >= 4;
	}
};

//内置数据类型
void test01()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(4);
	v.push_back(5);
	v.push_back(3);
	v.push_back(4);
	v.push_back(4);

	int num = count_if(v.begin(), v.end(), Greater4());

	cout << "大于4的个数为： " << num << endl;
}

//自定义数据类型
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

	string m_Name;
	int m_Age;
};

class AgeLess35
{
public:
	bool operator()(const Person &p)
	{
		return p.m_Age < 35;
	}
};
void test02()
{
	vector<Person> v;

	Person p1("刘备", 35);
	Person p2("关羽", 35);
	Person p3("张飞", 35);
	Person p4("赵云", 30);
	Person p5("曹操", 25);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);

	int num = count_if(v.begin(), v.end(), AgeLess35());
	cout << "小于35岁的个数：" << num << endl;
}


int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

**总结：**按值统计用 count，按条件统计用 count_if

### 5.3 常用排序算法

**学习目标：**

-   掌握常用的排序算法

**算法简介：**

-   `sort` //对容器内元素进行排序
-   `random_shuffle` //洗牌 指定范围内的元素随机调整次序
-   `merge ` // 容器元素合并，并存储到另一容器中
-   `reverse` // 反转指定范围的元素

#### 5.3.1 sort

**功能描述：**

-   对容器内元素进行排序

**函数原型：**

- `sort(iterator beg, iterator end, _Pred); `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // \_Pred 谓词

**示例：**

```c++
#include <algorithm>
#include <vector>

void myPrint(int val)
{
	cout << val << " ";
}

void test01() {
	vector<int> v;
	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(20);
	v.push_back(40);

	//sort默认从小到大排序
	sort(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint);
	cout << endl;

	//从大到小排序
	sort(v.begin(), v.end(), greater<int>());
	for_each(v.begin(), v.end(), myPrint);
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**sort 属于开发中最常用的算法之一，需熟练掌握

#### 5.3.2 random_shuffle

**功能描述：**

-   洗牌 指定范围内的元素随机调整次序

**函数原型：**

- `random_shuffle(iterator beg, iterator end); `

  // 指定范围内的元素随机调整次序

  // beg 开始迭代器

  // end 结束迭代器

**示例：**

```c++
#include <algorithm>
#include <vector>
#include <ctime>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	srand((unsigned int)time(NULL));
	vector<int> v;
	for(int i = 0 ; i < 10;i++)
	{
		v.push_back(i);
	}
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//打乱顺序
	random_shuffle(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**random_shuffle 洗牌算法比较实用，使用时记得加随机数种子

#### 5.3.3 merge

**功能描述：**

-   两个容器元素合并，并存储到另一容器中

**函数原型：**

- `merge(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest); `

  // 容器元素合并，并存储到另一容器中

  // 注意: 两个容器必须是**有序的**

  // beg1 容器 1 开始迭代器
  // end1 容器 1 结束迭代器
  // beg2 容器 2 开始迭代器
  // end2 容器 2 结束迭代器
  // dest 目标容器开始迭代器

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10 ; i++)
    {
		v1.push_back(i);
		v2.push_back(i + 1);
	}

	vector<int> vtarget;
	//目标容器需要提前开辟空间
	vtarget.resize(v1.size() + v2.size());
	//合并  需要两个有序序列
	merge(v1.begin(), v1.end(), v2.begin(), v2.end(), vtarget.begin());
	for_each(vtarget.begin(), vtarget.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**merge 合并的两个容器必须的有序序列

#### 5.3.4 reverse

**功能描述：**

-   将容器内元素进行反转

**函数原型：**

- `reverse(iterator beg, iterator end); `

  // 反转指定范围的元素

  // beg 开始迭代器

  // end 结束迭代器

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v;
	v.push_back(10);
	v.push_back(30);
	v.push_back(50);
	v.push_back(20);
	v.push_back(40);

	cout << "反转前： " << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	cout << "反转后： " << endl;

	reverse(v.begin(), v.end());
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**reverse 反转区间内元素，面试题可能涉及到

### 5.4 常用拷贝和替换算法

**学习目标：**

-   掌握常用的拷贝和替换算法

**算法简介：**

-   `copy` // 容器内指定范围的元素拷贝到另一容器中
-   `replace` // 将容器内指定范围的旧元素修改为新元素
-   `replace_if ` // 容器内指定范围满足条件的元素替换为新元素
-   `swap` // 互换两个容器的元素

#### 5.4.1 copy

**功能描述：**

-   容器内指定范围的元素拷贝到另一容器中

**函数原型：**

- `copy(iterator beg, iterator end, iterator dest); `

  // 按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

  // beg 开始迭代器

  // end 结束迭代器

  // dest 目标起始迭代器

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i + 1);
	}
	vector<int> v2;
	v2.resize(v1.size());
	copy(v1.begin(), v1.end(), v2.begin());

	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**利用 copy 算法在拷贝时，目标容器记得提前开辟空间

#### 5.4.2 replace

**功能描述：**

-   将容器内指定范围的旧元素修改为新元素

**函数原型：**

- `replace(iterator beg, iterator end, oldvalue, newvalue); `

  // 将区间内旧元素 替换成 新元素

  // beg 开始迭代器

  // end 结束迭代器

  // oldvalue 旧元素

  // newvalue 新元素

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v;
	v.push_back(20);
	v.push_back(30);
	v.push_back(20);
	v.push_back(40);
	v.push_back(50);
	v.push_back(10);
	v.push_back(20);

	cout << "替换前：" << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//将容器中的20 替换成 2000
	cout << "替换后：" << endl;
	replace(v.begin(), v.end(), 20,2000);
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**replace 会替换区间内满足条件的元素

#### 5.4.3 replace_if

**功能描述:**

-   将区间内满足条件的元素，替换成指定元素

**函数原型：**

- `replace_if(iterator beg, iterator end, _pred, newvalue); `

  // 按条件替换元素，满足条件的替换成指定元素

  // beg 开始迭代器

  // end 结束迭代器

  // \_pred 谓词

  // newvalue 替换的新元素

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

class ReplaceGreater30
{
public:
	bool operator()(int val)
	{
		return val >= 30;
	}

};

void test01()
{
	vector<int> v;
	v.push_back(20);
	v.push_back(30);
	v.push_back(20);
	v.push_back(40);
	v.push_back(50);
	v.push_back(10);
	v.push_back(20);

	cout << "替换前：" << endl;
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;

	//将容器中大于等于的30 替换成 3000
	cout << "替换后：" << endl;
	replace_if(v.begin(), v.end(), ReplaceGreater30(), 3000);
	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**replace_if 按条件查找，可以利用仿函数灵活筛选满足的条件

#### 5.4.4 swap

**功能描述：**

-   互换两个容器的元素

**函数原型：**

- `swap(container c1, container c2); `

  // 互换两个容器的元素

  // c1 容器 1

  // c2 容器 2

**示例：**

```c++
#include <algorithm>
#include <vector>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+100);
	}

	cout << "交换前： " << endl;
	for_each(v1.begin(), v1.end(), myPrint());
	cout << endl;
	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;

	cout << "交换后： " << endl;
	swap(v1, v2);
	for_each(v1.begin(), v1.end(), myPrint());
	cout << endl;
	for_each(v2.begin(), v2.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**swap 交换容器时，注意交换的容器要同种类型

### 5.5 常用算术生成算法

**学习目标：**

-   掌握常用的算术生成算法

**注意：**

-   算术生成算法属于小型算法，使用时包含的头文件为 `#include <numeric>`

**算法简介：**

-   `accumulate` // 计算容器元素累计总和

-   `fill` // 向容器中添加元素

#### 5.5.1 accumulate

**功能描述：**

-   计算区间内 容器元素累计总和

**函数原型：**

- `accumulate(iterator beg, iterator end, value); `

  // 计算容器元素累计总和

  // beg 开始迭代器

  // end 结束迭代器

  // value 起始值

**示例：**

```c++
#include <numeric>
#include <vector>
void test01()
{
	vector<int> v;
	for (int i = 0; i <= 100; i++) {
		v.push_back(i);
	}

	int total = accumulate(v.begin(), v.end(), 0);

	cout << "total = " << total << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**accumulate 使用时头文件注意是 numeric，这个算法很实用

#### 5.5.2 fill

**功能描述：**

-   向容器中填充指定的元素

**函数原型：**

- `fill(iterator beg, iterator end, value); `

  // 向容器中填充元素

  // beg 开始迭代器

  // end 结束迭代器

  // value 填充的值

**示例：**

```c++
#include <numeric>
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{

	vector<int> v;
	v.resize(10);
	//填充
	fill(v.begin(), v.end(), 100);

	for_each(v.begin(), v.end(), myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**利用 fill 可以将容器区间内元素填充为 指定的值

### 5.6 常用集合算法

**学习目标：**

-   掌握常用的集合算法

**算法简介：**

-   `set_intersection` // 求两个容器的交集

-   `set_union` // 求两个容器的并集

-   `set_difference ` // 求两个容器的差集

#### 5.6.1 set_intersection

**功能描述：**

-   求两个容器的交集

**函数原型：**

- `set_intersection(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest); `

  // 求两个集合的交集

  // **注意:两个集合必须是有序序列**

  // beg1 容器 1 开始迭代器
  // end1 容器 1 结束迭代器
  // beg2 容器 2 开始迭代器
  // end2 容器 2 结束迭代器
  // dest 目标容器开始迭代器

**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++)
    {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个里面较小的值给目标容器开辟空间
	vTarget.resize(min(v1.size(), v2.size()));

	//返回目标容器的最后一个元素的迭代器地址
	vector<int>::iterator itEnd =
        set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());

	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**

-   求交集的两个集合必须的有序序列
-   目标容器开辟空间需要从**两个容器中取小值**
-   set_intersection 返回值既是交集中最后一个元素的位置

#### 5.6.2 set_union

**功能描述：**

-   求两个集合的并集

**函数原型：**

- `set_union(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest); `

  // 求两个集合的并集

  // **注意:两个集合必须是有序序列**

  // beg1 容器 1 开始迭代器
  // end1 容器 1 结束迭代器
  // beg2 容器 2 开始迭代器
  // end2 容器 2 结束迭代器
  // dest 目标容器开始迭代器

**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个容器的和给目标容器开辟空间
	vTarget.resize(v1.size() + v2.size());

	//返回目标容器的最后一个元素的迭代器地址
	vector<int>::iterator itEnd =
        set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());

	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**

-   求并集的两个集合必须的有序序列
-   目标容器开辟空间需要**两个容器相加**
-   set_union 返回值既是并集中最后一个元素的位置

#### 5.6.3 set_difference

**功能描述：**

-   求两个集合的差集

**函数原型：**

- `set_difference(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest); `

  // 求两个集合的差集

  // **注意:两个集合必须是有序序列**

  // beg1 容器 1 开始迭代器
  // end1 容器 1 结束迭代器
  // beg2 容器 2 开始迭代器
  // end2 容器 2 结束迭代器
  // dest 目标容器开始迭代器

**示例：**

```C++
#include <vector>
#include <algorithm>

class myPrint
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};

void test01()
{
	vector<int> v1;
	vector<int> v2;
	for (int i = 0; i < 10; i++) {
		v1.push_back(i);
		v2.push_back(i+5);
	}

	vector<int> vTarget;
	//取两个里面较大的值给目标容器开辟空间
	vTarget.resize( max(v1.size() , v2.size()));

	//返回目标容器的最后一个元素的迭代器地址
	cout << "v1与v2的差集为： " << endl;
	vector<int>::iterator itEnd =
        set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), vTarget.begin());
	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;


	cout << "v2与v1的差集为： " << endl;
	itEnd = set_difference(v2.begin(), v2.end(), v1.begin(), v1.end(), vTarget.begin());
	for_each(vTarget.begin(), itEnd, myPrint());
	cout << endl;
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

**总结：**

-   求差集的两个集合必须的有序序列
-   目标容器开辟空间需要从**两个容器取较大值**
-   set_difference 返回值既是差集中最后一个元素的位置