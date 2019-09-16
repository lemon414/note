环境变量

zcg@zcg-PC:~$ echo $PATH

/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/sbin:/usr/sbin

变量定义等号前不能有空格a=123

export 会使变量变全局变量

使用变量要在变量前面加$

终端里的输出printf 结尾要手动添加\n

中括号[]也是一个命令，[  -f 前四天的文档.zip  ];  echo $? ，中括号里面前后必须要留空格

$[] 加上符号就是运算

Linux 中的所有程序执行结束后都有状态码

shell 里面0 代表true  1 代表false 和python正好相反



# shell脚本首行

脚本文件第一行通过注释的方式指明执行脚本的程序。

shell脚本第一句

#!/bin/bash

#!/bin/sh

#!/usr/bin/env bash

#!/usr/bin/env python (python脚本第一句）

# 创建脚本

```
chmod 755 test  赋予权限
vim test.sh   进入vim编辑器
添加代码
#!/bin/bash
echo "hello world"
echo "i am `whoami`"  反引号里面的代码优先执行
echo "the cpu in my pc has `cat /proc/cpuinfo |grep -c processor` cores"
exit 0    脚本的退出状态  
写入完成 保存退出
./test    执行脚本文件
echo $?    查看脚本的退出状态，状态码为零表示正常, 状态码为 正整数 代表异常退出
```

# 变量

变量定义，等号前后没有空格

a=12345

使用变量时，前面要加上$符号,双引号和单引号也有区别

echo "$a"   输出结果是123456

echo  '$a'     输出结果是$a    原样输出

shell下全局变量用export定义

常用的环境变量:$PATH：可执行文件目录

$PWD：当前目录

$HOME：家目录

$USER：当前用户名

$UID ：当前用户的uid

```
zcg@zcg-PC:~$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/sbin:/usr/sbin
zcg@zcg-PC:~$ echo $PWD
/home/zcg
zcg@zcg-PC:~$ echo $HOME
/home/zcg
zcg@zcg-PC:~$ echo $USER
zcg
zcg@zcg-PC:~$ echo $UID
1000
```

# 分支语句

条件测试命令：**[ condition ]**里面的条件是参数，所以其前后必须有空格，否则会报错。它可以进行三种比较：数值、字符串、文件。

格式：

```
if [ condition ]
then
	commands
fi
```

- 数值比较

> n1 -eq n2      检查n1是否与n2相等
> n1 -ge n2      检查n1是否大大于或等于n2
> n1 -gt n2       检查n1是否大大于n2
> n1 -le n2       检查n1是否小小于或等于n2
> n1 -lt n2        检查n1是否小小于n2
> n1 -ne n2      检查n1是否不不等于n2

- 字符串比较

> str1 = str2       检查str1是否和str2相同
> str1 != str2      检查str1是否和str2不不同
> str1 < str2       检查str1是否比比str2小小
> str1 > str2       检查str1是否比比str2大大
> -n str1              检查str1的⻓长度是否非非0
> -z str1               检查str1的⻓长度是否为0

- 文件比较

> -d file            检查file是否存在并是一一个目目录
> -e file            检查file是否存在
> -f file             检查file是否存在并是一一个文文件
> -r file             检查file是否存在并可读
> -w file           检查file是否存在并可写
> -x file            检查file是否存在并可执行行行
> -s file            检查file是否存在并非非空
> -O file           检查file是否存在并属当前用用户所有
> -G file            检查file是否存在并且默认组与当前用用户相同
> file1 -nt file2 检查file1是否比比file2新
> file1 -ot file2 检查file1是否比比file2旧

## for 

Shell 中的循环结构有三种: for 、 while 和 until

for 格式

```
for 变量 in 序列 do
	要执行的命令
done

打印1到10中的偶数
for i in `seq 1 10`
do
	if [[ $[ $i % 2] == 0 ]]
	then
		echo "偶数: $i"
	else
		echo "奇数: $i"
	fi
done

```

1. seq START END 语句用来产生一个数字序列
2. $[ NUM1 + NUM2 ] 语句用来进行基本的数学运算
3. [[ ... ]] 语句用来更方便的进行比较判断

c语言风格的for循环

```
for ((i=0; i<10; i++))
do
	echo "num is $i"
done
```

#  函数

1. 函数定义
    定义时 function 不是必须的,可以省略

  ```
  function foo() {
  	echo "---------------------------"
  	echo "Hello $1, nice to meet you!"
  	echo "---------------------------"
  }
  ```

2.函数的使用

- 在终端或脚本中直接输入函数名即可,不需要小括号
- 传参也只需将参数加到函数名后面,以空格做间隔,像正常使用命令那样

 ```
 foo seamile
 ```

3. 函数的参数

```
bar() {
	echo "执行者是 $0"
	echo "参数数量是 $#"
	echo "全部的参数 $@"
	echo "全部的参数 $*"
	if [ -d $1 ]; then# 检查传入的第一个参数是否是文件夹
		for f in `ls $1`
		do
			echo $f
        done
	elif [ -f $1 ]; then
		echo 'This is a file: $1' # 单引号内的变量不会被识别
		echo "This is a file: $1" # 如果不是文件夹, 直接显示文件名
	else
		echo 'not valid'
	fi
}
```

