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
