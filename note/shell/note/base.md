## shell学习笔记

### 环境搭建

详细见 —— `linux_note\note\docker\base.md`

使用vagrant和virtualBox，先把centos7启动

通过 `vagrant ssh-config` 查到主机号`127.0.0.1` ，端口号`2222` ，然后，xshell连接到虚拟机。

用户名 `vagrant` ，密码选择 —— `Vagrant\centos7\.vagrant\machines\default\virtualbox\private_key` 

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

