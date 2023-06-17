![829522](https://github.com/XinranSix/docs/assets/62458905/7e9c8282-1533-4f19-89b7-dd990cd6de4c)

[toc]

## 终端提示符

```bash
yaojie@yaojie-virtual-machine:~$ 
yaojie: 用户名
yaojie-virtual-machine: 主机名
```

```bash
~: 家目录
/: 根目录
```

```bash
$: 普通用户权限
#: 管理员权限
```

## 命令帮助信息

```bahs
命令 --help
```

> 注意：并不是所有的命令都有帮助信息。

![image](https://github.com/XinranSix/docs/assets/62458905/ddd040ff-025a-4674-b58a-cf33e3184e24)

### man 命令

man 命令是 linux 提供的帮助手册，可以查询命令、函数或者特殊的文件，这个手册有很多个章节。

第一章中放的是命令的帮助信息。

第二章中放的是系统调用。

第三章中放的是库函数的帮助信息。

使用 `man man` 查看 man 命令的帮助信息：

![image](https://github.com/XinranSix/docs/assets/62458905/3ded45a7-de5d-41f8-9b3d-3f59fa945f3a)

用法：

```bash
man 章节 查找信息

例如：
man 1 ls 或者 man ks
man 2 open
```

![image](https://github.com/XinranSix/docs/assets/62458905/262e202c-0379-4fb5-8945-6a2d8fe1e02e)

## 命令常用的技巧

### 自动补全

输入命令的一部分，按 <kbd>tab</kbd> 键，会可以自动补全命令，如果匹配到了多个命令，按两次 <kbd>tab</kbd>，会在终端打印所有可用的命令。

文件和目录也可以使用如上操作进行补全。

### 历史命令

可以通过**上下方向键**将以前输入过的命令调出来，敲回车再次执行和做修改后执行。

### 重定向

```bash
命令 > 目的文件 # 先清空原本文件内容，然后将命令的输出结果写入文件
命令 >> 目的文件 # 以追加的方式将命令的输出结果写入文件
```

![image](https://github.com/XinranSix/docs/assets/62458905/3acef1f4-1c41-4965-8d40-607529f00ddf)

### 管道

将一个程序的输出作为另外一个程序的输入：

```bash
ls ‐‐help | more # 以每页的方式查看ls命令的帮助信息
ls /etc | wc ‐w # 统计根目录下的etc目录中的文件数
```

![image](https://github.com/XinranSix/docs/assets/62458905/7e3f7021-9de4-4573-af31-55793882d017)

## `ls`

```bash
ls #查看当前目录下的文件名
ls 目录名 #查看指定目录下的文件名
ls / #查看根目录下的文件名
ls ‐a #查看当前目录下的所有文件名，包括隐藏文件
ls ‐l #查看当前目录下文件的详细信息
ls ‐al #查看当前目录下所有文件的详细信息
ls ‐hl #详细信息中的字节数可以带单位的显示
```

![image](https://github.com/XinranSix/docs/assets/62458905/76da838f-68bb-420b-a4c9-328006bd8293)

```bash
drwxr-xr-x  20 root root       4096  6月  7 15:12 .
d：文件类型，linux里面不以后缀名作为文件类型的区分
linux里面一共有其中文件类型bcd‐lsp，linux里面一切皆文件
    b：块设备文件
    c：字符设备文件
    11
    d：目录文件
    ‐：普通文件
    l：软链接文件
    s：套接字文件
    p：管道文件
rwxr-xr-x：文件权限，以三个为一组，分别表示用户主、用户组以及其他用户对文件的操作权限，r：读权限，w：写权限，x：可执行权限，如果是‐，就表示没有这个权限
20：链接文件的个数
root：用户名
root：用户组名
4096：文件大小，默认以字节为单位
6月  7 15:12：时间戳，文件的最后修改时间
.：文件名
```

## `tree`

以树状结构显示目录信息。

![image](https://github.com/XinranSix/docs/assets/62458905/978079cd-598c-4112-a24b-066af2214d7b)

```bash
 tree -L 层数 # 用于显示指定的层数
```

![image](https://github.com/XinranSix/docs/assets/62458905/2e1ec8ac-82f4-47da-aef5-dd805bc7bf2e)

## `clear`

清屏。

## `cd`

```bash
cd 当前目录下的目录名 #进入指定的目录
cd / #进入根目录
cd ~ #进入家目录
cd .. #进入当前目录的上一级目录
cd ‐ #返回到上一次的路径
```

## `pwd`

```bash
pwd #显示当前路径的绝对路径
```

![image](https://github.com/XinranSix/docs/assets/62458905/985fd7a6-2383-4925-acdd-87f6c853130c)

## `cat`

```bash
cat 文件名 #显示文件的内容
cat ‐n 文件名 #带行号的显示文件的内容
```

![image](https://github.com/XinranSix/docs/assets/62458905/dbbfe639-6755-49ad-805d-74421f89b169)

## `rm`

```bash
rm 文件名 #删除指定的文件
rm ‐rf 目录文件名 #删除指定的目录文件
```

![image](https://github.com/XinranSix/docs/assets/62458905/e89c9545-9582-43a4-b8e8-086aa2cefcd2)

## `cp`

```bash
cp 文件名 目录名 #将文件复制到目录中
cp 目录1 目录2 ‐a #将目录1复制到目录2中
cp 文件名1 文件名2 #如果文件2不是目录，则文件1复制一份为文件2，如果文件2存在且不是一个目录，则直接将内容替换传文件1的
```

![image](https://github.com/XinranSix/docs/assets/62458905/590f369d-0beb-4655-b094-de8792eabef8)

## `mv`

```bash
mv 文件名 目录名 #将文件移动到指定的目录中
mv 目录1 目录2 #将目录1移动到目录2中
mv 文件1 文件2 #如果文件2不存在，则功能为重命名
```

![image](https://github.com/XinranSix/docs/assets/62458905/80561c5d-d60f-4225-b78d-5b3f749bcd70)

## `mkdir`

```bash
mkdir 目录名 #创建一个目录文件
mkdir 目录1 目录2 ... #创建多个目录
mkdir ‐p 目录1/目录2/目录3/... #嵌套的创建多个文件
```

![image](https://github.com/XinranSix/docs/assets/62458905/17230b5f-42b5-46aa-a898-d9fefbf90a42)

## `touch`

```bash
touch 文件名 #创建一个文件
#注意：如果文件已经存在，则touch会修改当前时间的时间戳
```

![image](https://github.com/XinranSix/docs/assets/62458905/c99c60dd-fb89-4b43-b4cf-5306b95aa39d)

## `find`

```bash
find 路径 ‐name 文件名 #在指定的路径下查找指定的文件，会从指定路径下包括所有的子目录中寻找
```

![image](https://github.com/XinranSix/docs/assets/62458905/22dc10dc-17c9-4171-b0ce-23ab6ea161be)

## `grep`

```bash
grep 查找信息 文件名 #在指定的文件中查找指定的内容，将查找到的内容整行输出并高亮显示查找的内容
grep 查找信息 文件名 ‐n #在指定的文件中查找指定的内容，将查找到的内容整行且带行号输出并高亮显示查找的内容
grep 查找信息 * ‐R ‐n #从当前目录以及子目录中的文件中查找指定信息
```

## `ln`

```bash
ln 源文件名 链接文件名 ‐s #创建一个链接文件（类似windows的快捷方式）
```

> 注意：
>
> - 不管对源文件还是链接文件进行修改，双方的内容都会改变。
> - 如果删除链接文件，对源文件没有任何影响。
> - 如果删除源文件，则链接文件失效

## `tar`

### gzip 格式

**压缩：**

```bash
tar zcvf 压缩包包名 文件1 文件2 文件3 ...
# 注意：压缩包包名一般以.tar.gz作为后缀名
```

**解压：**

```bash
1tar zxvf 压缩包包名
tar zxvf 压缩包包名 ‐C 路径 #解压到指定的路径
```

### bz2 格式

**压缩：**

```bash
tar jcvf 压缩包包名 文件1 文件2 文件3 ...
#注意：压缩包包名一般以.tar.bz2作为后缀名
```

**解压：**

```bash
tar jxvf 压缩包包名
tar jxvf 压缩包包名 ‐C 路径 解压到指定的路径
```

## vi



### 安装 vim（vi 升级版）

```bash
sudo apt install vim
```

### vi 的使用

```bash
vi 文件名 #在vi编辑器中打开或者创建一个文件，并将光标置于第一行行首
vi +n #文件名 打开存在文件，并将光标置于第n行行首
```

### vi 的三种模式

1. 插入模式：这种模式可以直接编辑文档
2. 编辑模式：在编辑模式下可以执行一些命令，执行复制、剪切、粘贴等功能。
3. 命令模式：在此模式下可以保存文件，退出 vi.

![vim-vi-workmodel](https://github.com/XinranSix/docs/assets/62458905/fb96ef4d-e48e-4800-a772-2b5700375c15)

**命令模式下的一些指令：**

- `w`：保存文件
- `wq`：保存并退出
- `x`：保存并退出
- `q!`：强制退出
- `w finename`：能成为 `filename`

**编辑模式下的操作：**

- `u`：撤销前面多次修改，`ctrl` 反撤销。
- `[n]x`：删除光标后 n 个字符。
- `[n]X`：删除光标前 n 个字符。
- `[n]dd`：剪切从当前行开始的 n 行。
- `[n]yy`：复制从当前行开始的 n 行。
- `p`：粘贴。
- `.`：执行上一次操作。
- <kbd>shift</kbd> + `zz`：保存退出。

**编辑模式下移动光标：**

- `n[G]`：将光标移动到第 n 行开始处。
- `G`：将光标移动到文件尾。
- `gg`：将光标移动到文件开始处。

**编辑模式下的查找：**

- `/字符串`：从光标开始处向文件尾查找字符串。
- `n`：同一方向重复上一次查找命令。
- `N`：反方向错误上一次查找命令。

## GCC 编译器

程序的编译分为四个阶段： 由 `.c` 到可执行程序：

1. 预处理；
2. 编译；
3. 汇编；
4. 链接。

**编译程序：**

1. 一步到位：

```bash
gcc hello.c # 默认会生成一个名为a.out的可执行文件
gcc hello.c -o hello
```

```c
#include <stdio.h>

int main(int argc, const char *argv[]) {
    printf("hello world\n");
    return 0;
}
```

![image](https://github.com/XinranSix/docs/assets/62458905/940f33cf-8714-47ba-9475-416d87e4e98b)

2. 分步骤完成：

```bash
gcc -E hello.c -o hello.i #1、预处理
gcc -S hello.i -o hello.s #2、编译
gcc -c hello.s -o hello.o #3、汇编
gcc hello.o –o hello #4、链接
```

## 参考

- [Linux vi/vim | 菜鸟教程](https://www.runoob.com/linux/linux-vim.html)

