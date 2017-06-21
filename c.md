# 1、printf 输出
在处理 printf 的时候，压栈顺序是从右往左 ，也就是说从右往左的计算。
***注：*** 计算 ***不等于*** 输出
在计算的时候，遇到 x++ 会记录此时的 x 的值作为最后的结果，
遇到 x 和 ++x 的时候，则不会将此时的计算结果作为最终的输出，只会修改 x 的值，在最终输出的时候输出 x 的值，所以 **++x 和 x 的结果总是一样的。**
例如：
```
int a = 1;
printf(%d %d %d %d %d %d",a++,++a,a++,++a,a++,++a);
```
答案：
6，7，4，7，2，7
```
int arr[6][3]={1,2,3,4,5,6,7,8,9};
int (*p)[3]=arr;
printf("%d\t%d\t%d\n",**p,**p++,**++p);
```
答案：7，4，4

# 2、结构体
一、结构体在申明并初始化的时候，可以使用乱序初始化。
二、结构体在定义函数的时候，可以使用外部的 `typedef`，也可以直接在结构体内部声明。
```
#include "stdio.h"

typedef int (*func_add)(int a, int b);

int aaaa(int a, int b)
{
    return a+b;
}

typedef struct _stu
{
    int a;
    int b;
    func_add add;
    // int (*add)(int a, int b); //这个使用的结构体内部声明函数，且不需要 tpyedef
}stu;

int main(void)
{
    stu stu1 = {
        .b = 2,
        .a = 5,
        .add = aaaa,
    };
    int tem = 1;
    tem = stu1.add(stu1.a,stu1.b);
    printf("a=%d, b=%d, add(a,b)=%d\n",stu1.a,stu1.b, tem);
    return 0;
}
```

# 3、宏
一、` # `：在一个宏中的参数前面使用一个 `# `，预处理器会把这个参数转换为一个字符数组，即 # 是字符串化的意思。例如：
```
#define ERROR_LOG(moudule) fprintf(stderr, "error: "#moudule" \n")
```
所以， ERROR_LOG(add) 展开后是：
```
fprintf(stderr, "error: "add" \n")
```
ERROR_LOG(devied =0) 展开后是：
```
fprintf(stderr,"error: devied=0\n")
```

二、`## ` 是一个分隔连接方式，作用是先分隔，然后进行强制连接。
```
#define TYPE1(type,name)   type name_##type##_type
#define TYPE2(type,name)   type name##_##type##_type
```
所以，TYPE1(int, c) 展开之后是：
```
int name_int_tpye
```
TYPE2(int, c)展开之后是：
```
int c_int_type
```

# 注：
1、数组在初始化的时候，可以指定初始化项目，例如：
```
int a[10] = {1,2,[4] = 4};
```
2、数组在指定大小的时候，可以使用变量，例如：
```
int n = 5;
int a[n];
```