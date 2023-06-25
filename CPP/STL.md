![82104637_p0](https://github.com/XinranSix/docs/assets/62458905/44f91107-3118-4267-acba-6a5c66cd42fd)

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

队列是一种 FIFO 的数据结构。

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

### `list` 容器

STL 中的链表是一个双向循环链表

![image](https://github.com/XinranSix/docs/assets/62458905/6fc56009-08b2-4ca6-95d7-8143e9a1deeb)

由于链表的存储方式并不是连续的内存空间，因此链表 list 中的迭代器只支持前移和后移，属于**双向迭代器**。

`list` 的优点：

-   采用动态存储分配，不会造成内存浪费和溢出
-   链表执行插入和删除操作十分方便，修改指针即可，不需要移动大量元素

`list` 的缺点：

-   链表灵活，但是空间和时间额外耗费较大。

`list` 有一个重要的性质，插入操作和删除操作都不会造成原有 `list` 迭代器的失效。

**list 构造函数：**

|           函数           |                      说明                      | 示例 |
| :----------------------: | :--------------------------------------------: | :--: |
|      `list<T> lst;`      | `list` 采用采用模板类实现，对象的默认构造形式  |      |
|     `list(beg,end);`     | 构造函数将 `[beg, end)` 区间中的元素拷贝给本身 |      |
|     `list(n,elem);`      |        构造函数将 n 个 elem 拷贝给本身         |      |
| `list(const list &lst);` |                  拷贝构造函数                  |      |

**list 赋值和交换：**

|                函数                 |                    说明                    | 示例 |
| :---------------------------------: | :----------------------------------------: | :--: |
|         `assign(beg, end);`         | 将 `[beg, end)` 区间中的数据拷贝赋值给本身 |      |
|         `assign(n, elem);`          |        将 n 个 elem 拷贝赋值给本身         |      |
| `list& operator=(const list &lst);` |               重载等号操作符               |      |
|            `swap(lst);`             |          将 lst 与本身的元素互换           |      |

**list 大小操作：**

|         函数         |                             说明                             | 示例 |
| :------------------: | :----------------------------------------------------------: | :--: |
|      `size();`       |                     返回容器中元素的个数                     |      |
|      `empty();`      |                       判断容器是否为空                       |      |
|    `resize(num);`    | 重新指定容器的长度为 num，若容器变长，则以默认值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |
| `resize(num, elem);` | 重新指定容器的长度为 num，若容器变长，则以 elem 值填充新位置；如果容器变短，则末尾超出容器长度的元素被删除 |      |

**list 插入和删除：**

|           函数           |                       说明                        | 示例 |
| :----------------------: | :-----------------------------------------------: | :--: |
|    `push_back(elem);`    |              在容器尾部加入一个元素               |      |
|      `pop_back();`       |              删除容器中最后一个元素               |      |
|   `push_front(elem);`    |              在容器开头插入一个元素               |      |
|      `pop_front();`      |             从容器开头移除第一个元素              |      |
|   `insert(pos, elem);`   |  在 pos 位置插 elem 元素的拷贝，返回新数据的位置  |      |
| `insert(pos, n, elem);`  |     在 pos 位置插入 n 个 elem 数据，无返回值      |      |
| `insert(pos, beg, end);` | 在 pos 位置插入 `[beg,end)` 区间的数据，无返回值  |      |
|        `clear();`        |                移除容器的所有数据                 |      |
|    `erase(beg, end);`    | 删除 `[beg,end)` 区间的数据，返回下一个数据的位置 |      |
|      `erase(pos);`       |     删除 pos 位置的数据，返回下一个数据的位置     |      |
|     `remove(elem);`      |        删除容器中所有与 elem 值匹配的元素         |      |

**list 数据存取：**

|    函数    |       说明       | 示例 |
| :--------: | :--------------: | :--: |
| `front();` |  返回第一个元素  |      |
| `back();`  | 返回最后一个元素 |      |

> list 容器中不可以通过[]或者 at 方式访问数据。

**list 反转和排序：**

|     函数     |   说明   | 示例 |
| :----------: | :------: | :--: |
| `reverse();` | 反转链表 |      |
|  `sort();`   | 链表排序 |      |

### `set / multiset` 容器

`set`：

- 所有元素都会根据元素的键值自动被排序
- 不允许两个元素有相同的值
- 不可以通过 `set` 的迭代器改变 `set` 元素的值
- `set` 的 `iterator` 是一种 `const_iterator`
- 当对容器中的元素进行插入操作或者删除操作的时候，操作之前所有的迭代器，在操作完成之后依然有效。

`multiset`：特性及用法和 set 完全相同，唯一的差别在于它允许键值重复。

`set` 和 `multiset` 的底层实现是[红黑树](https://zh.wikipedia.org/wiki/%E7%BA%A2%E9%BB%91%E6%A0%91)。

![image](https://github.com/XinranSix/docs/assets/62458905/c3db04d9-0269-432a-8082-a50bbe5807aa)

**set 构造函数：**

|         函数          |     说明     | 示例 |
| :-------------------: | :----------: | :--: |
|     `set<T> st;`      | 默认构造函数 |      |
| `set(const set &st);` | 拷贝构造函数 |      |

**set 赋值和交换操作：**

|               函数               |       说明       | 示例 |
| :------------------------------: | :--------------: | :--: |
| `set& operator=(const set &st);` |  重载等号操作符  |      |
|           `swap(st);`            | 交换两个集合容器 |      |

**set 大小操作：**

|    函数     |         说明         | 示例 |
| :---------: | :------------------: | :--: |
|  `size();`  | 返回容器中元素的数目 |      |
| `empty();`  |   判断容器是否为空   |      |
| `swap(st);` |   交换两个集合容器   |      |

**set 插入和删除操作：**

|        函数        |                           说明                           | 示例 |
| :----------------: | :------------------------------------------------------: | :--: |
|  `insert(elem);`   |                     在容器中插入元素                     |      |
|     `clear();`     |                       清除所有元素                       |      |
|   `erase(pos);`    |    删除 pos 迭代器所指的元素，返回下一个元素的迭代器     |      |
| `erase(beg, end);` | 删除区间 `[beg,end)` 的所有元素 ，返回下一个元素的迭代器 |      |
|   `erase(elem);`   |                删除容器中值为 elem 的元素                |      |

**set 查找和统计：**

|          函数           |                             说明                             | 示例 |
| :---------------------: | :----------------------------------------------------------: | :--: |
|      `find(key);`       | 查找 key 是否存在，若存在，返回该键的元素的迭代器；若不存在，返回 `set.end();` |      |
|      `count(key);`      |                     统计 key 的元素个数                      |      |
| `lower_bound(keyElem);` |             返回第一个 key>=keyElem 元素的迭代器             |      |
| `upper_bound(keyElem);` |            返回第一个 key>keyElem 元素的迭代器。             |      |
| `equal_range(keyElem);` |     返回容器中 key 与 keyElem 相等的上下限的两个迭代器。     |      |

### `pair`

**两种创建方式：**

-   `pair<type, type> p(value1, value2);`
-   `pair<type, type> p = make_pair(value1, value2);`

### `map / multimap` 容器

-   map 中所有元素都是 pair
-   pair 中第一个元素为 key（键值），起到索引作用，第二个元素为 value
-   所有元素都会根据元素的键值自动排序

-   `map / multimap` 属于**关联式容器**，底层结构是用二叉树实现。

**优点：**

-   可以根据 key 值快速找到 value 值

`map` 和 `multimap` **区别**：

-   `map` 不允许容器中有重复 key 值元素
-   `multimap` 允许容器中有重复 key 值元素

**map 构造函数：**

|         函数          |     说明     | 示例 |
| :-------------------: | :----------: | :--: |
|   `map<T1, T2> mp;`   | 默认构造函数 |      |
| `map(const map &mp);` | 拷贝构造函数 |      |

**map 赋值操作：**

|               函数               |      说明      | 示例 |
| :------------------------------: | :------------: | :--: |
| `map& operator=(const map &mp);` | 重载等号操作符 |      |

**map 大小和交换操作：**

|    函数     |         说明         | 示例 |
| :---------: | :------------------: | :--: |
|  `size();`  | 返回容器中元素的数目 |      |
| `empty();`  |   判断容器是否为空   |      |
| `swap(st);` |   交换两个集合容器   |      |

**map 插入数据元素操作：**

|        函数         |                           说明                           | 示例 |
| :-----------------: | :------------------------------------------------------: | :--: |
|   `insert(elem);`   |                     在容器中插入元素                     |      |
| `operator[](elem);` |                     在容器中插入元素                     |      |
|     `clear();`      |                       清除所有元素                       |      |
|    `erase(pos);`    |    删除 pos 迭代器所指的元素，返回下一个元素的迭代器     |      |
| `erase(beg, end);`  | 删除区间 `[beg,end)` 的所有元素 ，返回下一个元素的迭代器 |      |
|    `erase(key);`    |                删除容器中值为 key 的元素                 |      |

**map 查找和统计：**

|          函数           |                             说明                             | 示例 |
| :---------------------: | :----------------------------------------------------------: | :--: |
|      `find(key);`       | 查找 key 是否存在，若存在，返回该键的元素的迭代器；若不存在，返回 `set.end()` |      |
|   `operator[](key);`    | 查找 key 是否存在，若存在，返回该键的元素的迭代器；若不存在，返回 `set.end()` |      |
|      `count(key);`      |                     统计 key 的元素个数                      |      |
| `lower_bound(keyElem);` |             返回第一个 key>=keyElem 元素的迭代器             |      |
| `upper_bound(keyElem);` |      返回容器中 key 与 keyElem 相等的上下限的两个迭代器      |      |

### 总结

![image](https://github.com/XinranSix/docs/assets/62458905/003ac080-8c9e-44b2-b257-dec25f5de084)

![image](https://github.com/XinranSix/docs/assets/62458905/f8665a43-82eb-4b82-a947-233bccaa7151)

## 函数对象

就是重载了 `()` 运算符类的实例。

亦称仿函数。

本质是一个对象，不是一个函数。

根据重载 `operator()` 时的形参个数可分为：一元仿函数、二元仿函数。

函数对象在调用时跟普通函数一样。

函数对象不同于普通函数，函数对象有自己的状态。

函数对象可作为参数传递。

函数对象通常不定义构造函数和析构函数，所以在构造和析构时不会发生任何问题，避免了函数调用的运行时问题。

函数对象可内联编译，性能好，函数指针几乎不可能。

模版函数对象使函数对象具有通用性。

**示例:**

```C++
#include <string>
#include <iostream>

using namespace std;

// 1、函数对象在使用时，可以像普通函数那样调用, 可以有参数，可以有返回值
class MyAdd {
public:
    int operator()(int v1, int v2) { return v1 + v2; }
};

void test01() {
    MyAdd myAdd;
    cout << myAdd(10, 10) << endl;
}

// 2、函数对象可以有自己的状态
class MyPrint {
public:
    MyPrint() { count = 0; }

    void operator()(string test) {
        cout << test << endl;
        count++; // 统计使用次数
    }

    int count; // 内部自己的状态
};

void test02() {
    MyPrint myPrint;
    myPrint("hello world");
    myPrint("hello world");
    myPrint("hello world");
    cout << "myPrint调用次数为： " << myPrint.count << endl;
}

// 3、函数对象可以作为参数传递
void doPrint(MyPrint &mp, string test) { mp(test); }

void test03() {
    MyPrint myPrint;
    doPrint(myPrint, "Hello C++");
}

int main() {

    test01();
    test02();
    test03();

    return 0;
}
```

运行结果：

![image](https://github.com/XinranSix/docs/assets/62458905/c48cbfae-7b10-4b01-952c-be54233c0a2d)

### 谓词

-   返回值类型为 `boo`l 类型的仿函数称为**谓词**
-   如果 `operator()` 接受一个参数，为一元谓词
-   如果 `operator()` 接受两个参数，为二元谓词

 **一元谓词示例：**

```C++
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

// 一元谓词
struct GreaterFive {
    bool operator()(int val) { return val > 5; }
};

int main() {

    vector<int> v;
    for (int i = 0; i < 10; i++) {
        v.push_back(i);
    }

    vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterFive());
    if (it == v.end()) {
        cout << "没找到!" << endl;
    } else {
        cout << "找到:" << *it << endl;
    }

    return 0;
}
```

![image](https://github.com/XinranSix/docs/assets/62458905/82042860-dc78-4360-9d38-10480f0860e7)

**二元谓词示例：**

```C++
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

// 二元谓词
class MyCompare {
public:
    bool operator()(int num1, int num2) { return num1 > num2; }
};

int main() {

    vector<int> v;
    v.push_back(10);
    v.push_back(40);
    v.push_back(20);
    v.push_back(30);
    v.push_back(50);

    // 默认从小到大
    sort(v.begin(), v.end());
    for_each(v.begin(), v.end(), [](int &i) { cout << i << ' '; });
    cout << endl;
    cout << "----------------------------" << endl;

    // 使用函数对象改变算法策略，排序从大到小
    sort(v.begin(), v.end(), MyCompare());
    for_each(v.begin(), v.end(), [](int &i) { cout << i << ' '; });
    cout << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/a9aff19d-0ea7-49e9-b964-f31bbcf1860f)

### 内建函数对象

-   算术仿函数

-   关系仿函数

-   逻辑仿函数

**用法：**

-   这些仿函数所产生的对象，用法和一般函数完全相同
-   使用内建函数对象，需要引入头文件 `#include<functional>`

**算术仿函数**

-   实现四则运算
-   其中 negate 是一元运算，其他都是二元运算

|             仿函数原型              |    说明    |
| :---------------------------------: | :--------: |
|    `template<class T> T plus<T>`    | 加法仿函数 |
|   `template<class T> T minus<T>`    | 减法仿函数 |
| `template<class T> T multiplies<T>` | 乘法仿函数 |
|  `template<class T> T divides<T>`   | 除法仿函数 |
|  `template<class T> T modulus<T>`   | 取模仿函数 |
|   `template<class T> T negate<T>`   | 取反仿函数 |

示例：

```C++
#include <functional>
#include <iostream>

using namespace std;

// negate
void test01() {
    negate<int> n;
    cout << n(50) << endl;
}

// plus
void test02() {
    plus<int> p;
    cout << p(10, 20) << endl;
}

int main() {

    test01();
    test02();

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/277d29fc-ef61-4c1c-af40-d4a2cb676650)

**关系仿函数：**

|                仿函数原型                 |   说明   |
| :---------------------------------------: | :------: |
|   `template<class T> bool equal_to<T>`    |   等于   |
| `template<class T> bool not_equal_to<T>`  |  不等于  |
|    `template<class T> bool greater<T>`    |   大于   |
| `template<class T> bool greater_equal<T>` | 大于等于 |
|     `template<class T> bool less<T>`      |   小于   |
|   template<class T> bool less_equal<T>`   | 小于等于 |

示例：

```C++
#include <functional>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int main() {

    vector<int> v{10, 30, 50, 20, 20};

    for_each(v.begin(), v.end(), [](int &i) { cout << i << ' '; });
    cout << endl;

    sort(v.begin(), v.end(), greater<int>());

    for_each(v.begin(), v.end(), [](int &i) { cout << i << ' '; });
    cout << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/d2ce0b9f-1791-4eb2-9fe4-59ee568092f5)

**逻辑仿函数：**

逻辑运算类运算函数，`not` 为一元运算，其余为二元运算。

|               仿函数原型                |  说明  |
| :-------------------------------------: | :----: |
| `template<class T> bool logical_and<T>` | 逻辑与 |
| `template<class T> bool logical_or<T>`  | 逻辑或 |
| `template<class T> bool logical_not<T>` | 逻辑非 |

示例：

```C++
#include <vector>
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std;

int main() {

    vector<bool> v{true, false, true, false};

    for_each(v.begin(), v.end(), [](const bool &b) { cout << b << ' '; });
    cout << endl;

    // 逻辑非  将v容器搬运到v2中，并执行逻辑非运算
    vector<bool> v2;
    v2.resize(v.size());
    transform(v.begin(), v.end(), v2.begin(), logical_not<bool>());

    for_each(v2.begin(), v2.end(), [](const bool &b) { cout << b << ' '; });
    cout << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/9d50a19b-9eb0-4b86-a91f-29dd562a9586)

## 适配器

用来适配参数，扩展参数接口，一般结合仿函数一起使用。

### 函数对象适配器

示例：

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

// 一元继承public unary_function<参数1 ,返回值类型>
// 二元继承public binary_function<int,int,void>
class Print : public binary_function<int, int, void> {
public:
    void operator()(int a, int num) const {
        cout << a << " " << num << endl;
        cout << a + num << endl;
    }
};

int main() {

    vector<int> v{1, 2, 3, 4};

    // 绑定参数 bind2nd
    for_each(v.begin(), v.end(), bind2nd(Print(), 200));

    cout << endl;
    
    // bind1st
    for_each(v.begin(), v.end(), bind1st(Print(), 200));

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/bc636f64-cd86-4c91-9786-ae5067b13651)

### 取反适配器

示例：

```cpp
#include <iostream>
#include <vector>
#include <functional>

using namespace std;

int main() {
    vector<int> v{1, 4, 2, 3, 5};

    // not1 一元取反
    // not2 二元取反
    // vector<int>::iterator it = find_if(v.begin(),v.end(), not1(greater2()));
    vector<int>::iterator it =
        find_if(v.begin(), v.end(), not1(bind2nd(greater<int>(), 2)));

    if (it != v.end()) {
        cout << *it << endl;
    }

    sort(v.begin(), v.end(), not2(greater<int>()));
    for_each(v.begin(), v.end(), [](const int &a) { cout << a << ' '; });

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/127acbc6-70b3-4143-900a-9ee582f3d4e9)

### 函数指针适配器

将函数指针适配成函数对象。

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

void print(int a, int num) { cout << a + num << endl; }

int main() {
    vector<int> v{1, 4, 2, 3, 5};

    // 需要将函数指针print适配成函数对象
    // ptr_fun 将函数指针适配成函数对象
    for_each(v.begin(), v.end(), bind2nd(ptr_fun(print), 200));
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/af1de132-03f0-41c0-aa99-a6e0fdd293d8)

### 成员函数适配器

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

class Person {
public:
    Person(string name, int age) {
        m_Name = name;
        m_Age = age;
    }

    // 打印函数
    void ShowPerson() {
        cout << "成员函数:"
             << "Name:" << m_Name << " Age:" << m_Age << endl;
    }
    void Plus100() { m_Age += 100; }

public:
    string m_Name;
    int m_Age;
};

void test01() {
    vector<Person *> v1;
    // 创建数据
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);

    v1.push_back(&p1);
    v1.push_back(&p2);
    v1.push_back(&p3);
    v1.push_back(&p4);

    for_each(v1.begin(), v1.end(), mem_fun(&Person::ShowPerson));
}

void test02() {
    vector<Person> v;
    Person p1("aaa", 10);
    Person p2("bbb", 20);
    Person p3("ccc", 30);
    Person p4("ddd", 40);
    v.push_back(p1);
    v.push_back(p2);
    v.push_back(p3);
    v.push_back(p4);
    // mem_fun_ref 将Person的成员函数适配成 普通回调函数
    for_each(v.begin(), v.end(), mem_fun_ref(&Person::ShowPerson));
}

int main() {
    test01();
    cout << endl;
    test02();
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/69eff3b3-029c-4124-b556-f2f71a8466b9)

## 常用算法

-   算法主要是由头文件 `<algorithm>`、 `<functional>`、 `<numeric>` 组成。

-   `<algorithm>` 是所有 STL 头文件中最大的一个，范围涉及到比较、 交换、查找、遍历操作、复制、修改等等。
-   `<numeric>` 体积很小，只包括几个在序列上面进行简单数学运算的模板函数。
-   `<functional>` 定义了一些模板类，用以声明函数对象。

### 常用遍历算法

|                             算法                             |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|      `for_each(iterator beg, iterator end, _callback);`      | 遍历算法<br />`beg`：开始迭代器<br />`end`：结束迭代器<br />`callback`：回调函数或函数对象<br />返回值：函数对象，即 `callback` 参数指向的函数对象 |
| `transform(iterator beg1, iterator end1, iterator beg2, _callbakc);` | 将指定容器区间元素搬运到另一容器中<br />`beg1`：源容器开始迭代器<br />`end1`：源容器结束迭代器<br />`beg2`：目标容器开始迭代器<br />`_callbakc`：回调函数或函数对象<br />返回值：返回目标容器迭代器 |

示例：

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

int main() {
    vector<int> v{1, 2, 3, 4};

    vector<int> v1;

    v1.resize(v.size());

    transform(v.begin(), v.end(), v1.begin(), [](const int &a) { return a; });

    for_each(v1.begin(), v1.end(), [](const int &a) { cout << a << endl; });
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/9ee06748-2504-4d1c-9e2b-18c1988de2fa)

### 常用查找算法

|                           算法                           |                             说明                             |
| :------------------------------------------------------: | :----------------------------------------------------------: |
|        `find(iterator beg, iterator end, value);`        | 查找元素<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`value`：查找的元素<br />返回值：返回查找元素的位置 |
|    `find_if(iterator beg, iterator end, _callback);`     | 按条件查找元素<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`callback`：回调函数或者谓词<br />返回值：找到返回 `true`，否则 `false` |
| `adjacent_find(iterator beg, iterator end, _callback);`  | 查找相邻重复元素<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`_callback`：回调函数或者谓词<br />返回值：返回相邻元素的第一个位置的迭代器 |
| `bool binary_search(iterator beg, iterator end, value);` | 二分查找法<br />注意：在无序序列中不可用<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`value`：查找的元素<br />返回值：找到返回 `true`，否则 `false` |
|       `count(iterator beg, iterator end, value);`        | 统计元素个数<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`value`：统计的元素<br />返回值：返回元素个数 |
|    `count_if(iterator beg, iterator end, _callback);`    | 统计元素个数按条件统计元素个数<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`_callback`：回调函数或者谓词<br />返回值：返回元素个数 |

**示例：**

```cpp
#include <iostream>
#include <string.h>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

class compare {
public:
    bool operator()(int a, int b) { return a % 2 == 1 && b % 2 == 1; }
};

int main() {

    vector<int> v{1, 2, 2, 3, 3, 4, 4};

    for_each(v.begin(), v.end(), [](int a) { cout << a << " "; });

    vector<int>::iterator it = find(v.begin(), v.end(), 3);
    if (it != v.end()) {
        cout << *it << endl;
    }

    it = adjacent_find(v.begin(), v.end(), compare());

    if (it != v.end()) {
        cout << *it << endl;
    }

    if (binary_search(v.begin(), v.end(), 3))
        cout << "找到了" << endl;

    int n = count(v.begin(), v.end(), 4);
    cout << n << endl;

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/87eaeef8-e174-44b5-b0e4-14c4b8cba7cc)

### 常用排序算法

|                             算法                             |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| `merge(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);` | 容器元素合并，并存储到另一容器中<br />注意：两个容器必须是有序的<br />`beg1`：容器 1 开始迭代器<br />`end1`：容器 1 结束迭代器<br />`beg2`：容器 2 开始迭代器<br />`end2`：容器 2 结束迭代器<br />`dest`：目标容器开始迭代器 |
|        `sort(iterator beg, iterator end, _callback);`        | 容器元素排序<br />`beg`：容器 1 开始迭代器<br />`end`：容器 1 结束迭代器<br />`_callback`：回调函数或者谓词 |
|        `random_shuffle(iterator beg, iterator end);`         | 对指定范围内的元素随机调整次序<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器 |
|            `reverse(iterator beg, iterator end);`            | 反转指定范围的元素<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器 |

**示例：**

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

void test01() {
    vector<int> v{1, 2, 3, 4};
    vector<int> v1{3, 4, 5};

    vector<int> v2;

    v2.resize(v.size() + v1.size());
    merge(v.begin(), v.end(), v1.begin(), v1.end(), v2.begin());

    for_each(v2.begin(), v2.end(), [](int a) { cout << a << " "; });
}

void test02() {
    vector<int> v{1, 2, 3, 4};

    // random_shuffle(v.begin(),v.end());
    reverse(v.begin(), v.end());
    for_each(v.begin(), v.end(), [](int a) { cout << a << " "; });
}
int main() {
    test01();
    cout << endl;
    test02();
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/1aaa134a-0a60-465c-bf63-92c42e0723ba)

### 常用拷贝和替换算法

|                             算法                             |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|      `copy(iterator beg, iterator end, iterator dest);`      | 将容器内指定范围的元素拷贝到另一容器中<br />beg：容器开始迭代器<br />end：容器结束迭代器<br />dest：目标起始迭代器 |
|  `replace(iterator beg, iterator end, oldvalue, newvalue);`  | 将容器内指定范围的旧元素修改为新元素<br />beg：容器开始迭代器<br />end：容器结束迭代器<br />oldvalue：旧元素<br /> newvalue：新元素 |
| `replace_if(iterator beg, iterator end, _callback, newvalue);` | 将容器内指定范围满足条件的元素替换为新元素<br />`beg`：容器开始迭代器<br />`end`：容器结束迭代器<br />`callback`：函数回调或者谓词<br />`newvalue`：新元素 |
|             `swap(container c1, container c2);`              |   互换两个容器的元素<br /> `c1`：容器 1<br /> `c1`：容器 2   |

**示例：**

```cpp
#include <iostream>
#include <string.h>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>
#include <numeric>

using namespace std;

class greater10 {
public:
    bool operator()(int a) { return a > 2; }
};

int main() {

    vector<int> v{1, 2, 3, 4};

    vector<int> v2;
    v2.resize(v.size());
    // copy(v.begin(),v.end(),v2.begin());
    // replace(v.begin(), v.end(), 3, 10);
    replace_if(v.begin(), v.end(), greater10(), 10);
    for_each(v.begin(), v.end(), [](int a) { cout << a << " "; });
    cout << endl;

    swap(v, v2);
    for_each(v.begin(), v.end(), [](int a) { cout << a << " "; });
    cout << endl;
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/e7e7c18a-4042-45a0-af61-4b69cb2bc2d3)

### 常用算术生成算法

|                       算法                       |                             说明                             |
| :----------------------------------------------: | :----------------------------------------------------------: |
| `accumulate(iterator beg, iterator end, value);` | 计算容器元素累计总和<br />`beg`：容器开始迭代器<br /> `end`：容器结束迭代器<br />`value`：起始值 |
|    `fill(iterator beg, iterator end, value);`    | 向容器中添加元素<br />`beg`：容器开始迭代器<br /> `end`：容器结束迭代器<br />`value`：填充元素 |

**示例：**

```cpp
#include <iostream>
#include <string.h>
#include <string>
#include <vector>
#include <algorithm>
#include <functional>
#include <numeric>

using namespace std;

int main() {
    vector<int> v{1, 2, 3, 4};

    int num = accumulate(v.begin(), v.end(), 100);
    cout << num << endl;

    fill(v.begin() + 2, v.end(), 20);
    for_each(v.begin(), v.end(), [](int a) { cout << a << " "; });

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/e0d8973f-3518-4031-b2db-3d1e2aedb4a0)

### 常用集合算法

|                             算法                             |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| `set_intersection(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);` | 求两个 set 的交集<br />`beg1`：容器 1 开始迭代器<br />`end1`：容器 1 结束迭代器<br />`beg2`：容器 2 开始迭代器<br />`end2`：容器 2 结束迭代器<br />`dest` 目标容器开始迭代器<br />返回值：目标容器的最后一个元素的迭代器地址 |
| `set_union(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);` | 求两个 set 的并集<br />`beg1`：容器 1 开始迭代器<br />`end1`：容器 1 结束迭代器<br />`beg2`：容器 2 开始迭代器<br />`end2`：容器 2 结束迭代器<br />`dest`：目标容器开始迭代器<br />返回值：目标容器的最后一个元素的迭代器地址 |
| `set_difference(iterator beg1, iterator end1, iterator beg2, iterator end2, iterator dest);` | 求两个 set 的差集<br />`beg1`：容器 1 开始迭代器<br />`end1`：容器 1 结束迭代器<br />`beg2`：容器2 开始迭代器<br />`end2`：容器 2 结束迭代器<br />`dest`：目标容器开始迭代器<br />返回值：目标容器的最后一个元素的迭代器地址 |

**示例：**

```cpp
#include <iostream>
#include <vector>
#include <functional>

using namespace std;

int main() {
    vector<int> v{1, 2, 3, 4};

    vector<int> v1{3, 4, 5, 6};

    vector<int> v2;
    v2.resize(v.size() + v1.size());

    set_intersection(v.begin(), v.end(), v1.begin(), v1.end(), v2.begin());
    for_each(v2.begin(), v2.end(), [](int a) { cout << a << " "; });
    cout << endl;

    set_union(v.begin(), v.end(), v1.begin(), v1.end(), v2.begin());
    for_each(v2.begin(), v2.end(), [](int a) { cout << a << " "; });
    cout << endl;

    v2.clear();
    v2.resize(v.size());
    set_difference(v.begin(), v.end(), v1.begin(), v1.end(), v2.begin());
    for_each(v2.begin(), v2.end(), [](int a) { cout << a << " "; });

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/docs/assets/62458905/15d21458-3f7c-46c9-8a43-d23b1d62c122)

> 1. 求交目标容器开辟空间需要从**两个容器中取小值**
> 2. 求并目标容器开辟空间需要**两个容器相加**
> 3. 求差目标容器开辟空间需要从**两个容器取较大值**


