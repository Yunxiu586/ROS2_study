# Linux操作系统

操作系统(Operating System, OS)是计算机系统中最为核心的**系统软件**，它是管理计算机硬件与软件资源，并为用户和其他软件提供服务的程序集合。操作系统内核必须针对CPU的指令集进行**编译**，才能在该CPU上运行。CPU通过指令集定义其能够理解和执行的基本操作命令。

| 操作系统       |           |           |
| -------------- | --------- | --------- |
| 桌面操作系统   | Windows   | Microsoft |
| 桌面操作系统   | macOS     | Apple     |
| 服务器操作系统 | Linux     | 开源      |
| 移动操作系统   | Android   | Google    |
| 移动操作系统   | iOS       | Apple     |
| 移动操作系统   | HarmonyOS | 华为      |

**Linux内核**提供Linux系统硬件调度管理等主要功能，是免费开源的。Linux内核之上，封装系统级应用程序，组合再一起称为Linux操作系统发行版，如Ubuntu，CentOS。

Linux目录结构是**树型结构**，只有一个**根目录/**，所有文件在此根目录下。用/表示路径之间的层级关系

```bash
# 路径第一个/表示根目录，后面的/表示层级关系
/user/local/hello.txt
```



# Linux命令

Linux命令，即Linux程序，一个命令是一个Linux程序。命令行，即Linux终端(Terminal)

Ctrl+Alt+T快捷键打开终端

```bash
command [-options] [parameter]
# options控制命令的行为细节
# parameter控制命令的指向目标
```



**ls命令**

```
ls [-a -l -h] [LinuxPath]
```

```bash
ls # 列出当前工作目录的内容
```

Linux系统的命令行终端启动时，默认加载当前登录用户的**HOME目录**作为当前工作目录，所以ls命令列出的是HOME目录的内容，即每个Linux操作用户在Linux系统的个人账户目录，路径在:/home/用户名

```bash
/home/yunxiu
```

| 选项和参数 |                                                              |
| ---------- | ------------------------------------------------------------ |
| -a         | **all** files：列出全部文件，包括隐藏文件或文件夹(以.开头)   |
| -l         | **long** listing format：竖向排列，更多信息                  |
| -h         | **human-readable** file sizes：以易于阅读的形式列出文件大小，如K，M，G。与l一起使用 |
| LinuxPath  | 指定目录                                                     |

```bash
ls / # 查看根目录的内容
```

```bash
ls -l -a / # -options和parameter混合使用
ls -la /
ls -al /
ls -lh /
```



**目录切换命令**

**cd命令**：Change Directory切换工作目录 

```bash
cd [LinuxPath]
```

无参数时默认回到HOME目录

**pwd命令**：Print Work Directory查看当前工作目录

```bash
pwd
```



绝对路径：根目录为起点

```bash
cd /home/yunxiu/Desktop
```

相对路径：当前目录为起点

```bash
cd Desktop
```

特殊路径符

```bash
cd ./Desktop 	# 切换到当前目录下的Desktop目录内，和cd Desktop效果一致
cd .. 			# 切换到上一级目录
cd ../..		# 切换到上二级的目录
cd ~			# 切换到HOME目录
cd ~/Desktop	# 切换到HOME内的Desktop目录
```



**mkdir命令**：Make Directory创建新目录(文件夹)，权限仅在HOME目录内

```bash
mkdir [-p] LinuxPath
```

参数LinuxPath必填

-p表示自动创建不存在的父目录，适合于创建连续多层级的目录

```bash
mkdir /home/yunxiu/test1
mkdir ./test2
mkdir ~/test3
mkdir -p ~/TEST/test4	# mkdir ~/TEST/test4
```



**文件操作命令**

**touch命令**：创建文件

```bash
touch LinuxPath
```

```bash
touch test.txt
```

**cat命令**：concatenate查看文件内容，直接将内容全部显示

```bash
cat LinuxPath
```

```bash
cat test1.txt
```

**more命令**：查看文件内容，支持空格翻页，Q退出

```bash
more LinuxPath
```

```bash
more /etc/services
```

**cp命令**：copy复制文件文件夹

```
cp [-r] param1 param2
```

-r选项：用于复制文件夹使用，表示递归

param1：Linux路径，表示被复制的文件或文件夹

param2：Linux路径，表示要复制去的地方

```bash
cp test1.txt text2.txt	# 文件复制
cp -r test1 text2		# 文件夹复制
```

**mv命令**：move移文件文件夹

```bash
mv param1 param2
```

param1：Linux路径，表示被移动的文件或文件夹

param2：Linux路径，表示要移动去的地方，如果目标不存在则重命名，确保目标存在

```bash
mv test1.txt Desktop	# 文件移动
mv test1.txt renamed.txt# 重命名
mv test Desktop			# 文件夹移动
```

**rm命令**：remove删除文件文件夹

```bash
rm [-r -f] param1 param2 ...
```

-r：同cp命令一样，选项用于删除文件夹

-f：force强制删除(不会弹出提示确认信息)普通用户删除内容不会弹出提示，只有root管理员用户删除内容会有提示所以一般普通用户用不到-f选项

param1  param2  ...  参数N ：表示要删除的文件或文件夹路径，按照空格隔开

```bash
rm text1.txt test2.txt
rm test1 test2
```

符号 * 表示**通配符**，即匹配任意内容(包含空)

```bash
mv test* 	# 表示删除任何以test开头的内容
mv *test	# 表示删除任何以test结尾的内容
mv *test*	# 表示删除任何包含test的内容
```

```bash
rm -rf /	# 格式化
rm -rf /*
```



**查找命令**

**which命令**：查找命令(程序)的文件

```bash
which command
```

```bash
which pwd
/usr/bin/pwd
```

**find命令**：

按文件名查找

```bash
su -root
find 起始路径 -name "被查找文件名"
```

按文件大小查找

```bash
su -root
find 起始路径 -size +或- n[kMG]
```

```bash
find / -size -100k	# 查找小于100k的文件
find / -size +1G	# 查找大于1G的文件
```

**history命令**：查看历史输入命令

```bash
history
```



**gerp命令**：**G**lobal **R**egular **E**xpression **P**rint通过关键字过滤文件行

```bash
grep [-n] 关键字 文件路径
```

选项-n：可选，表示在结果中显示匹配的行的行号

param1关键字：必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用" "将关键字包围起来

param2文件路径：必填，表示要过滤内容的文件路径，可作为管道符输入端口

**wc命令**：word count

```bash
wc [-c -m -l -w] 文件路径
```

-c：统计bytes数量

-m：统计字符数量

-l：统计行数

-w：统计单词数量

文件路径：被统计的文件，可作为管道符输入端口

**管道符**：将左侧结果作为右侧输入

```bash
cat file.text | grep word
```

```bash
cat file.text | wc -l
```



**echo命令**：

```bash
echo 输出的内容
```

建议复杂的输出可以用" "包围起来

```bash
echo "Hello World!"
```

```bash
echo `pwd`	# ``内的内容作为命令执行
/home/yunxiu
```

| 重定向符 |                                              |
| -------- | -------------------------------------------- |
| >        | 将左侧命令的结果，覆盖写入符号右侧指定的文件 |
| >>       | 将左侧命令的结果，追加写入符号右侧指定的文件 |

```bash
echo "Hello World!" > file.text
```

```bash
echo "Hello World!" >> file.text
```

```bash
echo "当前工作目录：`pwd`" > work.text
```

**tail命令**：查看文件尾部内容，跟踪文件的最新更改

```bash
tail [-f -num] LinuxPath
```

LinuxPath：表示被跟踪的文件路径

-f：follow表示持续跟踪选项，Ctrl+C退出

-num：表示查看尾部多少行，不填默认10行选项

```bash
tail -5 file.text
```

```
tail -f file.text
```

```bash
echo "内容" >> work.text
tail -f work.text 
```



| vi/vim编辑器                 | 默认命令模式i/a/o/I/A/O进入输入模式，输入模式ESC进入命令模式<br>命令模式:进入底线命令模式，底线命令模式:w保存，:q推出，:wq |
| ---------------------------- | ------------------------------------------------------------ |
| 命令模式(Command mode)       | 所敲的按键编辑器都理解为命令，以命令驱动执行不同的功能。<br>此模式下，不能自由进行文本编辑 |
| 输入模式(Insert mode)        | 也就是所谓的编辑模式、插入模式。<br>此模式下，可以对文件内容进行自由编辑 |
| 底线命令模式(Last line mode) | 以:开始，通常用于文件的保存、退出                            |

```bash
vi 文件路径
```

如果文件路径表示的文件不存在，那么此命令会用开编辑新文件
如果文件路径表示的文件存在，那么此命令用于编辑已有文件

```
vi file.text
```

| 模式         | 命令           |                                  |
| ------------ | -------------- | -------------------------------- |
| 命令模式     | i              | 当前光标位置进入输入模式         |
| 命令模式     | a              | 当前光标位置之后进入输入模式     |
| 命令模式     | I              | 当前行开头进入输入模式           |
| 命令模式     | A              | 当前行结尾进入输入模式           |
| 命令模式     | o              | 当前光标下一行进入输入模式       |
| 命令模式     | O              | 当前光标上一行进入输入模式       |
| 输入模式     | ESC            | 回到命令模式                     |
| 命令模式     | 键盘上、键盘k  | 向上移动光标                     |
| 命令模式     | 键盘下、键盘j  | 向下移动光标                     |
| 命令模式     | 键盘左、键盘h  | 向左移动光标                     |
| 命令模式     | 键盘右、键盘l  | 向后移动光标                     |
| 命令模式     | 0              | 移动光标到当前行的开头           |
| 命令模式     | $              | 移动光标到当前行的结尾           |
| 命令模式     | pageup(PgUp)   | 向上翻页                         |
| 命令模式     | pangdown(PgDn) | 向下翻页                         |
| 命令模式     | /              | 进入搜索模式                     |
| 命令模式     | n              | 向下继续搜索                     |
| 命令模式     | N              | 向上继续搜索                     |
| 命令模式     | dd             | 删除光标所在行的内容             |
| 命令模式     | ndd            | n是数字，删除当前光标向下n行     |
| 命令模式     | yy             | 复制当前行                       |
| 命令模式     | nyy            | n是数字，复制当前行和下面的n行   |
| 命令模式     | p              | 粘贴复制的内容                   |
| 命令模式     | u              | 撤销修改                         |
| 命令模式     | Ctrl+r         | 反向撤销修改                     |
| 命令模式     | gg             | 跳到首行                         |
| 命令模式     | G              | 跳到行尾                         |
| 命令模式     | dG             | 从当前行开始，向下全部删除       |
| 命令模式     | dgg            | 从当前行开始，向上全部删除       |
| 命令模式     | d$             | 从当前光标开始，删除到本行的结尾 |
| 命令模式     | d0             | 从当前光标开始，删除到本行的开头 |
| 命令模式     | :              | 进入底线命令模式                 |
| 底线命令模式 | :wq            | 保存并退出                       |
| 底线命令模式 | :q             | 仅退出                           |
| 底线命令模式 | :q!            | 强制退出                         |
| 底线命令模式 | :w             | 仅保存                           |
| 底线命令模式 | :set u         | 显示行号                         |
| 底线命令模式 | : set paste    | 设置粘贴模式                     |



**用户与权限**

普通用户：一般在HOME目录内不受限，HOME目录以外，一般仅有只读和执行权限，无修改权限

**root用户**：拥有最大权限的账户名(超级管理员)

**su命令**：**S**witch **U**ser

```bash
su [-] [用户名]
```

-：是否切换用户后加载环境变量

用户名：省略时默认切换为root用户

```bash
exit		# 回退到上一个用户，或Ctrl+D
```

```bash
su -root	# 切换root用户
# 输入密码
exit		# 退回普通用户
```

**sudo命令**：为普通命令授权，临时以root身份执行，需要普通用户配置sudo认证

```bash
sudo command
```



**用户和用户组管理**：需要root权限

创建用户组

```bash
groupadd 用户组名
```

删除用户组

```bash
groupdel 用户组名
```

创建用户

```bash
useradd [-g -d] 用户名
```

-g：指定已存在的用户组，如已存在同名组必须使用-g，不指定-g会创建同名组并自动加入

-d：指定用户HOME路径，不指定默认在/home/用户名

查看用户

```bash
userdel [-r] 用户名
```

-r：删除用户HOME路径，不使用

查看用户所属组

```bash
id [用户名]
```

修改用户所属组

```bash
usermod -aG
```

查看当前系统的所有用户信息

```
getent passwd
```

查看当前系统的所有用户组信息

```
getent group
```



**权限控制**

**认知权限信息**

|         | 所属 | 用户 | 权限 | 所属 | 用户组 | 权限 | 其他 | 用户 | 权限 |
| ------- | ---- | ---- | ---- | ---- | ------ | ---- | ---- | ---- | ---- |
| -或d或l | r或- | w或- | x或- | r或- | w或-   | x或- | r或- | w或- | x或- |

第1位：-表示文件，d表示文件夹，l表示软连接

w(write)写权限，x(execute)执行权限，r(read)读权限



**chmod命令**：change mode修改文件或文件夹的权限信息

只有**文件或文件夹的所属用户或root用户**可以修改

```bash
chmod [-R] 权限 文件或文件夹
```

-R：对文件夹内的全部内容应用相同的操作

```bash
chmod u=rwx,g=rx,o=x file.txt	# 文件file.txt权限修改为rwxr-x--x
```

u表示user所属用户权限，g表示group所属用户组权限，o表示other其他用户权限

| 数字 | 权限 |
| ---- | ---- |
| 0    | ---  |
| 1    | --x  |
| 2    | -w-  |
| 3    | -wx  |
| 4    | r--  |
| 5    | r-x  |
| 6    | rw-  |
| 7    | rwx  |

```bash
chmod 751 file.txt	# u=rwx,g=rx,o=x的快捷写法
```

**chown命令**：change owner修改文件和文件夹的所属用户和所属用户组

**只有root用户**可以修改文件和文件夹的所属用户和所属用户组

```bash
chown [-R] [用户][:][用户组] 文件或文件夹
```

-R：对文件夹内的全部内容应用相同的操作

```bash
chown root file.text	# 将文件file.text所属用户修改为root
```

```bash
chown ：root file.text	# 将文件file.text所属用户组修改为root
```

```bash
chown yunxiu：root file.text	# 将文件file.text所属用户修改为yunxiu，所属用户组修改为root
```



| 快捷键    | 功能                                                         |
| --------- | ------------------------------------------------------------ |
| Ctrl+C    | 强制停止；退出当前输入，重新输入                             |
| Ctrl+D    | 退出用户或某些特定程序，不能退出vi/vim                       |
| !命令前缀 | 自动执行上一次匹配的前缀                                     |
| Ctrl+R    | 输入内容区匹配历史命令，上下键查找上下命令，左右键可编辑命令，回车执行命令 |
| Ctrl+A    | 跳到命令开头                                                 |
| Ctrl+E    | 跳到命令结尾                                                 |
| Ctrl+左右 | 跳单词                                                       |
| Ctrl+L    | 清空终端内容，同clear命令                                    |



**apt命令**：Advanced Package Tool软件安装

```bash
apt [-y] [install | remove | search] 软件名称
```

-y：自动确认，无需手动确认安装或卸载过程

**systemclt命令**：控制软件的启动停止和开机启动

```bash
systemctl start | stop | status | enable | disable 服务名
```

start启动，stop关闭，status查看状态，enable开启开机自启动，disable关闭开机自启动

服务名：系统内置服务如NetworkManager主网络服务，network副网络服务，firewalld防火墙服务，sshd(ssh服务)

**ln命令**：创建软连接，将文件或文件夹链接到其他位置

```bash
ln -s param1 param2
```

param1：被链接的文件或文件夹

param2：要链接去的目的地

**date命令**：查看系统时间

```
date -d [+格式化字符串]
```

-d：按照给定的字符串显示日期，一般用于日期计算

格式化字符串：通过特定的字符串标记,来控制显示的日期格
%Y年
%y年份后两位数字(00~99)
%M月份(01~12)
%d日(01~31)
%H小时(00~23)
%M分钟(00~59)
%S秒(00~60)
%s自1970-01-00:00:00UTC到现在的秒数

```bash
date
Wed Jan  7 03:14:36 PM CST 2026
```

```bash
date +%Y-%m-%d
2026-01-07
```

```bash
date "+%Y-%m-%d %H:%M:%S"	# 有空格
2026-01-07 15:15:00
```

```bash
data -d "-1 day"			# 昨天
Tue Jan  6 03:19:11 PM CST 2026
```



**IP地址**(Internat Protocol Address)：网络通信的地址

IPv4地址的格式：a.b.c.d，其中abcd是0~255的数字，如192.168.232.204

```bash
idconfig	# 查看IP地址
eno1: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether e0:73:e7:ee:4d:97  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 1682  bytes 310736 (310.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1682  bytes 310736 (310.7 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlo1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.232.204  netmask 255.255.255.0  broadcast 192.168.232.255
        inet6 fe80::170c:deb4:6f30:ba6c  prefixlen 64  scopeid 0x20<link>
        ether 74:97:79:8a:b1:0d  txqueuelen 1000  (Ethernet)
        RX packets 91726  bytes 111372710 (111.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 43329  bytes 8457019 (8.4 MB)
        TX errors 0  dropped 59 overruns 0  carrier 0  collisions 0
```

| 接口名 | 网卡                           |
| ------ | ------------------------------ |
| eno1   | 有线网卡(Ethernet)             |
| lo     | 虚拟回环接口，用于本机内部通信 |
| wlo1   | 无线网卡(Wi-Fi)                |

UP：系统启用该网卡

RUNNING：物理链接激活

0.0.0.0：可以用于指代本机、可以在端口绑定中用来确定绑定关系、在一些地址限制中表示所有IP，如放行规则设置为0.0.0.0表示允许任意IP访问

127.0.0.1：本机地址，访问此地址就是访问本电脑

192.168.232.204：IPv4地址

**主机名**：

```bash
hostname
yunxiu-OMEN-by-HP-Gaming-Laptop-16-xf0xxx
```

```bash
hostnamectl set-hostname 主机名	# 修改主机名
```

域名解析：

