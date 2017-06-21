生成target：

```
obj=main.o add.o mul.o
target=app
CC = gcc
$(target):$(obj)
	$(CC) $(obj) -o $@
```

根据 .c 文件生成相应的 .o 文件：

```
%.o : %c
	gcc -c $< -o $@
```

- $< : 规则中第一个依赖
- $@ : 规则中的目标
- $^ : 规则中的所有的依赖

这三个变量只能在规则中使用。

## 系统自维护变量

- CC : 编译器
- CPPFLAGS : 预处理时候需要的参数，例如：-I（大写的i）
- CFALGS : 编译的时候使用的参数，例如：-Wall -g -c
- LDFLAGS : 链接库使用的选项 ：-L -l



## 函数

```
src = $(wildcard ./*.c)  查找所有的 .c 文件
obj = $(patshubst ./%.c, ./%.o, $(src)) 把所有的 .c 文件替换成 .o 文件，.c 文件从 src 中取
```

## 伪目标

```
.PHONY:clean
clean:
	-rm -f $(obj) $(target)
```

否则当你本地有个 clean 的文件的时候，会出现：“clean” 是最新的。

命令前面加一个`-`，表示如果 rm 执行失败了，则会忽略此命令，继续向下执行命令。