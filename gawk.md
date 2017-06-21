语法：

> awk  option  'pattern  {action}'  file

- pattern  表示 AWK 在数据中查找的内容
- action     表示在找到匹配内容时所执行的一系列命令

awk处理方式与数据库累死，支持对记录和字段处理。

在awk中，缺省的情况下是将文本文件中的一行视为一个记录，而把一行中的某一个部分作为记录中的一个字段，用1,2,3数字的方式顺序的表示行中的不同字段，用`$`符号后跟数字，引用对应的字段，以都好分割，0表示整个行。

|        选项        | 描述             |
| :--------------: | -------------- |
| -f  program-file | 从文件中读取awk程序源文件 |
|      -F fs       | 制定fs为输入字段分隔符   |
|   -v val=value   | 变量赋值           |
|     --posix      | 只支持POSIX正则表达式  |

|        pattern        | 描述               |
| :-------------------: | ---------------- |
|        BEGIN{}        | 给程序赋予初始状态，先执行的工作 |
|         END{}         | 程序结束后执行的一些扫尾工作   |
| /regular  expression/ | 为每个输入记录匹配正则表达式   |
|  pattern && pattern   | 逻辑 and，满足两个模式    |
|  pattern\|\|pattern   | 逻辑or，满足一个模式      |
|       ! pattern       | 逻辑not，不满足模式      |
|  pattern1, pattern2   | 范围模式，匹配模式1，直到模式2 |

#### 更改分隔符

```
tail /etc/services | awk -F '/' '{print $2}'
tail /etc/services | awk -F '[/#]+' '{print $2}'
tail /etc/services | awk -F '[ /#]+' '{print $2}'  加号表示前面的字符出现一次或者多次
```

### 定义变量

```
awk -va="123" 'BEGIN{print a}'
或者直接定义一个变量：
a=456
awk 'BEGIN{print '$a'}' 单引号表示引用的是变量
```

### BEGIN、END

```
tail /etc/services | awk 'BEGIN{print "\nServer\t\tPort\t\t\tDesc\n================="}{print $0}END{print "==========================\nend...."}'
```

### 匹配打印

```
tail /etc/services | awk '/tcp/{print $0}'
```

### && || ! 

```
tail /etc/services | awk '/^b/ && /tcp/ {print $0}'
tail /etc/services | awk '/^b/ || /^c/ {print $0}'
tail /etc/services | awk '!/tcp/ {print $0}'
```

|    内置变量    | 描述                            |
| :--------: | ----------------------------- |
|     FS     | 输入字段分隔符，默认是空格或者制表符            |
|    OFS     | 输出字段分隔符，默认是空格                 |
|     RS     | 输入记录分隔符，默认是换行符 \n             |
|    ORS     | 输出记录分隔符，默认是换行符                |
|     NF     | 统计当前记录总共几个字段                  |
|     NR     | 统计记录编号，每处理一行，编号会加一            |
|    FNR     | 与NR相同，但会在处理第二个文件的时候，编号会先清零    |
|    ARGC    | 命令行参数数量                       |
|   ARGIND   | 当前正在处理的文件索引值，第一个文件是1，第二个文件是2  |
|    ARGV    | 命令行参数数组序列，下标从0开始，ARGV[0]是 awk |
|  ENVIRON   | 当前系统环境变量                      |
|  FILENAME  | 输出当前处理的文件名                    |
| IGNORECASE | 忽略大小写                         |
|   SUBSEP   | 数组中下标的分隔符，默认为"\034"           |

### FS OFS

```
awk 'BEGIN{FS=":"}{print $1,$2}' /etc/passwd
也可以使用-v来重新给FS赋值
awk -vFS=":" '{print $1,$2}' /etc/passwd
```

```
awk 'BEGIN{FS=":";OFS="==="}{print $1,$2}' /etc/passwd
也可以直接更改输出形式：
awk 'BEGIN{FS=":"}{print $1"==="$2}' /etc/passwd
```

## RS

```
echo "www.baidu.com" | awk 'BEGIN{RS="."}{print $0}'
```

RS也支持正则：

```
seq -f "str%02g" 10 | sed 'n;n;a\------' | awk 'BEGIN{RS="-+"}{print $1}'
```

### NF

```
echo "a b c d e f" | awk '{print NF}'  		# NF=6
echo "a b c d e f" | awk '{print $NF}' 		# 打印第6个字段
echo "a b c d e f" | awk '{print $(NF-1)}' 	# 打印第5个字段
echo "a b c d e f" | awk '{$(NF-1)="z";print $0}'	# 把第五个字段赋值为z
```

### NR FNR

```
awk 'FNR==NR{print "1"FNR!=NR{print "2"}'
```

在处理两个文件的时候，因为FNR会重新计数，所以当他们相等的时候，输出为1，表示在处理第一个文件，当他们不相等的时候，表示在处理第二个文件，输出为2。

## ARGC ARGV

1:20:00