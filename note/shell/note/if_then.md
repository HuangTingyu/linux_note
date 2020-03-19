## 判断与控制

### if-then-else

```shell
if command | condition
then
    commands1
elif command | condition
then
    commands2
else
	commands3
fi
```

如果 command 的退出状态码为0，则会执行commands1语句。否则进入elif部分，退出状态码为0执行commands2语句，否则执行commands3

换种写法

```
if command | condition;then
    commands1
elif command | condition;then
    commands2
else
	commands3
fi
```

#### 例子1

```
if pwd
then
  echo "running"
fi
```

输出

```
running
```

#### 例子2

`ch3_1.sh`

```
# ! /bin/bash
#

if ps -ef | grep sshd | grep -v grep &> /dev/null
then
   echo "SSH is running"
else
   echo "SSH  stopped"
fi

```

解释 ——

`&> /dev/null` 是把 `ps -ef | grep sshd | grep -v grep` 的输出结果，重定向到垃圾桶。但是，不会改变`ps -ef | grep sshd | grep -v grep` 的运行状态码。

### 数值比较

```
n1 -eq n2	=
n1 -ne n2	≠
n1 -gt n2	>
n1 -ge n2	≥
n1 -lt n2   <
n1 -le n2	≤
```

#### 例子3

注意空白，中括号前后都要空格，不然会报错。

`ch3_4.sh`

```
# ! /bin/bash

if [ $1 -eq $2 ];then
   echo "$1 equal $2"
elif [ $1 -gt $2 ];then
   echo "$1 grater than $2"
elif [ $1 -lt $2 ];then
   echo "$1 less than $2"
fi

```

测试

```
sh ch3_4.sh 34 34
```

输出

```
34 equal 34
```

### 字符串比较

```
str1 = str2 相等
str1 != str2 不等
```

下面按照字母表的顺序，从第一个字符依次比较

```
str1 < str2 str1小于str2时，为true
str1 > str2 str1大于str2时，为true
```

判断字符串长度

```
-n str1 str1长度不为0, true
-z str1 str1长度为0, true
```

#### 例子4 判断等与不等

```
# ! /bin/bash
#

str1="Dear"
str2="dlrb"

if [ $str1 != $str2 ];then
   echo "equal"
else
   echo "not equal"
fi

```

#### 例子5 判断字符串大小(不常用)

注意小于号前面要加个转义符 `\` ，不然小于号会被识别为重定向。

```
# ! /bin/bash
#

str1="string"
str2="compare"

if [ "$str1" \< "$str2" ];then
   echo "$str1<$str2"
else
   echo "$str1>$str2"
fi
```

输出

```
string>compare
```

#### 例子6 判断空字符串

```
# ! /bin/bash
#

str1=""
str2="compare"

if [ -n "$str1" ];then
   echo "String exists"
else
   echo "Empty string"
fi

```

注意，这里的双引号

```
if [ -n "$str1" ];then
```

以及双引号，与 `$str1` 之间不要存在空格，不然就会报错。

### 文件判断

```
-d file file是否为目录
-f file file是否为文件
-e file file是否存在
-r file file是否可读
-w file file是否可写
-x file file是否可执行
```

文件比较

```
-s file file存在且非空
file1 -nt file2 str1大于str2为true
file1 -ot file2 str1长度不为0为true
```

高频 —— `-d` , `-f`

#### 例子7 判断是否为目录

```
# ! /bin/bash
#

if [ -d /usr/bin ];then
   echo "catalog"
else
   echo "It's not catalog"
fi

```

#### 例子8 判断文件是否为空

注意空格什么的，不要多打不要少打！

```
# ! /bin/bash
#

if [ -s /root/ch3_6_2.sh ];then
   echo "yes"
else
   echo "no"
fi
```

### 与或非

```
if condition1 && condition2
```

```
if condition1 || condition2
```

#### 例9 与或非

```
# ! /bin/bash
#

num1=520
num2=1314
num3=3344

if [ $num1 -lt $num2 ] && [ $num2 -lt $num3 ];then
   echo "Dear-dlrb"
else
   echo "sorry"
fi

```

