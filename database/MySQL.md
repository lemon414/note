# MySQL中的编码

## 字符集

1. 保存数据的时候需要使用字符集
2. 数据传输的时候也需要使用字符集
3. 在存续的时候使用字符集
4. 在MySQL的服务器上, 在数据库中, 在表的使用上, 在字段的设置上.
5. 在服务器安装的时候, 可以指定默认的字符集

`set names gbk`:修改当前MySQL的字符编码（全部修改）

`set charset_set_client=gbk`:临时修改

## 校对集

在某一种字符集下, 为了使字符之间可以互相比较, 让字符和字符形成一种关系的集合, 称之为校对集。
比如说 ASCII 中的 a 和 B, 如果区分大小写 a > B, 如果不区分 a < B;
不同字符集有不同的校对规则, 命名约定:以其相关的字符集名开始, 通常包括一个语言名, 并且以_ci 、 _cs 或 _bin 结束。
_ci : 大小写不不敏敏感
_cs : 大小写敏敏感
_bin : binary collation 二元法, 直接比较字符的编码, 可以认为是区分大小写的, 因为字符集中'A'和'a'的编码显然不不同。

# MySQL的数据类型

单行数据存储上限65535字节

布尔型底层是用int定义的，不能用引号

## 整型

![1567601752654](/tmp/1567601752654.png)

zerofill:显示宽度，位数不足时用0填充
unsigned 给int指定无符号，即不会有负数
```
create table t4(
id int(10) zerofill unsigned primary key auto_increment,
name char(32)
);
```

## 浮点型

float（M，D）

double（M，D）

M 是支持多少个长度, D 是小数点后面的位数

## 字符串

## 枚举

类似于网页里面的多选框，限制了可选值，节省了空间，运行效率高。

```
create table t6(
	name varchar(32),
	sex enum('男','女女女','保密') default '保密'
);
-- 枚举类型的计数默认从1开始
insert into t6 set name='王宝强',sex=1;
```

## 集合

set最多可以有64个不同的成员。类似于复选框, 有多少可以选多少。

```
create table t7 (
name varchar(32),
hobby set('吃','睡','玩','喝喝','抽')
);
insert into t7 values('张三','睡,抽,玩,吃,喝喝');
insert into t7 values('李李四','睡,抽');
```

## 时间类型

![1567602350076](/tmp/1567602350076.png)

## 布尔型

mysql中的bool类型也是1和0

```
create table `bool`(
cond boolean
);
insert into `bool` set cond=True; -- 成功
insert into `bool` set cond=False; -- 成功
insert into `bool` set cond=1; -- 成功
insert into `bool` set cond=10; -- 成功
insert into `bool` set cond=-1; -- 成功
insert into `bool` set cond=0; -- 成功
insert into `bool` set cond=0.1; -- 成功
insert into `bool` set cond='True'; -- 失败
```

## 列的属性

- null 插入的值是否可以为空，不写默认是空。
- default 设置默值
- auto_increment 自动增长（int类型），默认从1开始，长配合主键使用。
- primary key 主键，唯一的标示，不能为空也不能重复，一张表中只能拥有一个主键或者一个联合主键。
- unique 唯一值，保证列中的每一个数据都不重复
- comment 字段说明，一般给开发者看的

group by 也可以用于去重 distinct

# MySQL的运算符