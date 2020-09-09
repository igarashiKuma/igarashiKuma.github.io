# Linux基础

## 路径

### 绝对路径
>从根目录开始，依次将各级子目录的名字组合起来形成的路径

### 相对路径
>相对当前所在路径的位置的路径

### 特殊符号

- .
>用户所处当前目录

- ..
>当前目录的上级目录

- ~
>当前用户的家目录

## 系统文件

### etc/profile
- 定义Linux系统变量   
- 修改后需要source etc/profile来生效

### ~/.bash_profile

- 定义用户换机变量
- 修改后需要source ~/.bash_profile来生效

### ~/.bashrc

- 定义用户环境变量、别名等
- 修改后需要source ~/.bashrc来生效

### /etc/sysctl.conf

- 定义内核配置
- 修改后需要sysctl -p使其生效

### /etc/rc.local

- 定义开机启动后执行的动作

### /etc/security/limits.conf

- 限制用户对于文件、线程、内存等资源的最大使用量

## 常用命令

### cd 切换目录
- 用法：
```
cd /opt
```

### ls 列出当前目录下内容
- 语法：`ls [-options] [name...]`
- 参数：

参数值|参数作用
--|--
-a|显示所有文件及目录 (ls内定将文件名或目录名称开头为"."的视为隐藏档，不会列出)
-l|除文件名称外，亦将文件型态、权限、拥有者、文件大小等资讯详细列出
-r|将文件以相反次序显示(原定依英文字母次序)
-t|将文件依建立时间之先后次序列出
-A|同 -a ，但不列出 "." (目前目录) 及 ".." (父目录)
-F|在列出的文件名称后加一符号；例如可执行档则加 "*", 目录则加 "/"
-R|若目录下有文件，则以下之文件亦皆依序列出

### rm 删除
- 语法：`rm [-options] [name...]`
- 参数：

参数值|参数作用
--|--
-i|删除前逐一询问确认
-f|即使原档案属性设为唯读，亦直接删除，无需逐一确认
-r|将目录及以下之档案亦逐一删除

### cp 复制
- 语法：
   - `cp [-options] [source] [dest]`
   - `cp [-options] [source...] [directory]`
- 参数：

参数值|参数作用
--|--
-a|此选项通常在复制目录时使用，它保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合
-d|复制时保留链接。这里所说的链接相当于Windows系统中的快捷方式 
-f|覆盖已经存在的目标文件而不给出提示。
-i|与-f选项相反，在覆盖目标文件之前给出提示，要求用户确认是否覆盖，回答"y"时目标文件将被覆盖。
-p|除复制文件的内容外，还把修改时间和访问权限也复制到新文件中
-r|若给出的源文件是一个目录文件，此时将复制该目录下所有的子目录和文件。
-l|不复制文件，只是生成链接文件

### cat 查看文件所有内容
- 用法：
```
 cat /opt/test.log
```

### more 查看文件所有内容，空格翻页
- 语法：`more [-options] [-num] [+/pattern] [+linenum] [fileNames..]`
- 参数：

参数值|参数作用
--|--
-num|一次显示的行数
-d|提示使用者，在画面下方显示 [Press space to continue, 'q' to quit.] ，如果使用者按错键，则会显示 [Press 'h' for instructions.] 而不是 '哔' 声
-l|取消遇见特殊字元 ^L（送纸字元）时会暂停的功能
-f|计算行数时，以实际上的行数，而非自动换行过后的行数（有些单行字数太长的会被扩展为两行或两行以上）
-p|不以卷动的方式显示每一页，而是先清除萤幕后再显示内容
-c|跟 -p 相似，不同的是先显示内容再清除其他旧资料
-s|当遇到有连续两行以上的空白行，就代换为一行的空白行
-u|不显示下引号 （根据环境变数 TERM 指定的 terminal 而有所不同）
+/pattern|在每个文档显示前搜寻该字串（pattern），然后从该字串之后开始显示
+num|从第 num 行开始显示
fileNames|欲显示内容的文档，可为复数个数

### tail 尾部查看文件内容
- 语法：`tail [-options] [fileName]`
- 参数：

参数值|参数作用
--|--
-f|循环读取 
-q|不显示处理信息 
-v|显示详细的处理信息 
-c<数目>|显示的字节数 
-n<行数>|显示文件的尾部 n 行内容 
--pid=PID|与-f合用,表示在进程ID,PID死掉之后结束 
-q, --quiet, --silent|从不输出给出文件名的首部 
-s, --sleep-interval=S|与-f合用,表示在每次反复的间隔休眠S秒 

### head 头部查看文件内容
- 语法：`head [-options] [fileName]`
- 参数：

参数值|参数作用
--|--
-q|隐藏文件名 
-v|显示文件名 
-c<数目>|显示的字节数
-n<行数>|显示的行数

### mkdir 创建目录
- 语法：`mkdir [-p] dirName`
- 参数：

参数值|参数作用
--|--
-p|确保目录名称存在，不存在的就建一个

### chown 更改所属
- 语法：`chown [-cfhvR] [--help] [--version] user[:group] file...`
- 参数：

参数值|参数作用
--|--
user|新的文件拥有者的使用者 ID
group|新的文件拥有者的使用者组(group)
-c|显示更改的部分的信息
-f|忽略错误信息
-h|修复符号链接
-v|显示详细的处理信息
-R|处理指定目录以及其子目录下的所有文件
--help|显示辅助说明
--version|显示版本

### chmod 更改权限
```
r(Read，读取)：对文件而言，具有读取文件内容的权限；对目录来说，具有浏览目录信息的权限
w(Write,写入)：对文件而言，具有新增,修改 文件内容的权限(但不含删除该文件)；对目录来说，具有新建，删除，修改，移动目录内文件的权限
x(eXecute，执行)：对文件而言，具有执行文件的权限；对目录了来说该用户具有进入目录的权限
```

### du 显示每个文件和目录的磁盘使用空间
- 语法：`du [-abcDhHklmsSx][-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>][--max-depth=<目录层数>][--help][--version][目录或文件]`
- 参数：

参数值|参数作用
--|--
-a或-all|显示目录中个别文件的大小
-b或-bytes|显示目录或文件大小时，以byte为单位
-c或--total|除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和
-D或--dereference-args|显示指定符号连接的源文件大小
-h或--human-readable|以K，M，G为单位，提高信息的可读性
-H或--si|与-h参数相同，但是K，M，G是以1000为换算单位
-k或--kilobytes|以1024 bytes为单位
-l或--count-links|重复计算硬件连接的文件
-L<符号连接>或--dereference<符号连接>|显示选项中所指定符号连接的源文件大小
-m或--megabytes|以1MB为单位
-s或--summarize|仅显示总计
-S或--separate-dirs|显示个别目录的大小时，并不含其子目录的大小
-x或--one-file-xystem|以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过
-X<文件>或--exclude-from=<文件>|在<文件>指定目录或文件
--exclude=<目录或文件>|略过指定的目录或文件
--max-depth=<目录层数>|超过指定层数的目录后，予以忽略
--help|显示帮助
--version|显示版本信息

### df 显示磁盘分区上可以使用的磁盘空间
- 语法：`df [-options]`
- 参数：

参数值|参数作用
--|--
-a, --all|包含所有的具有 0 Blocks 的文件系统
--block-size={SIZE}|使用 {SIZE} 大小的 Blocks
-h, --human-readable|使用人类可读的格式(预设值是不加这个选项的...)
-H, --si|很像 -h, 但是用 1000 为单位而不是用 1024
-i, --inodes|列出 inode 资讯，不列出已使用 block
-k, --kilobytes|就像是 --block-size=1024
-l, --local|限制列出的文件结构
-m, --megabytes|就像 --block-size=1048576
--no-sync|取得资讯前不 sync (预设值)
-P, --portability|使用 POSIX 输出格式
--sync|在取得资讯前 sync
-t, --type=TYPE|限制列出文件系统的 TYPE
-T, --print-type|显示文件系统的形式
-x, --exclude-type=TYPE|限制列出文件系统不要显示 TYPE
-v|(忽略)
--help|显示这个帮手并且离开
--version|输出版本资讯并且离开

### free 显示系统中空闲的、已用的物理内存及swap内存
- 语法：`free [-options][-s <间隔秒数>]`
- 参数：

参数值|参数作用
--|--
-b|以Byte为单位显示内存使用情况。
-k|以KB为单位显示内存使用情况。
-m|以MB为单位显示内存使用情况。

### top 实时显示process的动态
- 语法：`top [-] [d delay] [q] [c] [S] [s] [i] [n] [b]`
- 参数：

参数值|参数作用
--|--
d|改变显示的更新速度，或是在交谈式指令列( interactive command)按 s
q|没有任何延迟的显示速度，如果使用者是有 superuser 的权限，则 top 将会以最高的优先序执行
c|切换显示模式，共有两种模式，一是只显示执行档的名称，另一种是显示完整的路径与名称
S|累积模式，会将己完成或消失的子行程 ( dead child process ) 的 CPU time 累积起来
s|安全模式，将交谈式指令取消, 避免潜在的危机
i|不显示任何闲置 (idle) 或无用 (zombie) 的行程
n|更新的次数，完成后将会退出 top
b|批次档模式，搭配 "n" 参数一起使用，可以用来将 top 的结果输出到档案内

### ping 检测主机到其他网络节点的状态
- 语法：`ping [-dfnqrRv][-c<完成次数>][-i<间隔秒数>][-I<网络界面>][-l<前置载入>][-p<范本样式>][-s<数据包大小>][-t<存活数值>][主机名称或IP地址]`
- 参数：

参数值|参数作用
--|--
-d|使用Socket的SO_DEBUG功能
-c<完成次数>|设置完成要求回应的次数
-f|极限检测
-i<间隔秒数>|指定收发信息的间隔时间
-I<网络界面>|使用指定的网络接口送出数据包
-l<前置载入>|设置在送出要求信息之前，先行发出的数据包
-n|只输出数值
-p<范本样式>|设置填满数据包的范本样式
-q|不显示指令执行过程，开头和结尾的相关信息除外
-r|忽略普通的Routing Table，直接将数据包送到远端主机上
-R|记录路由过程
-s<数据包大小>|设置数据包的大小
-t<存活数值>|设置存活数值TTL的大小
-v|详细显示指令的执行过程

### telnet 用于检测远程端口的开放情况以及远程登录
- 语法：`telnet [ip] [port]`
- 用法：
```
telnet 172.1.8.39 8080
```

### netstat 显示网络状态
- 语法：`netstat [-acCeFghilMnNoprstuvVwx][-A<网络类型>][--ip]`
- 参数：

参数值|参数作用
--|--
-a, --all|显示所有连线中的Socket。
-A<网络类型>, --<网络类型>|列出该网络类型连线中的相关地址
-c, --continuous|持续列出网络状态
-C, --cache|显示路由器配置的快取信息
-e, --extend|显示网络其他相关信息
-F, --fib|显示FIB
-g, --groups|显示多重广播功能群组组员名单
-h, --help|在线帮助
-i, --interfaces|显示网络界面信息表单
-l, --listening|显示监控中的服务器的Socket
-M, --masquerade|显示伪装的网络连线
-n, --numeric|直接使用IP地址，而不通过域名服务器
-N, --netlink, --symbolic|显示网络硬件外围设备的符号连接名称
-o, --timers|显示计时器
-p, --programs|显示正在使用Socket的程序识别码和程序名称
-r, --route|显示Routing Table
-s, --statistics|显示网络工作信息统计表
-t, --tcp|显示TCP传输协议的连线状况
-u, --udp|显示UDP传输协议的连线状况
-v, --verbose|显示指令执行过程
-V, --version|显示版本信息
-w, --raw|显示RAW传输协议的连线状况
-x, --unix|此参数的效果和指定"-A unix"参数相同
--ip, --inet|此参数的效果和指定"-A inet"参数相同

### ps 显示当前进程的状态
- 语法：`ps [options] [--help]`
- 参数：

参数值|参数作用
--|--
-A|列出所有的行程
-w|显示加宽可以显示较多的资讯
-au|显示较详细的资讯
-aux|显示所有包含其他使用者的行程
- au(x) 输出格式: USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
   - USER: 行程拥有者
   - PID: pid
   - %CPU: 占用的 CPU 使用率
   - %MEM: 占用的记忆体使用率
   - VSZ: 占用的虚拟记忆体大小
   - RSS: 占用的记忆体大小
   - TTY: 终端的次要装置号码 (minor device number of tty)
   - STAT: 该行程的状态:
      - D: 无法中断的休眠状态 (通常 IO 的进程)
      - R: 正在执行中
      - S: 静止状态
      - T: 暂停执行
      - Z: 不存在但暂时无法消除
      - W: 没有足够的记忆体分页可分配
      - <: 高优先序的行程
      - N: 低优先序的行程
      - L: 有记忆体分页分配并锁在记忆体内 (实时系统或捱A I/O)
   - START: 行程开始时间
   - TIME: 执行的时间
   - COMMAND:所执行的指令

### kill 删除执行中的程序或工作
- 语法：
   - `kill [-s <信息名称或编号>][程序]`
   - `kill [-l <信息编号>]`
- 参数：

参数值|参数作用
--|--
1 (HUP)|重新加载进程。 
9 (KILL)|杀死一个进程。 
15 (TERM)|正常停止一个进程

### tar 用于压缩或解压tar文件
- 语法：`tar [-options] [file or dir]`
- 参数：

参数值|参数作用
--|--
-c, --create|建立新的备份文件 
-f<备份文件>, --file=<备份文件>|指定备份文件 
-z, --gzip, --ungzip|通过gzip指令处理备份文件
-v, --verbose|显示指令执行过程
-x, --extract, --get|从备份文件中还原文件
-C<目的目录>, --directory=<目的目录>|切换到指定的目录

### unzip 用于解压zip文件
- 语法：`unzip [.zip文件][文件][-d <目录>]`
- 参数：

参数值|参数作用
--|--
-d<目录>|指定文件解压缩后所要存储的目录

### find 文件查找
- 语法：`find path [-option] [-print] [-exec -ok command ] {} \;`
- 参数：

参数值|参数作用
--|--
-amin n|在过去 n 分钟内被读取过
-anewer file|比文件 file 更晚被读取过的文件
-atime n|在过去n天内被读取过的文件
-cmin n|在过去 n 分钟内被修改过
-cnewer file|比文件 file 更新的文件
-ctime n|在过去n天内被修改过的文件
-empty|空的文件
-gid n,  -group name|gid 是 n 或是 group 名称是 name
-name name, -iname name|文件名称符合 name 的文件。iname 会忽略大小写
-size n|文件大小 是 n 单位，b 代表 512 位元组的区块，c 表示字元数，k 表示 kilo bytes，w 是二个位元组。
-type c|文件类型是 c 的文件。其中，d: 目录；c: 字型装置文件；b: 区块装置文件；p: 具名贮列；f: 一般文件；l: 符号连结；s: socket。