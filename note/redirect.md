## 重定向

1.命令 < 文件

将文件作为命令的标准输入

2.命令 << 分界符

从标准输入中读入，知道遇见分界符才停止

3.命令 > 文件

将标准输出重定向到一个文件中(清空，全文本覆盖)

4.命令 >> 文件

将标准输出重定向到一个文件中(追加)

5.命令 &>> 文件

将标准输出与错误共同写入文件中(追加)

### 管道

对于不必要跟参数的命令(如rm -rf，cp等)，可以通过 `xargs` 传递参数

1. `files.txt` 里面的内容如下所示，请问如何通过管道，把这些文件都删除？

```
/home/file1 
/home/file2
/home/file3 
/home/file4
/home/file
```

关键，使用参数 `xargs` 

```shell
cat files.txt |xargs rm -rvf
```

2. `files.txt` 同第一题，请问如何通过管道，把这些文件都复制到tmp目录下？

```shell
cat files.txt |xargs -I {} cp {} /tmp
```

`-I` 是暂存的意思，把cat的输出暂存到 `{}` 里面，

`cp {} /tmp` ，这里使用的 `{}` ，就是前面通过 `-I` 暂存的东西

## rz

下载 `lrzsz`，然后可以使用 `rz` 命令，上传压缩包。

## 安装mysql

注意：

1.安装 `gcc*`，以及 `ncurses-devel`

2.每次报错的时候，`rm -f CMakeCache.txt`

3.环境变量的错误，请检查，肯定是下面的错了

```shell
cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql -DMYSQL_DATADIR=/mysql/data -DDEFAULT_CHARSET=utf8 -DEXTRA_CHARSETS=all -DDEFAULT_COLLATION=utf8_general_ci -DWITH_SSL=system -DWITH_EMBEDDED_SERVER=1 -DENABLED_LOCAL_INFILE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DENABLE_DOWNLOADS=1 -DWITH_SSL=bundled
```

