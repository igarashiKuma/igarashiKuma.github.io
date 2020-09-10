# Linux系统设置

## 时区设置

- 查看时区 `date -R`
- 修改时区 `tzselect`
   - 还可以直接替换时区文件
   - 还可以创建链接文件 `cp /usr/share/zoneinfo/$主时区/$次时区 /etc/localtime`

---

## 环境变量设置
>环境变量文件介绍参考[linux系统基础](/SecondWeek/LinuxBasic)
- 示例一：JDK
```
1.1 安装JDK
cd /opt/softwares
tar zxvf jdk-8u131-linux-x64.tar.gz -C ..

1.2 编辑/etc/profile
export JAVA_HOME=/opt/jdk1.8.0_131
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=./:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$PATH

1.3 使配置生效
source /etc/profile 

1.4 验证
java -version与echo $JAVA_HOME
```
- 示例二：修改用户最大文件打开数
```
2.1 临时修改
ulimit -HSn 65535

2.2 永久修改
vi /etc/security/limits.conf

修改对应内容为：
* soft nofile 65535
* hard nofile 65535
```
---

## 修改内核设置
- 打开配置文件：`vim /etc/sysctl.conf`
- 参数项说明：

参数名称|含义
--|--
net.ipv4.tcp_syncookies=1|开启SYNCookies。当出现SYN等待队列溢出时，启用cookies来处理，可防范少量SYN***，默认为0，表示关闭
net.ipv4.tcp_tw_reuse=1|开启重用。允许将TIME-WAIT sockets重新用于新的TCP连接，默认为0，表示关闭
net.ipv4.tcp_tw_recycle=1|开启TCP连接中TIME-WAIT sockets的快速回收，默认为0，表示关闭
net.ipv4.tcp_fin_timeout=30|系統默认的TIMEOUT时间

---

## 故障排除

- 磁盘
   - df -h
- 内存
   - free -m
- 进程
   - ps -ef | grep XXX
- 端口侦听情况
   - netstat -tunlp | grep xxx
   - telnet ip port
- 系统负载
   - top
   - vmstat 3 10