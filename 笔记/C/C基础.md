## 第一个 C 语言程序

```c
#include <stdio.h> //头文件

int main() {
    printf("Hello World!\n"); // 使用printf函数输出括号里面的字符串
    return 0;
}
```

## 关键字

### 数据类型相关的关键字

|   关键字   |                             说明                             |                           数据范围                           |
| :--------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   `char`   |               用来定义字符型变量，占 1 个字节                |    有符号：$-2^{7}\sim2^7-1$<br />无符号：$0 \sim 2^8-1$     |
|  `short`   |               用来定义短整型变量，占 2 个字节                | 有符号：$-2^{15}\sim2^{15}-1$<br />无符号：$0 \sim 2^{16}-1$ |
|   `int`    |                用来定义整型变量，占 4 个字节                 | 有符号：$-2^{31}\sim2^{31}-1$<br />无符号：$0 \sim 2^{32}-1$ |
|   `long`   | 用来定义长整型变量，在 32 位操作系统下占 4 个字节，在 64 位操作系统下占 8 个字节 |                                                              |
|  `double`  |             用来定义单精度浮点类型，占 4 个字节              |                                                              |
|  `float`   | 用来定义双精度浮点类型，占 8 个字节，在 32 位操作系统上由两个 4 字节组成 |                                                              |
|  `struct`  |                    用来定义结构体的关键字                    |                                                              |
|  `union`   |                    用来定义共用体的关键字                    |                                                              |
|   `enum`   |                     用来定义枚举的关键字                     |                                                              |
|  `signed`  | 表示有符号数，用来修饰 `short`、`int`、`long`，默认情况下整形都是有符号数，无需带上此关键字 |                                                              |
| `unsigned` |        表示无符号数，用来修饰 `short`、`int`、`long`         |                                                              |
|   `void`   | 空类型关键字，可以用来修饰函数返回值、声明万能指针（`void *`） |                                                              |

测试数据类型所占内存大小：

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    char a;
    short b;
    int c;
    long d;
    float e;
    double f;

    printf("%lld\n", sizeof(a));
    printf("%lld\n", sizeof(b));
    printf("%lld\n", sizeof(c));
    printf("%lld\n", sizeof(d));
    printf("%lld\n", sizeof(e));
    printf("%lld\n", sizeof(f));
    
    return 0;
}
```

输出如下：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/6b55d317-594d-41c8-b1f1-5070692ffada)

#### 存储相关关键字

存储相关关键字有：`register`、`static`、`auto`、`extern`.

#### register

`register` 是寄存器的意思，用 `register` 修饰的变量是寄存器变量，即：在编译的时候告诉编译器这个变量是寄存器变量，尽量将其存储空间分配在寄存器中。

注意：

1. 定义的变量不一定真的存放在寄存器中。
2. CPU 取数据的时候去寄存器中拿数据比去内存中拿数据要快。
3. 因为寄存器比较宝贵，所以不能定义寄存器数组。
4. `register` 只能修饰字符型及整型的，不能修饰浮点型。
5. 因为 `register` 修饰的变量可能存放在寄存器中不存放在内存中，所以不能对寄存器变量取地址，因为只有存放在内存中的数据才有地址。

#### static

`static` 可以修饰全局变量、局部变量、函数，使用 `static` 修饰的变量保存在内存的静态区空间中。

#### const

用 `const` 修饰的变量是只读的，不能修改它的值。

#### auto

`auto int a`; 和 `int a;` 是等价的，`auto` 关键字现在基本不用。

#### extern

是外部的意思，一般用于函数和全局变量的声明。

### 控制语句相关的关键字

`if` 、`else` 、`break`、`continue`、`for` 、`while`、`do`、`switch`、`case`、`goto`、`default`.

### 其他关键字

`sizeof`、`typedef`、`volatile`.

#### sizeof

使用来测变量、数据类型、数组的占用存储空间的大小（字节数）。

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int a = 10;
    printf("%lld\n", sizeof(a));
    printf("%lld\n", sizeof(double));
    return 0;
}
```

输出如下：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/89177b85-9d3f-4105-9734-edbfa0bf45ea)

#### typedef

给一个已有的类型重新起个类型名，没有创造一个新的类型。

语法：

```c
typedef old_type_name new_type_name
```

例如：

```c
typedef short int INT16;
```

`INT16` 就和 `short int` 是等价的。

#### volatile

用 `volatile` 定义的变量，是易改变的，即告诉 CPU 每次用 `volatile` 变量的时候，重新去内存中读取，保证用的是最新的值，而不是寄存器中的备份。

`volatile` 关键字现在较少适用。

## 数据类型

### 基本类型

`char`、`short`、`int`、`long`、`float`、`double`.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    char a = 'w';
    printf("a = %c\n", a);
    short b = 100;
    printf("b = %d\n", b);
    int c = 9999;
    printf("c = %d\n", c);
    long d = 34536453;
    printf("d = %ld\n", d);
    float e = 3.1415926;
    printf("e = %f\n", e);
    double f = 3452.2345324523452;
    printf("f = %lf\n", f);

    return 0;
}
```

输出如下：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/e4ecc5cd-3da4-4a0d-a2b1-31877af0b8aa)

### 构造类型

由若干个相同或不同类型数据构成的集合，包括：数组、结构体、共用体、枚举。

### 常量和变量

#### 常量

在程序运行过程中，其值不可以改变的量。

例：`100`、`'a'`、`"hello"`.

常量的分类：

- 整型：`100`，`125`，`-100`，`0`
- 实型：`3.14`、`0.125f`、`-3.789`
- 字符型：'a'、`b`、`2`
- 字符串：`"a"`、`"ab"`、`"1232"`

ASCII 码表：对于计算机而言，只能识别二进制数，也就是数字，对于非数值型数据，如果要使用，就需要将其用一个数值型数据进行标识，描述这种映射关系的就是 [ASCII 码表](http://c.biancheng.net/c/ascii/)。

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    char ch1 = 'w';
    printf("ch1 = %c %d\n", ch1, ch1);
    char ch2 = 97;
    printf("ch2 = %c %d\n", ch2, ch2);
    return 0;
}
```

输出如下：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/2eeaec89-9366-46cd-9201-79d91b8d74fd)

#### 变量

值可以改变的量被称为变量。

定义方式：

```c
存储类型 数据类型 变量名;
存储类型 数据类型 变量名 = 变量或者常量;
```

变量在定义的时候要满足标识符的命名规则：

1. 只能由字母、数字和下划线组成。
2. 首字母不能是数字。
3. 不能是关键字。

整型：

- 整型常量:（按进制分）

  - 十进制： 以正常数字 1- 9 开头，如 `457`、`789`.

  - 八进制：以数字 0 开头，如 `0123`.
  - 十六进制：以 0x 开头，如 `0x1e`.

- 整型变量：

  - 短整型：2 个字节。
  - 整型：4 个字节，
  - 长整型：32 位平台上位 4 个字节。

实型（浮点型）：

- 实型常量：实型常量也称为实数或者浮点数，不以 f 结尾的常量是 `double` 类型，以 f 结尾的常量（如 `3.14f`）是 `float` 类型。
  - 十进制形式：由数字和小数点组成：`0.0`、`0.12`、`5.0`.
  - 指数形式：`123e3` 代表 ${123}\times {10}^3$，`123e-3`代表 ${123}\times {10}^{-3}$. 
- 实型变量：
  - f`loat` 型：占 4 字节，7 位有效数字，指数 -37 到 38.
  - double 型：占 8 字节，16 位有效数字，指数 -307 到 308.

字符数据：

- 字符常量：
  - 直接常量：用单引号括起，如：`'a'`、`'b'`、`'0'`等。
  - 转义字符：以反斜杠 `\` 开头，后跟一个或几个字符、如 `'\n'`、`\t` 等，分别代表换行、制表符。

- 字符变量：用 char 定义，每个字符变量被分配一个字节的内存空间字符值以 ASCII 码的形式存放在变量的内存单元中。

字符串常量：

是由双引号括起来的字符序列，如：`"CHINA"`、`"哈哈哈"`、`"C program"`，`"$12.5"` 等都是合法的字符串常量。

> 字符串常量与字符常量的不同：`'a'` 为字符常量，`"a"` 为字符串常量，每个字符串的结尾，编译器会为其自动添加一个结束标志位 `\0`，即字符串 `"a"` 包含两个字符：`a` 和 '\0'.

### 格式化输出字符串

| 格式符 |            说明            |
| :----: | :------------------------: |
|  `%d`  |      十进制有符号整数      |
| `%ld`  | 十进制 `long` 型有符号整数 |
|  `%u`  |      十进制无符号整数      |
|  `%o`  |     以八进制表示的整数     |
|  `%x`  |    以十六进制表示的整数    |
|  `%f`  |      `float` 型浮点数      |
| `%lf`  |     `double` 型浮点数      |
|  `%e`  |      指数形式的浮点数      |
|  `%c`  |          单个字符          |
|  `%s`  |           字符串           |
|  `%p`  |          指针的值          |



```c
#include <stdio.h>

// 格式化输出字符的使用

int main(int argc, char *argv[]) {
    // 输出整数
    int a = 100;
    // 输出十进制数，用%d
    printf("a = %d\n", a);
    // 输出八进制数，用%o
    // printf("a = %o\n", a);
    // 使用%#o，可以输出八进制数的前导符
    printf("a = %#o\n", a);
    // 输出十六进制数
    // printf("a = %x\n", a);
    //  使用%#x，可以输出十六进制数的前导符
    printf("a = %#x\n", a);
    // 输出浮点型数据,float使用%f，double使用%lf
    // 默认小数点后保留六位，并且可以四舍五入，如果不够六位自动补0
    float b = 3.1415926;
    double c = 2345.2345;
    printf("b = %f\n", b);
    printf("c = %lf\n", c);
    // 输出字符，使用%c输出字符，使用%d可以输出字符的ascii码值
    char d = 'y';
    printf("d = %c %d\n", d, d);
    // 输出字符串，使用%s
    // 没有专门的变量保存字符串，一般使用数组来保存
    char e[] = "hello world";
    printf("e = %s\n", e);
    // 输出地址，使用%p
    int f = 999;
    //&：取一个变量的地址，一般地址用十六进制数标识
    printf("&f = %p\n", &f);
    return 0;
}

```

输出为：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/0730882c-0318-4ab1-a78d-3bfde5f2b1af)

- `%3d`：要求宽度为 3 位，如果不足 3 位，前面空格补齐；如果足够 3 位，此语句无效。
- `%03d`：要求宽度为 3 位，如果不足 3 位，前面 0 补齐；如果足够 3 位，此语句无效。
- `%-3d`：要求宽度为 3 位，如果不足 3 位，后面空格补齐；如果足够 3 位，此语句无效。
- `%.2f`：小数点后只保留 2 位。

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int m = 456;
    printf("%d%d\n", m, m);
    printf("%5d%5d\n", m, m);
    printf("%05d%05d\n", m, m);
    printf("%-5d%-5d\n", m, m);
    float n = 3.678;
    printf("n = %f\n", n);
    printf("n = %.2f\n", n);
    
    return 0;
}

```

输出为：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/8d43328e-ce79-4fa2-8111-225cab0c19dc)

### 类型转换

数据有不同的类型，不同类型数据之间进行混合运算时必然涉及到类型的转换问题。

转换的方法有两种：

- 自动转换：遵循一定的规则，由编译系统自动完成。
- 强制类型转换：把表达式的运算结果强制转换成所需的数据类型。

#### 自动转换

自动转换原则

1. 占用内存字节数少的类型，向占用内存字节数多的类型转换，以保证精度不降低。
2. 转换方向：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/d1ce4c8d-9328-4aa6-a606-ff6e918efcb0)

#### 强制转换

通过类型转换运算来实现，语法：

```c
(类型名) (表达式)
```

功能：把表达式的运算结果强制转换成类型说明符所表示的类型。

例如：

```c
(float) a;
(int) (x + y);
```

注意：类型名必须加括号。

#### 案例：

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    printf("%d\n", 5 / 2);
    printf("%lf\n", 5.0 / 2);
    int a = -8;
    unsigned int b = 7;
    if (a + b > 0) {
        printf("a+b>0\n");
    } else {
        printf("a+b<=0\n");
    }
    int m;
    float n = 5.8f;
    m = n;
    printf("m = %d\n", m);
    printf("n = %f\n", n);
    int x = 10;
    int y = 4;
    float w;
    w = (float)x / (float)y;
    printf("w = %f\n", w);

    return 0;
}
```

输出为：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/af098cf9-c45d-4897-a1d8-cafd9423cc36)

## 运算符

### 算术运算符

`+`、`-`、`*`、`/`、`%`、`+=`、`-=`、`*=`、`/=`、`%=`.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int a = 40;
    int b = 6;

    printf("%d + %d = %d\n", a, b, a + b);
    printf("%d - %d = %d\n", a, b, a - b);
    printf("%d * %d = %d\n", a, b, a * b);
    printf("%d / %d = %d\n", a, b, a / b);
    printf("%d %% %d = %d\n", a, b, a % b);

    float m = 10.32;
    float n = 4.5;

    printf("%.4f + %.4f = %.4f\n", m, n, m + n);
    printf("%.4f - %.4f = %.4f\n", m, n, m - n);
    printf("%.4f * %.4f = %.4f\n", m, n, m * n);
    printf("%.4f / %.4f = %.4f\n", m, n, m / n);

    return 0;
}

```

输出为：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/31aae51d-3a09-4f54-a860-7bdc44cb0198)

### 关系运算符

`>`、`<`、`==`、`>=`、`<=`、`!=`.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int a = 10 > 5;
    int b = 10 < 5;

    printf("a = %d, b = %d\n", a, b);

    return 0;
}

```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/e2fe18b3-46de-410d-b32e-668543432de0)

### 逻辑运算符

`&&`、`||`、`!`.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int a = 20;
    int ret = a > 10 && a < 19;
    printf("ret = %d\n", ret);
    ret = a > 10 || a < 19;
    printf("ret = %d\n", ret);

    int b = 100;
    ret = (a < 19) && (b += 10);
    printf("b = %d\n", b);

    ret = (a > 19) || (b += 10);
    printf("b = %d\n", b);
    
    return 0;
}
```

输出为：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/a8e3f10a-e346-41d0-aa96-e728d1f0d880)

> 注意逻辑运算符存在短路现象。

### 位运算符

`&`：任何值与 0 得 0，与 1 保持不变

```
0101 1011
1011 0100
0001 0000
```

`|`：任何值或 1 得 1，或 0 保持不变

```
0101 0011
1011 0100
1111 0111
```

`~`：1 变 0，0 变 1

```
0101 1101
1010 0010
```

`^`：相异得 1，相同得 0

```
1001 1100
0101 1010
1100 0110
```

`>>`：右移

高位溢出，低位补 0

`<<`：左移

> 注意右移分：逻辑右移、算数右移。

逻辑右移：高位补 0，低位溢出。

算数右移：高位补符号位，低位溢出。

在一个编译系统中到底是逻辑右移动，还是算数右移，取决于编译器。

```c
// 判断右移是逻辑右移还是算数右移
#include <stdio.h>

int main(int argc, char *argv[]) {

    printf("%d\n", -1 >> 3);

    return 0;
}
// 如果结果还是‐1 证明是算数右移
```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/032c6576-78dd-4ec9-8fba-d268e650f918)

### 条件运算符号

语法：

```c
(表达式 A) ? (表达式 B) : (表达式 C)
```

相对于：

```	c
if (A) {
    B;
} else {
    C;
}
```

例如：

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int a = 10, b = 20;
    int c;
    c = (a > b) ? (a += 10) : (b += 10);
    printf("c = %d\n", c);
    printf("a = %d, b = %d\n", a, b);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/83689588-d49c-4fe6-ad02-d8292a5955d1)

### 逗号运算符

语法：

```c
(表达 A, 表达式 B, 表达式 C, ...)
```

例如：

```c
A = (B, C, D);
```

先运行表达式 B，再运行表达式 C，最后运行表达式 D，最终变量 A 的值为表达式 D 的值。

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int a = 10, b = 20;
    int c;
    c = (a += 10, b += 10, a += b);
    printf("a = %d, b = %d, c = %d\n", a, b, c);
    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/6bbaa575-b203-40dc-90cf-b85a9975bcb1)

### 自增自减运算符

`++`、`--`

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int a = 100;
    int b;
    b = a++;
    printf("a = %d, b = %d\n", a, b);

    a = 100;
    b = ++a;
    printf("a = %d, b = %d\n", a, b);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/00b4d8b3-0496-42b9-a1b5-6d4f7f359893)

### 运算符优先级表

[C 语言运算符优先级和结合性一览表](http://c.biancheng.net/view/161.html)

## 控制语句

### 选择控制语句

#### if 语句

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int n = 40;

    if (n > 50) {
        printf("%d > 50\n", n);
    } else if (n == 50) {
        printf("%d = 50\n", n);
    } else {
        printf("%d < 50\n", n);
    }
    
    return 0;
}
```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/104075a5-01ea-442f-b33c-6ed91aebc32d)

#### switch 语句

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int num = 2;

    switch (num) {
    case 1:
        printf("111111111111\n");

        break;
    case 2:
        printf("222222222222\n");
        break;
    case 3:
        printf("333333333333\n");
        break;
    default:
        printf("hahahahahaha\n");
        break;
    }

    return 0;
}

```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/52ed46eb-d44c-47b1-ae8e-bd7d120a2fd9)

运行顺序：将常量表达式的值语句 switch 后面的表达式的值对比，如果表达式的值刚好等于 case 后面的某一个值，就会立即去执行 case 后的语句，如果都不是，则会执行 default 后面的语句。

注意事项：

1. switch 后面的表达式不能是浮点型，只能是整形的。
2. 如果 case 后面的常量表达式与 switch 的表达式的值都不同，则执行 default 后面的语句。
3. 每一个 case 执行结束后理论上必须跟一个 break，作用就是跳出整个 switch.
4. case 后面如果语句很多，不需要加大括号。

### 循环控制语句

#### for 循环

使用 for 循环求 1 到 100 的累加和：

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int sum = 0;

    for (int i = 1; i <= 100; i++) {
        sum += i;
    }

    printf("1 + 2 + 3 + ... + 100 = %d\n", sum);

    return 0;
}
```

输出结果：

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/3d008b67-abf2-4cc5-a1d8-39f5f7ba6f22)

#### while 循环

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int i = 1;
    int sum = 0;

    while (i <= 100) {
        sum += i;
        i++;
    }

    printf("1 + 2 + 3 + ... + 100 = %d\n", sum);

    return 0;
}
```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/7133b3c2-d601-4897-8b10-fb3e6d8ab331)

#### do while 循环

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    int i = 1;
    int sum = 0;

    do {
        sum += (i++);
    } while (i <= 100);

    printf("1 + 2 + 3 + ... + 100 = %d\n", sum);

    return 0;
}
```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/79006d13-e08c-4a83-bdf1-74ffdfda3648)

> do while 至少执行一次循环体。

#### goto

goto 主要用于在一个函数里面实现代码的跳转。

```c
#include <stdio.h>

int main(int argc, char *argv[]) {

    printf("11111111111111\n");
    goto NEXT;
    printf("22222222222222\n");
    printf("33333333333333\n");
NEXT:
    printf("44444444444444\n");
    printf("hello world\n");

    return 0;
}
```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/027264d2-9b5e-48fb-acc0-dc4dd353f299)

使用 goto 实现求 1 到 100 的累加和：

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int i = 1;
    int sum = 0;

JOOP:
    sum += i;
    i++;
    if (i <= 100) {
        goto JOOP;
    }

    printf("1 + 2 + 3 + ... + 100 = %d\n", sum);
    return 0;
}

```

![image](https://github.com/XinranSix/Computer-Graphics/assets/62458905/cbf35b47-f485-4f3c-8b1f-153684f64dd3)

> 迪杰斯特拉提出了 goto 有害论，所以我们要少用 goto 语句。

