### 安装

1.先下载vmware，新建虚拟机，选择一个空白的虚拟机(最后一个选项)，然后选择linux，32位的CentOS(64位存在兼容性问题)。

2.VMware_Install_Cleaner —— 用于解决虚拟机没有删除干净的问题。

### 网络连接

1.Bridged桥接 —— 选择桥接以后，不仅可以和本地通信，也可以跟网段内的其他机器通信。

2.NAT —— 如果虚拟机装在自己的电脑上，开启NAT，网速就跟自己的电脑一样。

3.Host-only —— 虚拟机不能上网，虚拟机只能跟自己的电脑通信。

### 快照

1. Take a snapshot 快照 —— 保存当前设置。
2. Manage snapshots 管理快照 —— 可以把系统还原到，任何一个快照的状态。

### 安装linux

操作注意：虚拟机没有关机的情况下，不要点右上角直接叉掉，否则虚拟机会崩溃。

1.磁盘选项 ——

Allow one all disk space now —— 允许使用一整块磁盘

store virtual disk as a single file ——  将虚拟磁盘存储为单个文件(文件利用率低)

split virtual disk into multiple files —— 将虚拟磁盘拆成多个文件(推荐，文件利用率高)

2.图形界面选项 ——

GNOME Desktop

注意：记得打开网卡，有个选项可以打开网卡 —— NETWORK & HOST NAME

3.记得调整一下时区

### 概念

### 分区类型

1.主分区：最多只能有4个

2.扩展分区：

最多只能有1个；主分区加扩展分区最多有4个；不能写入数据，只能包含逻辑分区；

#### linux格式化

把整个分区分成等大小的数据块，在分区列表里面建立二维表格，二维表格记录了每个文件的ID (I Node) ，修改时间，权限，文件的保存位置。格式化，为了写入文件系统。

### 文件

linux中，一切皆文件。

“`/`” 表示根目录，

### 挂载(相当于windows系统的盘符)

#### 必须分区

1. “`/`” (根分区)

根分区是挂载点。如果类比windows 根分区概念就相当于系统盘，分区类型不会说是系统盘和非系统盘。

1. swap分区 (交换分区，内存2倍，不超过2GB)

内存4GB以内，swap分区应该是内存的2倍；

4GB以上，swap分区，应该跟内存一样大。

#### 推荐分区

“`/boot`” (启动分区，单独分区，200MB)

如果不单独分出来，一旦分区写满，将不能启动系统。

### 分区总结

1.分区 —— 把大硬盘分为小的逻辑分区

2.格式化 —— 写入文件系统

3.分区设备文件名 —— 给每个分区定义设备分件名

4.挂载 —— 给每个分区分配挂载点

常用分区：主分区，扩展分区，逻辑分区

