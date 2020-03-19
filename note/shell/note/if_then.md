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





