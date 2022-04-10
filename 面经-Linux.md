# Linux

### 命令

​		**cat**（英文全拼：concatenate）命令用于连接文件并打印到标准输出设备上。



​		**top:**整机查看

```shell
top - 10:45:15 up 23:17,  0 users,  load average: 0.00, 0.00, 0.00
Tasks:  12 total,   1 running,  10 sleeping,   1 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.1 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  12718.5 total,  12488.4 free,     94.9 used,    135.2 buff/cache
MiB Swap:   4096.0 total,   4096.0 free,      0.0 used.  12408.0 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    1 root      20   0    1384    920    468 S   0.0   0.0   0:08.81 init
   19 root      20   0    1512    488     20 S   0.0   0.0   0:00.00 init
   20 root      20   0    1512    488     20 S   0.0   0.0   0:00.00 init
   21 hty       20   0    7000   1656   1480 S   0.0   0.0   0:02.97 fsnotifier-wsl
   27 root      20   0    1512    488     20 S   0.0   0.0   0:00.00 init
   28 root      20   0    1512    488     20 S   0.0   0.0   0:00.01 init
   29 hty       20   0   10056   5112   3336 S   0.0   0.0   0:00.10 bash
  668 root      20   0    1384    564     20 S   0.0   0.0   0:00.00 init
  669 root      20   0    1384    564     20 S   0.0   0.0   0:00.03 init
  670 hty       20   0   10056   5200   3420 S   0.0   0.0   0:00.13 bash
  735 hty       20   0   10876   3628   3116 T   0.0   0.0   0:00.03 top
  737 hty       20   0   10876   3792   3280 R   0.0   0.0   0:00.00 top
```



​		**df - h**：硬盘信息

```shell
hty@LAPTOP-G1B63ICO:/home$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb        251G  7.0G  232G   3% /
tmpfs           6.3G     0  6.3G   0% /mnt/wsl
tools           200G  157G   44G  79% /init
none            6.3G     0  6.3G   0% /dev
none            6.3G  4.0K  6.3G   1% /run
none            6.3G     0  6.3G   0% /run/lock
none            6.3G     0  6.3G   0% /run/shm
none            6.3G     0  6.3G   0% /run/user
tmpfs           6.3G     0  6.3G   0% /sys/fs/cgroup
drivers         200G  157G   44G  79% /usr/lib/wsl/drivers
lib             200G  157G   44G  79% /usr/lib/wsl/lib
C:\             200G  157G   44G  79% /mnt/c
D:\             558G  399G  159G  72% /mnt/d
E:\             196G  120G   76G  62% /mnt/e
```



​		**iostat**:通过iostat方便查看CPU、网卡、tty设备、磁盘、CD-ROM 等等设备的活动情况, 负载信息。

		-C 显示CPU使用情况
		-d 显示磁盘使用情况
		-k 以 KB 为单位显示
		-m 以 M 为单位显示
		-N 显示磁盘阵列(LVM) 信息
		-n 显示NFS 使用情况
		-p[磁盘] 显示磁盘和分区的情况
		-t 显示终端和CPU的信息
		-x 显示详细信息
		-V 显示版本信息
```shell
hty@LAPTOP-G1B63ICO:/home$ iostat
Linux 5.10.16.3-microsoft-standard-WSL2 (LAPTOP-G1B63ICO)       01/12/22        _x86_64_        (8 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.00    0.00    0.01    0.00    0.00   99.98

Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s    kB_read    kB_wrtn    kB_dscd
sda               0.10         0.00        48.86         0.00        225    4197132          0
sdb               0.06         1.55         0.13         0.12     132997      10856       9980
```



​		**iotop:**可以监控进程的I/O信息。它是Python语言编写的，与iostat工具比较，**iostat是系统级别的IO监控，而iotop是进程级别IO监控。**

```shell
Total DISK READ:         0.00 B/s | Total DISK WRITE:         0.00 B/s
Current DISK READ:       0.00 B/s | Current DISK WRITE:       0.00 B/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND                                                      1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init
    8 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init
  668 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init
  669 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init
  670 be/4 hty         0.00 B/s    0.00 B/s  0.00 %  0.00 % -bash
  735 be/4 hty         0.00 B/s    0.00 B/s  0.00 %  0.00 % top
  909 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % sudo su
  910 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % su
  911 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % bash
  921 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % python3 /usr/sbin/iotop
```

![image-20220112112540907](面经-Linux.assets\image-20220112112540907.png)



​		**free**:free 是监控 Linux 内存使用状况最常用的命令

		**Mem** 行(第二行)是内存的使用情况。
		**Swap** 行(第三行)是交换空间的使用情况。
		**total** 列显示系统总的可用物理内存和交换空间大小。
		**used** 列显示已经被使用的物理内存和交换空间。
		**free** 列显示还有多少物理内存和交换空间可用使用。
		**shared** 列显示被共享使用的物理内存大小。
		**buff/cache** 列显示被 buffer 和 cache 使用的物理内存大小。
		**available** 列显示还可以被应用程序使用的物理内存大小。
​		

​		**netstat:**显示网络连接、路由表和网络接口信息

- **-t : 指明显示TCP端口**
- 　　**-u : 指明显示UDP端口**
- 　　**-l : 仅显示监听套接字(所谓套接字就是使应用程序能够读写与收发通讯协议(protocol)与资料的程序)**
- 　　**-p : 显示进程标识符和程序名称，每一个套接字/端口都属于一个程序。**
- 　　**-n : 不进行DNS轮询，显示IP(可以加速操作)**



​		**grep**: Linux grep 命令用于查找文件里符合条件的字符串。

- ​		**-c 只输出匹配行的数量**
- ​		**-i 不区分大小写（只适用于单字符）**
- ​		**-h 查询多文件时不显示文件名**
- ​		**-l 查询多文件时只输出包含匹配字符的文件名**
- ​		**-n 显示匹配行及行号**
- ​		**-s 不显示不存在或无匹配文本的错误信息**
- ​		**-v 显示不包含匹配文本的所有行**	



​		**|:**在linux中是作为管道符的，将‘|’前面命令的输出作为'|'后面的输入。



​		**lsof**:**列出打开文件（lists openfiles）**

- **默认** : 没有选项，lsof列出活跃进程的所有打开文件
- **组合** : 可以将选项组合到一起，如-abc，但要当心哪些选项需要参数
- **-a** : 结果进行“与”运算（而不是“或”）
- **-l** : 在输出显示用户ID而不是用户名
- **-h** : 获得帮助
- **-t** : 仅获取进程ID
- **-U** : 获取UNIX套接口地址
- **-F** : 格式化输出结果，用于其它命令。可以通过多种方式格式化，如-F pcfn（用于进程id、命令名、文件描述符、文件名，并以空终止）

### ------------------------------

### fork（）函数的底层实现原理

```shell
#include<unistd.h>
pid_t fork(void)
```

fork调用的一个奇妙之处就是它仅仅被调用一次，却能够返回两次，它可能有三种不同的返回值：
 		 1）**在父进程中**，fork返回新创建子进程的进程ID；
		  2）**在子进程中**，fork返回0；
		  3）如果出现错误，fork返回一个负值

**当进程调用fork后，当控制转移到内核中的fork代码后，内核会做4件事情:**
		1、分配新的内存块和内核数据结构给子进程

​		2、将父进程部分数据结构内容拷贝至子进程

​		3、添加子进程到系统进程列表当中

​		4、fork返回，开始调度器调度

### ------------------------------

### Linux 文件层次

​		“linux 文件颜色的含义,蓝色代表目录,绿色代表可执行文件,红色表示压缩文件,浅蓝色表示链接文件,灰色表示其他文件,红色闪烁表示链接的文件有问题了,黄色表示设备文件。”

#### **一级目录详细说明**

| 一级目录     | 功能（作用）                                                 |
| ------------ | ------------------------------------------------------------ |
| /bin/        | 存放系统命令，普通用户和 root 都可以执行。放在 /bin 下的命令在单用户模式下也可以执行 |
| /boot/       | 系统启动目录，保存与系统启动相关的文件，如内核文件和启动引导程序（grub）文件等 |
| /dev/        | 设备文件保存位置                                             |
| /etc/        | 配置文件保存位置。系统内所有采用默认安装方式的服务配置文件全部保存在此目录中，如用户信息、服务的启动脚本、常用服务的配置文件等 |
| /home/       | 普通用户的主目录（也称为家目录）。在创建用户时，每个用户要有一个默认登录和保存自己数据的位置，就是用户的主目录，所有普通用户的主目录是在 /home/ 下建立一个和用户名相同的目录。 |
| /lib/        | 系统调用的函数库保存位置                                     |
| /media/      | 挂载目录。系统建议用来挂载媒体设备，如软盘和光盘             |
| /mnt/        | 挂载目录。早期 Linux 中只有这一个挂载目录，并没有细分。系统建议这个目录用来挂载额外的设备，如 U 盘、移动硬盘和其他操作系统的分区 |
| /misc/       | 挂载目录。系统建议用来挂载 NFS 服务的共享目录。虽然系统准备了三个默认挂载目录 /media/、/mnt/、/misc/，但是到底在哪个目录中挂载什么设备可以由管理员自己决定 |
| /opt/        | 第三方安装的软件保存位置。这个目录是放置和安装其他软件的位置，手工安装的源码包软件都可以安装到这个目录中。 |
| /root/       | root 的主目录。普通用[户主目录](https://www.zhihu.com/search?q=户主目录&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"351675403"})在 /home/ 下，root 主目录直接在“/”下 |
| /sbin/       | 保存与系统环境设置相关的命令，只有 root 可以使用这些命令进行系统环境设置，但也有些命令可以允许普通用户查看 |
| /srv/        | 服务数据目录。一些系统服务启动之后，可以在这个目录中保存所需要的数据 |
| /tmp/        | [临时目录](https://www.zhihu.com/search?q=临时目录&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"351675403"})。系统存放临时文件的目录，在该目录下，所有用户都可以访问和写入。建议此目录中不能保存重要数据，最好每次开机都把该目录清空 |
| /lost+found/ | 当系统意外崩溃或意外关机时，产生的一些文件碎片会存放在这里。在系统启动的过程中，fsck  工具会检查这里，并修复已经损坏的文件系统。这个目录只在每个分区中出现，例如，/lost+found  就是根分区的备份恢复目录，/boot/lost+found 就是 /boot 分区的备份恢复目录 |
| /proc/       | 虚拟文件系统。该目录中的数据并不保存在硬盘上，而是保存到内存中。主要保存系统的内核、进程、外部设备状态和网络状态等。如  /proc/cpuinfo 是保存 CPU 信息的，/proc/devices 是保存设备驱动的列表的，/proc/net 是保存[网络协议](https://www.zhihu.com/search?q=网络协议&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"351675403"})信息的/sys/虚拟文件系统。和 /proc/  目录相似，该目录中的数据都保存在内存中，主要保存与内核相关的信息 |
|              |                                                              |

## **二级目录说明**

| /usr子目录        | 功能（作用）                                                 |
| ----------------- | ------------------------------------------------------------ |
| /usr/bin/         | 存放系统命令，普通用户和超级用户都可以执行。这些命令和系统启动无关，在单用户模式下不能执行 |
| /usr/sbin/        | 存放根文件系统不必要的系统管理命令，如多数[服务程序](https://www.zhihu.com/search?q=服务程序&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"351675403"})，只有 root 可以使用。 |
| /usr/lib/         | 应用程序调用的函数库保存位置                                 |
| /usr/XllR6/       | 图形界面系统保存位置                                         |
| /usr/local/       | 手工安装的软件保存位置。我们一般建议源码包软件安装在这个位置 |
| /usr/share/       | 应用程序的资源文件保存位置，如帮助文档、说明文档和字体目录   |
| /usr/src/         | 源码包保存位置。我们手工下载的源码包和内核源码包都可以保存到这里。 |
| /usr/include      | C/C++ 等编程语言头文件的放置目录                             |
| /var子目录        | 功能（作用）                                                 |
| /var/lib/         | 位置。如 MySQL  的数据库保存在 /var/lib/mysql/ 目录中        |
| /var/log/         | 登陆文件放置的目录，其中所包含比较重要的文件如 /var/log/messages, /var/log/wtmp 等。 |
| /var/run/         | 一些服务和程序运行后，它们的 PID（进程  ID）保存位置         |
| /var/spool/       | 里面主要都是一些临时存放，随时会被用户所调用的数据，例如 /var/spool/mail/ 存放新收到的邮件，/var/spool/cron/  存放系统定时任务。 |
| /var/www/         | RPM 包安装的 Apache 的网页主目录                             |
| /var/nis和/var/yp | NIS 服务机制所使用的目录，nis 主要记录所有网络中每一个 client 的连接信息；yp 是 linux 的 nis  服务的日志文件存放的目录 |
| /var/tmp          | 一些应用程序在安装或执行时，需要在重启后使用的某些文件，此目录能将该类文件暂时存放起来，完成后再行删除 |
|                   |                                                              |

### Linux下权限的粒度有 **当前用户，群组用户，其他用户**

- Linux下文件的权限类型一般包括读，写，执行。对应字母为 r、w、x。分别对应4，2，1
