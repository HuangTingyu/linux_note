## 用户

### 查询系统所有用户信息

```shell
cat /etc/passwd
```

### 查看用户

```shell
id bacra
```

出现 `bacra:x:1005:1008` ，这里面1005是uid，1008是组的id，也就是gid

### 创建用户

```shell
useradd bacra
```

### 用户相关目录

- `/etc/passwd` —— `gz:x:1005:1008`
- `/etc/group` —— `gz:x:1008`
- `/etc/shadow` —— `gz:!!:1838:0:...`
- `/home` 
- `/var/mail`

注意，uid，gid不要和其他的冲突

1.先进/etc/passwd里面，复制一行，然后改用户名，uid和gid(区别其他行，不然会冲突)

`user05:x:8083:8083::/home/user04:/bin/bash`

2.进/etc/group里面，复制一行，把gid改成上面的gid

`user05:x:8083:`

3.进/etc/shadow里面，复制一行，把组名改成用户的组名

`user05`:!!:18179:0:99999:7:::

4.进入/home里面，创建`user05`

```shell
mkdir user05 #ll查看下，此时user05是root权限
chown user05.user05 user05 #ll查看下，此时user05权限改了
```

5.进入/var/mail，创建`user05` ，重复上面的操作

```shell
mkdir user05 #ll查看下，此时user05是root权限
chown user05.user05 user05 #ll查看下，此时user05权限改了
```

## 组

### 查看组

```shell
cat /etc/group
```

### 查看组里有哪些成员

```shell
 cat /etc/group | grep IT
```

### 管理组(gpasswd)

`-a` —— 添加用户到组

`-d` ——从组删除用户

### 修改密码

允许用户修改密码

```
echo "123" | passwd --stdin user02
```

## 权限

#### chmod

改变用户的权限

-rwxrw-r-- 解析

第一个 `-` 是文件类型，表示该文件是普通文件

`rwx` 表示用户(u)的权限为读，写，执行，4+2+1 = 7

`rw-` 表示组(g)的权限是，读，写

`r--` 表示其他人(o)的权限是读

- 增加权限 —— `chmod u+x file.sh`
- 回收权限 —— `chmod u-x file.sh`
- 使用数字 —— `chmod 777 file.sh`

注意下面的例子：

tom是否能写入tom.txt？

```shell
chmod 464 /tmp/tom.txt
chmod tom.tom /tmp/tom.txt
```

判断规则，先判断所有者，因为tom是所有者，所以

#### chown

改变文件所属的组 `chown bacra.bacra file1.txt`

### setfacl

应用场景 —— 文件chmod的x权限被去掉的时候，可以用setfacl去赋予写权限

针对特定的用户，赋予权限

`-m` —— 针对普通用户

`-x` —— 删除特定用户的权限(用法同 ` -m` )

`-R` —— 递归参数

`-b` —— 删除文件所有的ACL

`u:` + 用户

`g:` + 组

1.加权限

```shell
setfacl -m u:bacra:rw /home/test.txt
```

2.剥掉权限

```shell
setfacl -x u:bacra /home/test.txt
```

### umask

一般不要去动这个东西

```
umask 
```

输出 —— 0002

这代表文件创建的时候，会默认给权限664，也就是(rw-rw-r--)，目录创建的时候，会默认给775。

这个的计算原理是这样的，文件一般默认是给(666)，设置了unmask以后，就是(rw-rw-r--)去掉002(-------w-)，那就是(rw-rw-r--)。目录默认是给(777)，同理(rwxrwxrwx)去掉(-------w-)，那就是(rw-rw-r-x)

### su

切用户 `su - bacra`

如果不加 `-` ，一些属性不会跟着切过去

### sudo

普通用户使用 root 权限

1. `visudo` 进入配置文件
2. 添加配置信息

```shell
bacra ALL=(ALL) ALL
root ALL=(ALL) ALL
```

 3.然后，sudo + 命令，就可以使用原来没有权限的指令。

### 注意

1.文件x权限小心给，目录w权限小心给

2.当目录给了w权限以后，普通用户也可以强制修改目录下的文件





