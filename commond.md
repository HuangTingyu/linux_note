## 快捷键

`ctrl + l` —— 清空屏幕

进入文件后，记得按下`Esc`

`Home` —— 行首

`end` —— 行尾

`num `+`gg` ，例如 `5gg` 可以跳到第五行行头

## 查询文件

### ls

显示目录文件信息，格式为 `ls [选项][文件]`

`-l` 参数可以查看 `文件` 的属性，大小等详细信息；

`ls -l` 相当于 `ll` ，显示文件信息；

`-a` 参数看到全部 `文件` ；

`-d` 参数可以查看 `目录` 权限与属性信息；

常用命令 ——

1.查看所有文件和文件属性

```shell
ls -al
```

2.查看目录属性

```shell
ls -ld /etc
```

3.查看根目录

```shell
ls /
```

### tree

查看文件目录。

查看虚拟机中，所有目录的层级

```shell
tree /
```

### pwd

`pwd -P`

显示当前目录

### cd

1. `cd -` 返回上一次所处的目录
2. `cd ..` 返回到上一级目录
3. `cd ~` 返回根目录

### more

查看长文件，格式为 `more [选项] 文件`

`-n` 可以显示行数

翻页 —— 按空格或者回车

下面的例子，翻页查看 `etc` 目录下面的文件信息

```shell
ll /etc/ | more
```

### head

查看纯文本的 `前` n行，格式 `head [选项][文件]`

```shell
head -n 20 initial-setup-ks.cfg
```

### tail

查看纯文本的 `后 ` n行，以及持续刷新的内容，格式 `tail [选项][文件]`

查看持续刷新的内容 `tail -f 文件名`

### cat

用于查看比较短的纯文本，会一口气拉所有东西，慎用！

格式 `cat [选项] [文件]`

`-n` —— 显示行号

`-A` —— 显示换行符和制表符

## 编辑文件

### vim

vim进入文件以后，按下`Esc` ，然后 `:set nu` ，显示行号。

### 编辑操作

#### 字符

`i` —— 光标  `前` 插入 `字符`

`a` —— 光标 `后` 插入 `字符`

`r` —— 替换当前光标所在的`字符` ，先按`r` ，然后输想替换的东西

#### 行(先esc退出)

`o` —— 光标 `下` 插入新 `行`

`yy` —— 复制一行，3yy(复制行，当前行往下2行)，yG(当前行以下全部复制)

`p` —— 粘贴一行

`dd` —— 删除一行，3dd(删除下面3行)，dG(当前行及以下全部删除)

`shif` + d —— 删除光标到行尾的内容

#### 撤回(先esc退出)

`u` —— 撤销

`ctrl` + `r` —— 取消撤销操作

#### 可视化

`ctrl` + `v` —— 批量操作

#### 批量插入

`ctrl`+`v` ，`gg` 跳转行，然后 `shift` + `i` ，插入完毕以后，连按两次`Esc`

#### 批量删除

`ctrl`+`v` ，`gg` 跳转行，然后 `x` 

## 操作文件

### cp

复制文件或目录，格式为 `cp [选项] 源文件 目标文件`

```shell
touch install.log
cp install.log x.log
```

目录下会出现，`install.log` 和 `x.log` 两个文件。

### mv

mv用于剪切文件或将文件重命名，格式为 `mv [选项] 源文件 [目标路径|目标文件名]`

如果对同一个目录进行剪切操作，相当于重命名

```shell
mv x.log linux.log
```

### find

查找含有host关键字的文件

```shell
find /etc -name "host*" -print
```

`-name` —— 匹配名称

`-user` —— 匹配所有者

`- exec {} \` —— 后面可跟用于进一步处理搜索结果的命令

```shell
find / -user linuxprobe -exec cp -a {} /root/findresults/\;
```

### grep

用于在文本中执行关键词搜索，并匹配搜索结果，格式为 `grep [选项] [文件]`

`-n` —— 用来显示行号

`-v` —— 用于反选信息，即没有包含关键词的信息行

一旦用户的登录端被设置为 `/sbin/nologin`，即不能登录

下面的指令即，在文件 `etc/passwd` 中搜索含有 `/sbin/nologin` 的用户信息。

```shell
grep /sbin/nologin /etc/passwd
```

### tr

用于替换文本中的字符，格式为 `tr [原始字符] [目标字符]`

例如把小写替换为大写

```shell
cat anaconda-ks.cfg | tr [a-z][A-Z]
```

### mkdir

`-p` 可以用来创建具有层级关系的文件夹

例如

```shell
mkdir -p a/b/c/d/e
```

### tar

解压，格式为 `tar [选项] [文件]`

`-c` 创建压缩文件

`-x` 解开压缩文件

`-t` 查看压缩包内的文件

`-z` 用Gzip压缩或解压

`-v` 显示压缩或解压过程

`-f` 目标文件名

#### 打包

常见打包命令 —— `tar -czvf 压缩包名称.tar.gz 要打包的目录`

打包etc文件夹，打包文件命名为 etc.tar.gz

```
tar -czvf etc.tar.gz /etc
```

打包完输入一下，ls，可以看到etc.tar.gz

#### 解压

常用解压命令 —— `tar -xzvf 压缩包名称 -C 指定目录`

把压缩包指定解压到 `/root/etc` 目录中

```
tar xzvf etc.tar.gz -C /root/etc
```

## 统计行数

### wc

常用命令 —— `wc [参数] 文本`

`-l` 显示行数

`-w` 显示单词数

`-c` 显示字节数

显示有多少个用户

```shell
wc -l /etc/passwd
```

## 进程/系统

### ps

可以查看系统中进程的状态。

常用命令

```shell
ps aux
```

### wget

下载，格式为  `wget [参数] 下载地址`

`-p` 下载到指定目录

`-r` 递归下载

递归下载 `www.linuxprobe.com` 网页内所有数据以及文件，保存到当前路径到 `www.linuxprobe.com` 文件夹中。

```shell
wget -r -p http://www.linuxprobe.com
```

## 管道符 `|`

管道符，执行格式 `命令A |命令B`，管道符作用，把命令A的输出结果，当做命令B的输入。

统计不能登录的用户数目

```shell
grep "/sbin/nologin" /etc/passwd | wc -l
```

