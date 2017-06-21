# 启动gdb

- start  只执行一步
- n --- next
- s ---- step(单步，可以进入函数体内部)
- c ---- continue (直接停在断点位置)
- finish  从函数体内跳出
- u  退出当前循环
- p  ---- print  查看变量的值
- ptype 变量名   ：查看变量值类型
- set var 变量名=赋值 ：设置变量的值
- display    设置追踪变量
- quit  退出gdb



# 查看代码

- l ---- list
- l 行号 (函数名)
- l filename:行号(函数名)



# 设置断点

- 设置当前文件：
  - b ---- break
  - b 行号(函数名)
  - b filename:行号(函数名)
- 设置指定文件断点：
- 设置条件断点：
  - b  行号 if  value == 19
- 删除断点：
  - d ---- del ---- delete
  - d 断点编号
- 查看断点编号：
  - i ---- info
  - info 断点