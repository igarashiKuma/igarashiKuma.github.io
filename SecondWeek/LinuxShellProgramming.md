# Linux Shell编程

## 简介
>Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。
>Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

## 种类
- Bourne Shell(/usr/bin/sh或/bin/sh)
- Bourne Again Shell(/bin/bash)
- C Shell(/usr/bin/csh)
- K Shell(/usr/bin/ksh)
- Shell for Root(/sbin/sh)

## 编程

### 定义解释器
>`#!`是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell
```
#! /bin/bash
```

### 定义变量
>定义变量时，变量名不加美元符号（$，PHP语言中变量需要）。   
>注意，变量名和等号之间不能有空格，这可能和你熟悉的所有编程语言都不一样。同时，变量名的命名须遵循如下规则： 
>- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
>- 中间不能有空格，可以使用下划线（_）。
>- 不能使用标点符号。
>- 不能使用bash里的关键字（可用help命令查看保留关键字）。

```
your_name="runoob.com"
```

### 使用变量
>使用一个定义过的变量，只要在变量名前面加美元符号即可

```
your_name="runoob.com"
echo $your_name
echo ${your_name}
```

### 书写注释
>以 # 开头的行就是注释，会被解释器忽略

```
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
#
#
##### 用户配置区 结束 #####
```

### 传递参数
>我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：$n。n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推。

```
test.sh文件中添加如下语句
ehco "执行的第一个参数为： $1";

调用时传参
./test.sh 1

显示结果
第一个参数为： 1
```

#### 特殊参数
参数值|参数作用
--|--
$#|传递到脚本的参数个数
$\*|以一个单字符串显示所有向脚本传递的参数。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。
$$|脚本运行的当前进程ID号
$!|后台运行的最后一个进程的ID号
$@|与$*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
$-|显示Shell使用的当前选项，与set命令功能相同。
$?|显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。

### 输入输出重定向
>大多数 UNIX 系统命令从你的终端接受输入并将所产生的输出发送回到您的终端。一个命令通常从一个叫标准输入的地方读取输入，默认情况下，这恰好是你的终端。同样，一个命令通常将其输出写入到标准输出，默认情况下，这也是你的终端。

命令|说明
--|--
command > file|将输出重定向到 file
command < file|将输入重定向到 file
command >> file|将输出以追加的方式重定向到 file

#### 深入讲解
>一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：
>- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据
>- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据
>- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息

#### dev/null
>/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。   
>如果希望屏蔽 stdout 和 stderr，可以这样写`command > /dev/null 2>&1`

### 基本运算符
>Shell 和其他编程语言一样，支持多种运算符，包括：
>- 算数运算符
>- 关系运算符
>- 布尔运算符
>- 逻辑运算符
>- 字符串运算符
>- 文件测试运算符

>需要注意的是
>- 表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2，这与我们熟悉的大多数编程语言不一样。
>- 完整的表达式要被\` \`包含，注意这个字符不是常用的单引号，在 Esc 键下边。

#### 算术运算符

运算符|说明|举例
--|--|--
+|加法|`expr $a + $b` 结果为 30。
-|减法|`expr $a - $b` 结果为 -10。
*|乘法|`expr $a \* $b` 结果为  200。
/|除法|`expr $b / $a` 结果为 2。
%|取余|`expr $b % $a` 结果为 0。
=|赋值|a=$b 将把变量 b 的值赋给 a。
==|相等。用于比较两个数字，相同则返回 true。|[ $a == $b ] 返回 false。
!=|不相等。用于比较两个数字，不相同则返回 true。|[ $a != $b ] 返回 true。

#### 关系运算符

运算符|说明|举例
--|--|--
-eq|检测两个数是否相等，相等返回 true。|[ $a -eq $b ] 返回 false。
-ne|检测两个数是否不相等，不相等返回 true。|[ $a -ne $b ] 返回 true。
-gt|检测左边的数是否大于右边的，如果是，则返回 true|[ $a -gt $b ] 返回 false。
-lt|检测左边的数是否小于右边的，如果是，则返回 true。|[ $a -lt $b ] 返回 true。
-ge|检测左边的数是否大于等于右边的，如果是，则返回 true。|[ $a -ge $b ] 返回 false。
-le|检测左边的数是否小于等于右边的，如果是，则返回 true。|[ $a -le $b ] 返回 true。

#### 布尔运算符

运算符|说明|举例
--|--|--
!|非运算，表达式为 true 则返回 false，否则返回 true。|[ ! false ] 返回 true。
-o|或运算，有一个表达式为 true 则返回 true。|[ $a -lt 20 -o $b -gt 100 ] 返回 true。
-a|与运算，两个表达式都为 true 才返回 true。|[ $a -lt 20 -a $b -gt 100 ] 返回 false。

#### 逻辑运算符

运算符|说明|举例
--|--|--
&&|逻辑的 AND|[[ $a -lt 100 && $b -gt 100 ]] 返回 false
\|\||逻辑的 OR|[[ $a -lt 100 \|\| $b -gt 100 ]] 返回 true

#### 字符串运算符

运算符|说明|举例
--|--|--
=|检测两个字符串是否相等，相等返回 true。|[ $a = $b ] 返回 false。
!=|检测两个字符串是否相等，不相等返回 true。|[ $a != $b ] 返回 true。
-z|检测字符串长度是否为0，为0返回 true。|[ -z $a ] 返回 false。
-n|检测字符串长度是否不为 0，不为 0 返回 true。|[ -n "$a" ] 返回 true。
$|检测字符串是否为空，不为空返回 true。|[ $a ] 返回 true。

#### 文件测试运算符

运算符|说明|举例
--|--|--
-b file|检测文件是否是块设备文件，如果是，则返回 true。|[ -b $file ] 返回 false。
-c file|检测文件是否是字符设备文件，如果是，则返回 true。|[ -c $file ] 返回 false。
-d file|检测文件是否是目录，如果是，则返回 true。|[ -d $file ] 返回 false。
-f file|检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。|[ -f $file ] 返回 true。
-g file|检测文件是否设置了 SGID 位，如果是，则返回 true。|[ -g $file ] 返回 false。
-k file|检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。|[ -k $file ] 返回 false。
-p file|检测文件是否是有名管道，如果是，则返回 true。|[ -p $file ] 返回 false。
-u file|检测文件是否设置了 SUID 位，如果是，则返回 true。|[ -u $file ] 返回 false。
-r file|检测文件是否可读，如果是，则返回 true。|[ -r $file ] 返回 true。
-w file|检测文件是否可写，如果是，则返回 true。|[ -w $file ] 返回 true。
-x file|检测文件是否可执行，如果是，则返回 true。|[ -x $file ] 返回 true。
-s file|检测文件是否为空（文件大小是否大于0），不为空返回 true。|[ -s $file ] 返回 true。
-e file|检测文件（包括目录）是否存在，如果是，则返回 true。|[ -e $file ] 返回 true。

### 流程控制

#### 条件判断 if else
```
1、单if写法

if condition
then
   command1
   ...
   commandN
fi

2、if...else...写法

if condition
then
   command1
   ...
   commandN
else
   command
fi

3、if...else if...写法

if condition
then
   command1
elif condition2
then
   command2
else
   commandN
fi
```

#### 循环 for
```
for var in item1 item2 ... itemN
do
   command1
   ...
   commandN
done
```

#### 循环 while
```
while condition
do
   command
done

无限循环①
while :
do
   command
done

无限循环②
while true
do
   command
done
```
>使用break命令跳出循环，使用continue命令跳过当前循环

