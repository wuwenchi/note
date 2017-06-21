## 生成 elf 和 bin 文件

gcc 命令编译出来的是 elf 格式文件，bin 文件是 elf 文件中的代码段、数据段，以及一些自定义的段抽取出来做成的一个内存镜像。

可以使用 `objcopy ` 工具来把 elf 文件转换为 bin 文件：

```
objcopy [选项]... 输入文件 [输出文件] 
objcopy -O binary abc.elf abc.bin
```



## 指定链接的库 `-l -L`

- `-l` 小写的L，用来指定程序要链接的库
- `-L` 用来指定库名

比如，要使用 /a/b/c 目录下的 libtest.a 库：

```
-L/a/b/c -ltest
```

## `-c` 

只激活预处理、编译 和 汇编，

即生成 .o 文件。

## `-D` 宏定义

- -Daa 定义宏 aa，相当于 c 里面的 #define aa
- -Daa=bb 定义宏aa，并赋值bb，相当于 c 里面的 #define aa bb



## `-I` 添加头文件搜索路径

使用此选项，可以指定头文件搜索路径，例如：

```
./include
|-----  a.h
|-----  h
		|---- b.h
gcc -I ./include
```

则在 c 中就可以直接写为：

```
#include <a.h>
#include <h/b.h>
```



| 选项                 | 描述                 |
| ------------------ | ------------------ |
| static             | 禁止使用动态库            |
| share              | 尽量使用动态库            |
| Wall               | 生成所有警告信息           |
| nostdlib           | 不使用标准系统的启动文件和系统库   |
| nostartfiles       | 连接的时候，不使用标准系统的启动文件 |
| ffunction-sections | 优化的时候使用的……         |
