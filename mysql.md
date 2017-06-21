# 数据库操作

## 创建

```
create database demo;
```

## 选择

```
use demo;
```

## 删除
```
drop database user;
```

## 查看

```
show databases;
```

# 数据表操作

## 查看

```
show tables;
```


## 创建

格式为：

```
CREATE TABLE [IF NOT EXISTS] 表名称(
  字段1  列类型  [属性]  [索引]
  字段2  列类型  [属性]  [索引]
  ....
  字段n  列类型  [属性]  [索引]
)[表类型] [表字符集];
```

其中，方括号里面的是可选选项。

字符集一般使用`utf-8`。

表名称和字段名需要自己定义，这些名称区分大小写。

例如：

```
create table if not exists user(
id int, 
name varchar(9), 
pswd varchar(10)
);
```

## 删除

```
drop table if exists user
```

## 查看表字段

```
desc user;
```

## 查看表数据

```
select * from user;
```



## 插入表内容

```
insert into user(id,name,pswd) values(1,"zhangsan","zhangsan");
insert into user(id,name,pswd) values(1,"lisi","lisi");
insert into user(id,name,pswd) values(1,"wanger","wanger");
insert into user(id,name,pswd) values(1,"mazi","mazi");
```

## 删除表内容

```
delete from user where id=1;
```

## 修改表内容

```
update user set id=2 where id=1;
```

## 修改表名字

```
rename table user to user2;
```

## 增加一列

```
alter table user add sex varchar(5) not null dafault "man"
```

# 索引操作

## 创建一个带有自增的、有主键索引和普通索引的表格

```
mysql> create table suoyin_table(
    -> id int unsigned auto_increment,
    -> name varchar(10),
    -> primary key(id),
    -> index in_name(name)
    -> );
```

## 查看表里的索引内容

```
show index from suoyin_table\G
```

## 删除索引

```
alter table suoyin_table drop index in_name;
```

## 增加索引

```
alter table suoyin_table add index in_name(name);
```

## 寻找一个表的内容

```
select * from suoyin_table where name="c";
```

## 查看寻找内容使用了多少行

```
desc select * frome suoyin_table where name="c"\G
```

# 数据表字段

## 添加

```
alter table suoyin_table add age int;
```

## 修改

```
alter table suoyin_table modify age int not null default 20;
```

修改`age`的属性，默认年龄为20岁。

```
alter table suoyin_table change name username varchar(30);
```

修改`name`名称为`username`。

但是后面必须要跟上类型，但是其索引类型不需要写，并且不会丢失。

## 删除

```
alter table suoyin_table drop age;
```

# 保存所有mysql数据操作

```
mysql -u root -pwuwenchi --tee=/home/mysql.log
```

# 查看当前状态

```
\s
```

