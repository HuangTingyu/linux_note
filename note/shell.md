第一个 `shell` 脚本 —— vim example.sh

```shell
# ! /bin/bash
# For Example BY linuxprobe.com
pwd
ls -al
```

第一行脚本声明 `# !` 用来告诉系统使用哪种shell解释器来执行

第二行脚本声明 `#` 是对脚本功能和命令的介绍

### 接受用户的参数

`$0` —— 对应的是当前Shell脚本程序的名称

`$#` —— 对应的是总共有几个参数

`$*` —— 对应的是所有位置的参数值

`$?` —— 显示的上一次命令的返回值

`$1` ,...,`$n` —— 代表的是第1，第2，...，直到第n个参数

### 判断用户的参数

文本测试，指定条件判断文本是否存在或者是否满足条件

`-d` 文件是否为 目录

`-e` 文件是否存在

`-f` 是否为一般文件

`-r` 读取权限

`-w` 写入权限

示例 —— 

判断文件是否为目录，0表示是，1表示否

```shell
[ -d /etc/passwd ]
echo $?
```

可以用&& (且)，命令执行成功，即执行&&后面的语句

```shell
[ -e /etc/passwd ] && echo "yes"
```

结合系统变量USER，判断当前用户是否为管理员，如果不是就输出"no"

```shell
echo $USER
[ $USER = root ] || echo "no"
```

上面两条命令可以合起来

```shell
[ $USER = root ] && echo "yes" || echo "no"
```

## 整数比较运算符

`-lt` 小于

`-le` 小于等于

`ge` 大于等于

`-eq` 等于

`-ne` 不等于

`gt` 大于

示例，判断内存，小于1024M的时候输出，insufiiciten Memory

```
FreeMem=`free -m | grep Mem | awk '{print $4}'
[ $FreeMem -lt 1024 ] && echo "insufiiciten Memory" || echo "adequate"
```

