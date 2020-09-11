# Linux常用服务

## 定时计划任务
> `crontab` 定时任务的守护进程，精确到分。是用来让使用者在固定时间或固定间隔执行程序之用，换句话说，也就是类似使用者的时程表。

### 使用方式

- 语法：
   - `crontab [-u user] file`
   - `crontab [-u user] {-l | -r | -e}`
- 参数：

参数值|参数作用
--|--
-u user|是指设定指定 user 的时程表，这个前提是你必须要有其权限(比如说是 root)才能够指定他人的时程表。如果不使用 -u user 的话，就是表示设定自己的时程表
-e|执行文字编辑器来设定时程表
-r|删除目前的时程表
-l|列出目前的时程表
file|使用者也可以将所有的设定先存放在文件中，用 crontab file 的方式来设定执行时间

### 实例
```
每一分钟执行一次 /bin/ls
* * * * * /bin/ls

在 12 月内, 每天的早上 6 点到 12 点，每隔 3 个小时 0 分钟执行一次 /usr/bin/backup
0 6-12/3 * 12 * /usr/bin/backup

周一到周五每天下午 5:00 寄一封信给 alex@domain.name
0 17 * * 1-5 mail -s "hi" alex@domain.name < /tmp>

每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分....执行 echo "haha"
20 0-23/2 * * * echo "haha"
```

### 问题排查

- 程序自动执行后收到邮件
   - 在命令结尾加上`> /dev/null 2>&1` 来避免接收到邮件
- 脚本无法正常执行
   - 将所有命令写成结对路径形式，如`/usr/local/bin/docker`
   - 在Shell脚本开头使用以下代码

   ```
   #!/bin/sh
   . /etc/profile
   . ~/.bash_profile
    ```

   - 在/etc/crontab中添加环境变量，即在可执行命令之前添加命令/etc/profile;/bin/sh    
   `20 03 * * * . /etc/profile;/bin/sh /var/www/runoob/test.sh`


---

## 共享存储 NFS
>NFS 是 Network FileSystem 的缩写，顾名思义就是网络文件存储系统，它最早是由 Sun 公司发展出来的，也是 FreeBSD 支持的文件系统中的一个，它允许网络中的计算机之间通过 TCP/IP 网络共享资源。通过 NFS，我们本地 NFS 的客户端应用可以透明地读写位于服务端 NFS 服务器上的文件，就像访问本地文件一样方便。简单的理解，NFS 就是可以透过网络，让不同的主机、不同的操作系统可以共享存储的服务。

### 安装

- 确认当前安装情况 `rpm -qa nfs-utils rpcbind`

- 安装服务端 `yum install -y nfs-utils rpcbind`

- 仅安装客户端 `yum install -y nfs-utils`

### 配置

- 创建一个目录作为共享目录 `mkdir -p /data/share`
- 修改/etc/exports来开放共享目录 `vim /etc/exports`

#### 配置实例
```
将/data/share文件目录设置为允许IP为10.222.77.0/24区间的客户端挂载
/data/share 10.222.77.0/24(rw,sync,insecure,no_subtree_check,no_root_squash)
```

#### 参数说明
参数值|参数作用
--|--
ro|只读访问
rw|读写访问
sync|所有数据在请求时写入共享
async|nfs 在写入数据前可以响应请求
secure|nfs 通过 1024 以下的安全 TCP/IP 端口发送
insecure|nfs 通过 1024 以上的端口发送
wdelay|如果多个用户要写入 nfs 目录，则归组写入（默认）
no_wdelay|如果多个用户要写入 nfs 目录，则立即写入，当使用 async 时，无需此设置
hide|在 nfs 共享目录中不共享其子目录
no_hide|共享 nfs 目录的子目录
subtree_check|如果共享 /usr/bin 之类的子目录时，强制 nfs 检查父目录的权限（默认）
no_subtree_check|不检查父目录权限
all_squash|共享文件的 UID 和 GID 映射匿名用户 anonymous，适合公用目录
no_all_squash|保留共享文件的 UID 和 GID（默认）
root_squash|root 用户的所有请求映射成如 anonymous 用户一样的权限（默认）
no_root_squash|root 用户具有根目录的完全管理访问权限
anonuid=xxx|指定 nfs 服务器 /etc/passwd 文件中匿名用户的 UID
anongid=xxx|指定 nfs 服务器 /etc/passwd 文件中匿名用户的 GID

### 启动
```
启动RPC服务
service rpcbind start
（或/bin/systemctl start rpcbind.service）

查看NFS服务项rpc服务器注册的端口列表
rpcinfo -p localhost

启动NFS
service nfs start
（或/bin/systemctl start nfs.service）

查看在配置中开放的目录
showmount -e localhost
```

### 客户端挂载
```
查看可共享的目录信息
showmount -e 10.222.77.86

创建目录用于挂载
mkdir -p /share

挂载远端目录到本地/share目录
mount -t nfs 10.222.77.86:/data/share /share
```
