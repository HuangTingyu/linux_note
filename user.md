## 用户

### 查询系统所有用户信息

```shell
cat /etc/passwd
```

### 查看用户

```shell
id bacra
```

### 创建用户

```shell
useradd bacra
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

