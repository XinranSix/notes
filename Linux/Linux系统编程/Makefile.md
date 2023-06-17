![5c23d52f880511ebb6edd017c2d2eca2](https://github.com/XinranSix/docs/assets/62458905/92325779-86d5-450d-9d76-bfc4e27629c2)

[toc]

## make 概述

`make` 是个命令，是个可执行程序，用来解析 makefile，这个命令存放在 `/usr/bin/`.

makefile 是个文件，这个文件中描述了程序的编译规则。

执行 `make` 命令的时候，`make` 命令会在当前目录下找 makefile 文件，根据 makefile 文件里的规则，编译程序。

> makefile 文件是程序员根据自己的程序编写的编译规则。

1. GNU make 是一种代码维护工具；
2. make 工具会根据 makefile 文件定义的规则和步骤，完成整个软件项目的代码维护工作；
3. 用来简化编译工作，可以极大地提高软件开发的效率；
4. windows 下一般由集成开发环境自动生成；
5. linux 下需要由我们按照其语法自己编写。

**make 主要解决两个问题：**

1. 大量代码的关系维护：大项目中源代码比较多，手工维护、编译时间长而且编译命令复杂，难以记忆及维护，把代码维护命令及编译命令写在 makefile 文件中，然后再用 `make` 工具解析此文件自动执行相应命令，可实现代码的合理编译。
2. 减少重复编译时间：在改动其中一个文件的时候，能判断哪些文件被修改过，可以只对该文件进行重新编译，然后重新链接所有的目标文件，节省编译时间。

## makefile 语法及其执行

### makefile 语法规则

```makefile
目标:依赖文件列表
	命令列表
```

> 1. 目标：通常是要产生的文件名称，目标可以是可执行文件或其它 obj 文件，也可是一个动作的名称。
> 2. 依赖文件：是用来输入从而产生目标的文件，一个目标通常有几个依赖文件（可以没有）。
> 3. 命令：make 执行的动作，一个规则可以含几个命令（可以没有），有多个命令时，每个命令占一行。

例如下面是一个简单的 makfile 案例：

```h
// main.h

#define.h PI 3.1415926
```

```c
// main.c

#include <stdio.h>
#include "main.h"

int main() {
    printf("hello makefile\n");
    printf("PI=%lf", PI);
    return 0;
}
```

```makefile
main:main.c main.h
	gcc main.c -o main
clean:
	rm main
```

### make 命令格式

```bash
make [-f file] [targets]
```

1. `[-f file]`：`make` 默认在工作区查找名为 `GUNmakefile`、`makefile`、`Makefile` 的文件作为其输入文件，`-f` 参数可以指定非以上名字的文件作为 makefile 文件输入。
2. `targets`：在执行 `make` 命令是如果没有指定目标，则会默认执行 makefile 文件里的第一个目标，然后退出，可以指定多个目标，目标之间用空格分隔。

### Makefile 案例

```c
// sum.c

#include "head.h"

int sum(int a, int b) { return a + b; }
```

```c
// sub.c

#include "head.h"

int sub(int a, int b) { return a - b; }
```

```h
// head.h

#ifndef HEAD_H
#define HEAD_H

int sum(int a, int b);
int sub(int a, int b);

#endif
```

```h
// main.c

#include "head.h"
#include <stdio.h>

int main(int argc, const char *argv[]) {
    int x = 1000;
    int y = 900;

    printf("%d + %d = %d\n", x, y, sum(x, y));
    printf("%d ‐ %d = %d\n", x, y, sub(x, y));

    return 0;
}
```

```makefile
# makefile

main:main.o sub.o sum.o
        gcc main.o sub.o sum.o -o main

main.o:main.c
        gcc -c main.c -o main.o

sub.o:sub.c
        gcc -c sub.c -o sub.o

sum.o:sum.c
        gcc -c sum.c -o sum.o

clean:
        rm *.o main a.out -rf
```

![image](https://github.com/XinranSix/docs/assets/62458905/ba7c60ad-10aa-4817-8025-b889b9c9d4ab)

### 假想目标

前面 makefile 中出现的文件称之为假想目标，假想目标并不是一个真正的文件名，通常是一个目标集合或者动作，可以没有依赖或者命令，一般需·要显示的使用 `make + 名字` 显示调用。

```bash
all:exec1 exec2
clean:
    rm *.o exec
    
# 运行时使用make clean 就会执行clean后面的命令
```

## makefile 变量

### makefile 变量概述

makefile 变量类似于 C 语言中的宏，当 makefile 被 make 工具解析时，其中的变量会被展开。

变量的作用：保存文件名列表、保存文件目录列表、保存编译器名、保存编译参数、保存编译的输出。

### 变量的分类

1. 自定义变量：在makefile文件中定义的变量，make 工具传给 makefile的变量。
2. 系统环境变量：make 工具解析 makefile 前，读取系统环境变量并设置为 makefile 的变量。
3. 预定义变量。

### 自定义变量语法

```makefile
定义变量：
    变量名=变量值
引用变量：
    $(变量名)或${变量名}
注意：makefile 变量名可以以数字开头
```

> 注意：
>
> 1. 变量是大小写敏感的；
> 2. 变量一般都在 makefile 的头部定义；
> 3. 变量几乎可在 makefile 的任何地方使用。

```makefile
CC=gcc
obj=main
obj1=sub
obj2=sum
OBJ=main.o sub.o sum.o

$(obj):$(OBJ)
        $(CC) $(OBJ) -o $(obj)

$(obj).o:$(obj).c
        $(CC) -c $(obj).c -o $(obj).o

$(obj1).o:$(obj1).c
        $(CC) -c $(obj1).c -o $(obj1).o

$(obj2).o:$(obj2).c
        $(CC) -c $(obj2).c -o $(obj2).o
    
clean:
        rm *.o $(obj) a.out -rf
```

![image](https://github.com/XinranSix/docs/assets/62458905/e1c323ce-ea91-49ec-9a6b-97e6cd852fd8)

### 系统环境变量

make 工具会拷贝系统的环境变量并将其设置为 makefile 的变量，在 makefile 中可直接读取或修改拷贝后的变量。

### 预定义变量

makefile 中有许多预定义变量，这些变量具有特殊的含义，可在 makefile 中直接使用。

|   变量名   |                解释                 |
| :--------: | :---------------------------------: |
|    `$@`    |               目标名                |
|    `@<`    |     依赖文件列表中的第一个文件      |
|    `@^`    |  依赖文件列表中除去重复文件的部分   |
|    `AR`    |  归档维护程序的程序名，默认值为 ar  |
| `ARFLAGS`  |         归档维护程序的选项          |
|    `AS`    |     汇编程序的名称，默认值为 as     |
| `ASFLAGS`  |           汇编程序的选项            |
|    `CC`    |     C 编译器的名称，默认值为 cc     |
|  `CFLAGS`  |           C 编译器的选项            |
|   `CPP`    | C 预编译器的名称，默认值为 $(CC) -E |
| `CPPFLAGS` |           C 预编译的选项            |
|   `CXX`    |   C++ 编译器的名称，默认值为 g++    |
| `CXXFLAGS` |          C++ 编译器的选项           |

```makefile
CC=gcc
obj=main
obj1=sub
obj2=sum
OBJ=main.o sub.o sum.o
CFLAGS=-Wall -g

$(obj):$(OBJ)
        $(CC) $^ -o $@

$(obj).o:$(obj).c
        $(CC) $(CFLAGS) -c $< -o $@

$(obj1).o:$(obj1).c
        $(CC) $(CFLAGS) -c $< -o $@

$(obj2).o:$(obj2).c
        $(CC) $(CFLAGS) -c $< -o $@

clean:
        rm *.o $(obj) a.out -rf
```

![image](https://github.com/XinranSix/docs/assets/62458905/545d9d4c-ca5c-4889-8ac0-65a0ad2833e7)

最精简版：

```makefile
CC=gcc
obj=main
OBJ=main.o sub.o sum.o
CFLAGS=-Wall -g

$(obj):$(OBJ)
        $(CC) $^ -o $@

%*.o:%*.c
        $(CC) $(CFLAGS) -c $< -o $@

clean:
        rm *.o $(obj) a.out -rf
```

![image](https://github.com/XinranSix/docs/assets/62458905/d94cb078-d2c5-4d75-ac72-21e9670b1ba9)

## 参考

- [跟我一起写 Makefile（一）| 陈皓| CSDN](https://haoel.blog.csdn.net/article/details/2886?spm=1001.2101.3001.6650.17&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-17-2886-blog-2898.235%5Ev38%5Epc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-17-2886-blog-2898.235%5Ev38%5Epc_relevant_sort_base1&utm_relevant_index=18)