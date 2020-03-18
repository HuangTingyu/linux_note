## shell学习笔记

### 环境搭建

详细见 —— `linux_note\note\docker\base.md`

使用vagrant和virtualBox，先把centos7启动

通过 `vagrant ssh-config` 查到主机号`127.0.0.1` ，端口号`2222` ，然后，xshell连接到虚拟机。

用户名 `vagrant` ，密码选择 —— `Vagrant\centos7\.vagrant\machines\default\virtualbox\private_key` 

xshell 参考链接 —— <https://blog.csdn.net/lxmsc612109/article/details/85265635>

### 日常开机

xshell

```
cd C:\Users\hty\Vagrant\centos7
vagrant up
```

然后创建连接，秘钥保存在

```
C:\Users\hty\Vagrant\centos7\.vagrant\machines\default\virtualbox
```

### 切换root用户

```
sudo -i
```

### 自定义变量

1.变量由字母，数字，下划线组成，不能以数字开头

2.区分大小写，Var1不等于var1

3.变量、等号、值中间不能出现空格！

下面这种写法是会报错的！

```
var1 = 112
```

4.如果文本之间有空格，应该用双引号包起来

```
#! /bin/bash
#

var1=dlrb
var2="i love you so much"

echo $var1
echo $var2

```

运行shell脚本

```
sh ch2_1.sh
```

### 位置变量

当一条命令或脚本执行时，后面可以跟多个参数，使用位置参数来表示这些参数。

`$n` —— n为数字，`$0`代表脚本，`$1-$9` 代表1-9个参数，10以上的参数需要大括号，如`${10}`

`$@` —— 命令行所有参数，每个参数区别对待

`$*` —— 命令行所有参数，所有参数视为一个整体

`$#` —— 参数个数

#### 例子1 ——

```
# ! /bin/bash
#

echo "The first blood: $1"
echo "The second blood: $2"
echo "The third blood: $3"

echo $*
echo $@
echo $#
```

输入

```
sh ch2_2.sh Dear dlrb
```

输出

```
The first blood: Dear
The second blood: dlrb
The third blood: 
Dear dlrb
Dear dlrb
2
```

#### 例子2 ——

`ch2_2_2.sh`

```
# ! /bin/bash
#

function add
{
  value=`expr $1 + $2`
  echo $value

}

add $1 $2

```

输入

```
sh ch2_2_2.sh 123 456
```

输出

```
579
```

### 环境变量

1.对所有用户生效的环境变量 `/etc/profile`

2.对特定用户生效的环境变量 `~/.bashrc` 或者 `~/.bash_profile`

3.临时有效的环境变量 脚本或命令行使用 export

#### 例子1 ——

不同的用户，输出的环境变量不同。

```
[root@localhost ~]# echo $HOME
/root
[root@localhost ~]# su - vagrant
Last login: Tue Mar 17 11:28:57 UTC 2020 from 10.0.2.2 on pts/0
[vagrant@localhost ~]$ echo $HOME
/home/vagrant
```

#### 常用环境变量

PATH —— 命令搜索的路径

HOME —— 用户家目录路径

LOGNAME —— 用户登录名

PWD —— 当前所在路径

HISTFILE —— 历史命令的保存文件

HISTSIZE —— 历史命令保存的最大行数

分割线 ————————————————————————

HOSTNAME —— 主机名

SHELL —— 用户当前使用的SHELL

PS1 —— 一级命令提示符

TMOUT —— 用户和系统交互过程的超时值

IFS —— 系统输入分隔符

OFS —— 系统输出分隔符

### 管道

#### 需求1

列出系统所有的软件包，搜索python相关的软件包

#### 解决1.重定向 

1.查找所有软件包，重定向到一个文件

```
rpm -qa > all_soft.txt
```

2.查文件信息，以及文件行数

```
ll all_soft.txt
wc all_soft.txt
```

3.查找文件中，python相关的

```
vim all_soft.txt
```

#### 解决2.管道

前一行命令的输出，作为输入交给下一个命令

```
rpm -qa | grep python | wc -l
```

### 退出状态码

1.shell命令使用退出码告知shell，它已经执行完毕

2.退出码是一个0-255的整数

3.Linux提供了一个 `$?` 捕获退出状态码

总结 ——

0 命令运行成功

其他状态码 命令运行不成功

#### 使用场景1

判断命令是否执行成功

```js
date

if [ $? -eq 0 ];then
   echo "success..."
else
   echo "failed by status code $?"
fi

```

中括号里的东西，是判断语句，如果状态码等于0，就输出

```
sucess...
```

#### 使用场景2

判断进程是否存在

```
ps -ef | grep nginx | grep -v grep
```

或者

```
ps -ef | grep sshd | grep -v grep
```

再输入

```
echo $?
```

如果输出1，代表进程不存在，输出0，代表进程存在

