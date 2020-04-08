# python
AIX介绍：

  AIX 全名为（Advanced Interactive Executive），它是IBM 公司的UNIX操作系统， 整个系统的设计从网络、主机硬件系统，到操作系统完全遵守开放系统的原则。 下面对AIX 作以介绍。 

RS/6000 采用IBM 的UNIX操作系统-AIX作为其操作系统。这是一个目前操作系统界最成功，应用领域最广，最开放的第二代的UNIX系统。它特别适合于做关键数据处理（CRITICAL）。 

AIX 包含了许多IBM 大型机传统受欢迎的特征，如系统完整性，系统可管理性和系统可用性。

在 AIX  操作系统上，有许多的数据库和开发工具，用户除了选用已有的应用软件外，还可以根据各自的需要进行开发。 

 此外，在AIX 之上，有一组功能强，使用方便的系统管理工具。对于异种平台互存，互操作有很成熟的解决方案。 

 由于该 UNIX 的先进的内核技术和最好的开放性，因此，虽然RS/6000从宣布到今天只有短短的5 年多的时间，它已在各行各业有了广泛的运用， 并在1993和1994年连续二年在MIDRANGE商用 UNIX 领域处于第一位。

 RISC SYSTEM/6000的操作系统是AIX ，它是性能卓越的、开放的UNIX，汇集了多年来计算机界在UNIX上的研究成果，以IBM 在计算机体系结构、操作系统方面40多年极其丰富的经验。最大限度的使用RISC技术，安装了象AIX 这样的具备工业界实力的UNIX操作系统。 

 它既可连接SAA 体系结构，又能与非IBM 系统的网络相连，因此，可以和多数专业银行现有的系统实现互连，这对今后业务系统拓展将带来极大的灵活性，并降低投资。 

  AIX 遵循一系列的国际标准： 
*   IEEE POSIX1004.1－1990 
*   X/OPEN 移植指南ISSUE3的基本级（XPG3） 
*   AES/OS REVISION A （OSF/1 LEVEL 2 资格） 
*   FIPS 151－1 
*   AIX的编译器： XLC、C++(可选)、FORTRAN(可选)、PASCAL(可选)、COBOL(可选) 
*   ADA 的编译器已达到XPG3“成员”级的认可。 
*   AIX 支持多用户、多任务。 

    AIX有一些其它特性包括： 


n         AIX 提供了3 种SHELL ：SYSTEM V的KORN、BOURNE SHELL和4.3BSDC  SHELL作为可选择的UNIX系统界面； 

n         安全设施满足TCB （Trusted Computing Base）的C2级； 

n         实时处理能力，这对于“面向交易”的应用至关重要（如零售业 和银行等），它使RS/6000 获得极高的响应和吞吐量； 

n         虚拟存储管理，当需要时，可将一些不常用的模块转送至外存，提高内存的可利用性。

n         先进的文件系统，使得系统管理更加有效，并提高了数据可靠性以及完整性。 

n         能兼容DOS 应用程序和数据。 

 

 InfoExplorer，快速信息超文本索引系统- 不仅包括文字，而且对包含声音、图像的索引系统，这是个联机的文件接口。包括全部的超文本的索引和查找，以及面向任务和坐标的多重导引和索引系统。 这个文字及图形索引系统以一个灵活的、基于任务的方式去使用详细 
资料及培训资料。 

    高级系统管理工具（SMIT，System Management Interface Tool）。提供一级菜单驱动程序，诸如完成软件的安装与设置、设备的设置及管理、问题的测定、存贮管理等。可以自动地进行I/O 设备设置，ASCII 终端也可充当系统控制台。在LAN 上可以进行远程系统的安装。

 

AIX系统结构：

   applications >> shell >> kernel >> hardware

 

AIX特点：

   1.先进内核

   2.基于众多工业标准

   3.强大通讯能力

  

AIX(Advanced Integrative Executive)的几项重要技术：

   1.SMIT ( system management interface tool ) 系统界面管理工具

   2.LVM  ( logic volume manager ) 逻辑卷管理器

   3.JFS  ( journal file system ) 日志文件系统

  

AIX系统启动过程：(3种启动模式：Normal (多用户),Service(维护模式),Secure(系统不启动))

   1.ROM 只读存储器，初始化/自检

   2.boot loaded  装载引导块(IPL)

   3.AIX kernel 内核，文件系统设备配置数据

   4./etc/init ( /etc/inittab ，系统初始化程序引导

   5.getty

   6.login ( /etc/passwd, /etc/security/passwd )

   7.ksh ( $HOME/.profile )   

 

AIX Kernel 包括：

   1.多任务处理，多用户

   2.I/O设备的接口

   3.管理磁盘上的文件

   4.C语言环境

 

AIX文件系统：/home /usr /etc /bin /dev /tmp /var  

 

AIX存储的组成部分：

   1.文件

   2.目录

   3.文件系统

   4.逻辑卷

   5.物理存储

   6.逻辑存储

   7.逻辑卷的管理

 

一些系统命令：

   lsdev -C           列出所有系统设备(包括所有状态：Undefined,Defined,Available)

   lsdev -Cc adapter  列出系统现有设备

   lsdev -PH          列出系统所有支持的设备

   lsdev -P -r class  列出系统所有支持的设备分类(例如：swap,sys,tape,tty,printer,mouse,memory,lvm等)

   lsdev -P -c disk -r subclass 列出系统所有支持的设备分类(磁盘)的子类(例如：SCSI,DAR,IDE,ISCSI等)

   lsdev -P -c tape             列出所有支持的磁带设备

   lsdev -l hdi*                列出所有系统的SCSI Disk Drive

   lsattr -l rmt0 -E            查看磁带设备rmt0的属性信息

   lsattr -l scsi0 -a bus_intr_lvl -E 查看SCSI卡适配器scsi0的bus_intr_lvl属性信息

   lsattr -l tty0 -a login -R

   lsattr -E -l sys0                  列出所有系统属性（包括物理内存）

   lsattr -E -l sys0 -a realmem       列出系统物理内存大小

  

   netstat -in 查看所有网卡IP地址

   netstat -r  查看所有路由

   ifconfig -a 查看所有网络配置信息

   netstat -D  查看所有通讯包的统计

   netstat -s -f inet 查看每种协议传输的数据量统计

   netstat -v         查看每块网卡传输的数据量和状态统计

 

$smit lvm         进行lv的管理

$smit pv          进行PV物理卷的管理

$smitty mkvg      新建VG

$smit mklv        添加一个LV

$smit mklvcopy    添加一个LV镜像

$smit rmlv        删除一个LV

$smit pv          管理物理卷

$smit extendvg    增加一个PV到VG

$lspv             列出物理卷

$lspv hdisk2      查看该PV的信息

$lspv -l hdisk2   查看该PV的详细信息

$lsvg -o          查看正在使用的vg

$lsvg -l rootvg   查看该VG详细信息

$lslv hd5         查看该LV的信息

$lslv -l hd5      查看该LV的详细信息

$varyonvg testvg  激活一个VG

$varyoffvg testvg 卸载一个VG

$lsfs        列出文件系统

Name            Nodename   Mount Pt               VFS   Size    Options    Auto Accounting

/dev/hd4        --         /                      jfs2  262144  --         yes  no

/dev/hd1        --         /home                  jfs2  262144  --         yes  no

/dev/hd2        --         /usr                   jfs2  8388608 --         yes  no

/dev/hd9var     --         /var                   jfs2  262144  --         yes  no

/dev/hd3        --         /tmp                   jfs2  1048576 --         yes  no

/dev/hd10opt    --         /opt                   jfs2  262144  --         yes  no

/dev/LF_test    --         /test                  jfs2  10485760 rw         yes  no

/dev/lv02       --         /LAPCMP                jfs   31195136 rw         no   no

/dev/lv00       --         /LAPSWT                jfs   30932992 rw         no   no

/dev/lv01       --         /LAPTRS                jfs   20709376 rw         no   no

 

$lsvg -l rootvg

rootvg:

LV NAME             TYPE       LPs   PPs   PVs  LV STATE      MOUNT POINT

hd5                 boot       1     2     2    closed/syncd  N/A

hd6                 paging     64    128   2    open/syncd    N/A

hd8                 jfs2log    2     4     2    open/syncd    N/A

hd4                 jfs2       8     16    2    open/syncd    /

hd2                 jfs2       32    64    1    open/syncd    /usr

hd9var              jfs2       8     16    2    open/syncd    /var

hd3                 jfs2       8     16    2    open/syncd    /tmp

hd1                 jfs2       8     16    2    open/syncd    /home

hd10opt             jfs2       8     16    2    open/syncd    /opt

lg_dumplv           sysdump    16    16    1    open/syncd    N/A

LF_LAPPTGZ          jfs2       160   320   2    open/syncd    /LAPPTGZ

LF_LAPPTDL          jfs2       80    160   2    open/syncd    /LAPPTDL

LF_LAPPOMS          jfs2       16    32    2    open/syncd    /LAPPOMS

LF_LAPPTQD          jfs2       80    160   2    open/syncd    /LAPPTQD

LF_LDBSTGD          jfs2       16    32    2    open/syncd    /LDBSTGD

LF_LAPPTSZ          jfs2       160   320   2    open/syncd    /LAPPTSZ

LF_LAPPTFZ          jfs2       80    160   2    open/syncd    /LAPPTFZ

LF_LAPPMOS          jfs2       8     16    2    open/syncd    /var/pdos

LF_LAPPTTJ          jfs2       80    160   2    open/syncd    /LAPPTTJ

LF_LAPPTKM          jfs2       80    160   2    open/syncd    /LAPPTKM

LF_LAPPTXM          jfs2       80    160   2    open/syncd    /LAPPTXM

LF_LDBSGD1          jfs2       16    32    2    open/syncd    /LDBSGD1

LF_LPAMBAK          jfs2       16    32    2    open/syncd    /LPAMBAK

 

$lslv -l LF_LAPPTFZ

 

PV                COPIES        IN BAND       DISTRIBUTION 

hdisk5            080:000:000   100%          000:000:058:022:000

hdisk1            080:000:000   100%          000:000:004:076:000

 

 

 

物理卷(PV):一个硬盘 //  lspv

卷组(VG):可用硬盘的集合// lsvg( lsvg -o 查看正在使用的vg)

物理分区(PPAR)

逻辑卷(LV):每个卷组(VG)可以划分成若干LV，可以跨多块硬盘

逻辑分区(LPAR)：lv 由逻辑分区组成

 

LVM (Logic Volume Manager ) 逻辑卷管理器：

---------------------------------------------------------------------------------------

   1.传统分区1，分区2，。。。不能扩展，存在文件和文件系统限制，需要连续数据和事先计划

   2.LVM,可以使用不相连空间，跨硬盘，动态增长，可以作镜像，可以重新定向

   3.物理分区PPAR(硬盘上的一个物理分区) >> 物理卷PV(一个硬盘) >> 卷组 VG (可用硬盘的集合)

     逻辑分区LPAR >> 逻辑卷LV >> 卷组VG

     rootvg(内置盘) vg00(外置盘)  >> 卷组 VG

 

 

在存取卷组前必须用varyonvg命令激活

 

停止HA，vg被2号机器自动接管,IP地址也被自动接管，即2号机会增加所有1号机的IP地址：

--------------------------------------------------------------------------------

停HACMP:smitty clstop 

使用lsvg –o 命令会看不到一些（应用）VG(1号机会接管)；

使用 netstat –i命令可以看到系统SVC地址会变成BOOT地址 

把HDISK0从ROOTVG中不做MIRROW : unmirrorvg rootvg hdisk0 

可观察CLUSTER的启动：/usr/es/adm/cluster.log,  /tmp/hacmp.out 

 

HACMP主要完成3个步骤：

  1.IP接管

  2.VG接管

  3.应用接管

－查看是否开始HACMP接管：查看/tmp/hacmp.out文件。

 

smit(SMIT，System Management Interface Tool)快捷命令进行各项设定:例如增加路由smit mkroute

诸如完成软件的安装与设置、设备的设置及管理、问题的测定、存贮管理等。可以自动地进行I/O 设备设置，ASCII 终端也可充当系统控制台。在LAN 上可以进行远程系统的安装。

 

RS/6000 采用IBM 的UNIX操作系统-AIX作为其操作系统。这是一个目前操作系统界最成功，应用领域最广，最开放的第二代的UNIX系统。它特别适合于做关键数据处理（CRITICAL）。 

 

AIX常用命令

 

查看交换区信息：
lsps -a 显示交换区的分布信息
lsps -s 显示交换区的使用信息
slibclean 清除处理程序遗留的旧分页信息
smit mkps 建立交换区空间信息
swapon -a 启动所有的分页空间
/etc/swapspaces 存放分页空间表格信息
-------------------------------------------------
显示卷信息：
lsvg 显示卷的名称
lsvg -l rootvg 显示rootvg卷的详细信息

-------------------------------------------------
mount卷的方法：
varyonvg datavg 加载datavg卷
mount /dev/data1 加载datavg下的一个data1卷

裸设备类型：raw,jfs jfs可以转变成文件系统，而raw则不行
-------------------------------------------------

在裸设备上安装oracle系统：
修改裸设备的权限，如裸设备名为system01，安装数据库用户为oracle
chown oracle:dba /dev/system01
chown oracle:dba /dev/rsystem01
在使用文件时必须用rsystem01
-------------------------------------------------

smit快速路径名称：(smit：图形方式，smitty：字符方式)
dev 设备管理
diag 诊断
jfs 定期档案管理系统
lvm 逻辑卷册系统管理员管理
nfs NFS管理
sinstallp 软件安装及维护
spooler 列印队列管理
system 系统管理
tcpip TCP/IP管理
USER 使用者管理
clstart，clstop：启动和停止cluster
lssrc -g cluser：查看cluser的状态
-------------------------------------------------

查看已安装的软件信息：
ls -aF /usr/lpp (lpp:Licensed Program Products)
查看安装媒体内容：
installp -q -d /dev/cdrom -l
-------------------------------------------------

启动时自动加载文件系统信息：
需要加载的信息存放在/etc/filesystems
mount -t nf 加载所有在/ect/filesystems中定义type=nfs的文件系统
显示已加载的文件系统及状态： df -v,mount
-------------------------------------------------

查看错误日志信息：
errpt -a
-------------------------------------------------

有关TCP/IP的命令
网路卡：
smit chgenet,chgtok,chgfddi,opschange,mktty:adptr架构快速路径
smit mkinet,ppp:slip与ppp快速路径
ifconfig:config界面
位址：
/etc/hosts 静态主机表
/etc/resolv.conf 位址解析的名称服务器
/etc/named.boot 名称服务器架构
/etc/named.ca 根名称服务器快取
/etc/named.data 位址列表
/etc/named.rev 反转指标列表
nslookup 查询名称服务器资讯
网络路由：
route 管理路由
netstat -rn 列出定义的路由
routed 路由(daekmin rip)
gated 路由(daekmin rip、egp、hello)
/etc/gateways 已知网关
/etc/networks 已知网路
服务：
/etc/services
/etc/inetd.conf
TCP/IP群组子系统:
/etc/rc.net
startsrc -g tcpip 启动全部的tcpip子系统 
startsrc -s inetd 启动主要internet
除错：
iptrace 启动封包追踪
ipreport 追踪结果格式化输出
netstat 网络统计
ping 检查是否可以到达
查看HACMP，外部硬盘信息:
lscfg -v
lsdev -Cc adapter
对等机器信息：
/etc/.rhosts
/etc/hosts.equiv
/etc/hosts
-------------------------------------------------

观察进程内存使用情况：
ps aux 观察参数%mem：内存使用百分比 RSS:实际使用内存
vmstat free的单位为块，缺省值为4096bytst
-------------------------------------------------

创建raw设备时选择的类型:
raw_lv 

 

AIX系统日常管理

 

1． 文件系统是否满 
方法： df –k 可以以K为单位检查文件系统的使用率。（90%以上，需要调整） 


2． 检查系统出错日志 使用errpt |more来检查 
清除现有的log: Errclear 0 


3． 检查系统合法/非法登陆情况 
使用Last命令来检查来自登陆的地方。 


4． 检查系统是否有巨大的Core文件生成 
使用 find / -name core –print来检查。对Core文件，一般直接删除就可以了。 


5． 系统性能检查： 

a) CPU性能：使用Vmstat, topas来检查 
b) 内存使用情况：也是使用topas, vmstat来检查 
c) 检查IO平衡使用情况：使用iostat来检查 
d) 交换空间使用情况：使用lsps –a来检查 


6． Mail检查 
7． Diag 一个月一次 


 

不该忽视的AIX命令

内核

如何查明正在运行的是 32 位内核还是 64 位内核？

要想显示内核是 32 位还是 64 位的，输入：

bootinfo -K

如何查明正在运行的是单处理器内核还是多处理器内核？

/unix 是被引导的内核的符号链接。要想查明正在运行的内核模式，输入 ls -l /unix 并查看 /unix 链接到哪个文件。下面是 ls -l /unix 命令可能产生的三种输出以及与它们对应的内核：

/unix -> /usr/lib/boot/unix_up # 32 bit uniprocessor kernel
/unix -> /usr/lib/boot/unix_mp # 32 bit multiprocessor kernel
/unix -> /usr/lib/boot/unix_64 # 64 bit multiprocessor kernel

注意：
AIX 5L Version 5.3 不支持单处理器内核。

如何从一种内核模式切换到另一种模式？

在安装过程中，会根据使用的 AIX 版本和硬件，默认启用一种内核。使用回答前一个问题的方法并假设启用了 32 位内核。再假设您希望改为以 64 位内核模式引导系统。可以通过执行以下命令来完成这个任务：

ln -sf /usr/lib/boot/unix_64 /unix
ln -sf /usr/lib/boot/unix_64 /usr/lib/boot/unix

bosboot -ad /dev/hdiskxx
shutdown -r

/dev/hdiskxx 目录是引导逻辑卷 /dev/hd5 的位置。要想查明 hdiskxx 中的 xx 是什么，运行以下命令：

lslv -m hd5

注意：
在 AIX V5.2 中，默认安装 32 位内核。在 AIX V5.3 中，在 64 位硬件上默认安装 64 位内核，在 32 位硬件上默认安装 32 位内核。

硬件

如何查明自己的机器是否能够运行 AIX 5L Version 5.3？

AIX 5L Version 5.3 可以在支持的所有基于 CHRP (Common Hardware Reference Platform) 的 POWER? 硬件上运行。

如何查明自己的机器是否是基于 CHRP 的？

运行 prtconf 命令。如果是 CHRP 机器，在 Model Architecture 行上就会出现字符串 chrp。

如何查明自己的 System p（硬件）是 32 位还是 64 位的？

要想显示硬件是 32 位还是 64 位的，输入：

bootinfo -y

机器上的真实内存有多少？

要想以 KB 为单位显示真实内存，输入以下命令之一：

bootinfo -r

lsattr -El sys0 -a realmem

我的机器可以运行 64 位内核吗？

运行 64 位内核需要 64 位硬件。

系统中设备的属性值是多少？

要想列出磁带设备 rmt0 的属性的当前值，输入：

lsattr -l rmt0 -E

要想列出磁带设备 rmt0 的属性的默认值，输入：

lsattr -l rmt0 -D

要想列出 TTY 设备 tty0 的 login 属性的可能值，输入：

lsattr -l tty0 -a login -R

要想显示系统级属性，输入：

lsattr -E -l sys0

我的系统有多少个处理器？

要想显示系统上的处理器数量，输入：

lscfg | grep proc

我的系统有多少个硬盘？哪些硬盘正在使用？

要想显示系统上的硬盘数量，输入：

lspv

如何获得关于某一物理卷的信息？

要想找到关于 hdisk1 的详细信息，输入：

lspv hdisk1

如何获得系统的详细配置？

输入以下命令：

lscfg

以下选项提供特定信息：

-p	显示与平台相关的设备信息。在 AIX V4.2.1 或更高版本上可以使用这个选项。
-v	显示在定制的 VPD (Vital Product Database) 对象类中找到的 VPD。
例如，要想显示关于磁带设备 rmt0 的详细信息，输入：

lscfg -vl rmt0

可以通过运行 prtconf 命令获得相似的信息。

如何查明芯片类型、系统名、节点名、型号等信息？

uname 命令提供关于系统的详细信息。

uname -p	显示系统的芯片类型。例如，PowerPC?。
uname -r	显示操作系统的发布版本号。
uname -s	显示系统名。例如，AIX。
uname -n	显示节点名。
uname -a	显示系统名、节点名、版本和机器 ID。
uname -M	显示系统型号名。例如，IBM, 9114-275。
uname -v	显示操作系统版本。
uname -m	显示运行系统的硬件的机器 ID 号。
uname -u	显示系统 ID 号。
AIX

系统上运行的 AIX 的版本、发布版本和维护级别是什么？

输入以下命令之一：

oslevel -r

lslpp -h bos.rte

如何判断某个 AIX 级别缺少哪些文件集更新？

例如，要想判断 5300-04 缺少哪些文件集更新，运行以下命令：

oslevel -rl 5300-04

系统上安装了哪个 SP (Service Pack)？

要想查明系统上当前安装的是哪个 SP，运行 oslevel -s 命令。对于带 TL4 并安装了 SP2 的 AIX 5L Version 5.3 系统，输出如下：

oslevel –s
5300-04-02

系统上是否安装了 CSP (Concluding Service Pack)？

要想查明系统上当前是否安装了 CSP，运行 oslevel -s 命令。对于带 TL3 并安装了 CSP 的 AIX 5L Version 5.3 系统，输出如下：

oslevel –s
5300-03-CSP

如何创建文件系统？

以下命令将在卷组 testvg 中创建一个 jfs 文件系统，大小为 10MB，挂载点是 /fs1：

crfs -v jfs -g testvg -a size=10M -m /fs1

以下命令将在卷组 testvg 中创建一个 jfs2 文件系统，大小为 10MB，挂载点是 /fs2，具有只读权限：

crfs -v jfs2 -g testvg -a size=10M -p ro -m /fs2

如何改变文件的大小？

要想把 /usr 文件系统增大 1000000 个 512 字节的块，输入：

chfs -a size=+1000000 /usr

注意：
在 AIX V5.3 中，还可以缩小 JFS2 文件系统。

如何挂载 CD？

输入以下命令：

mount -V cdrfs -o ro /dev/cd0 /cdrom

如何挂载文件系统？

以下命令把文件系统 /dev/fslv02 挂载在 /test 目录上：

mount /dev/fslv02 /test

如何挂载所有默认文件系统（/etc/filesystems 文件中标有 mount=true 属性的所有标准文件系统）？

以下命令将挂载所有这些文件系统：

mount {-a|all}

如何卸载文件系统？

输入以下命令卸载 /test 文件系统：

umount /test

如何显示已经挂载的文件系统？

输入以下命令显示当前挂载的所有文件系统的相关信息：

mount

如何删除文件系统？

输入以下命令删除 /test 文件系统：

rmfs /test

如何对文件系统进行碎片整理？

可以使用 defragfs 命令改进或报告文件系统中连续空间的状态。例如，使用以下命令对 /home 文件系统进行碎片整理：

defragfs /home

哪个文件集包含某个二进制程序？

要想显示 bos.acct 包含 /usr/bin/vmstat，输入：

lslpp -w /usr/bin/vmstat

要想显示 bos.perf.tools 包含 /usr/bin/svmon，输入：

which_fileset svmon

如何显示关于系统上安装的文件集的信息？

输入以下命令：

lslpp -l

如何判断系统上是否安装了维护级别的所有文件集？

输入以下命令：

instfix -i | grep ML

如何判断系统上是否安装了一个修补程序？

要想判断是否安装了 IY24043，输入：

instfix -ik IY24043

如何通过 APAR 安装修补程序？

例如，要想从 /dev/cd0 安装 APAR IY73748，输入以下命令：

instfix -k IY73748 -d /dev/cd0

如何检查所需的文件集是否完全安装好了？

要想显示需要安装或纠正哪些文件集，输入：

lppchk -v

如何对装载器部分的头信息和采用符号表示法的符号项进行转储？

输入以下命令：

dump -Htv

如何判断已经分配和正在使用的分页空间数量？

输入以下命令：

lsps -a

如何加大分页空间？

可以使用 chps -s 命令动态地增加分页空间的大小。例如，如果希望把 hd6 加大三个逻辑分区，那么执行以下命令：

chps -s 3 hd6

如何减小分页空间？

可以使用 chps -d 命令动态地减小分页空间。例如，如果希望把 hd6 减小四个逻辑分区，那么执行以下命令：

chps -d 4 hd6

如何查明系统是否能够使用 Simultaneous Multi-threading (SMT)？

如果系统是运行 AIX 5L Version 5.3 的基于 POWER5? 的系统，就能够使用 SMT。

如何查明系统是否启用了 SMT？

如果不带任何选项运行 smtctl 命令，它就会指出是否启用了 SMT？

32 位内核是否支持 SMT？

是的，32 位和 64 位内核都支持 SMT。

如何启用或禁用 SMT？

可以通过运行 smtctl 命令启用或禁用 SMT。语法如下：

smtctl [ -m off | on [ -w boot | now]]

可以使用以下选项：

-m off	把 SMT 模式设置为禁用。
-m on	把 SMT 模式设置为启用。
-w boot	如果在下一次系统重新引导之前运行 bosboot 命令，这个选项使 SMT 模式修改在以后的重新引导时仍然有效。
-w now	使 SMT 模式修改立即生效，但是在重新引导之后失效。
如果既没有指定 -w boot 选项，也没有指定 -w now 选项，那么模式修改立即生效。如果在下一次系统重新引导之前运行 bosboot 命令，那么修改在以后的重新引导时仍然有效。

如何获得与分区相关的信息和统计数据？

lparstat 命令提供分区信息和利用率统计数据报告。这个命令还显示 Hypervisor 信息。

卷组和逻辑卷

如何查明卷组是一般卷组、大卷组还是可伸缩卷组？

在卷组上运行 lsvg 命令并查看 MAX PVs 的值。值为 32 代表一般卷组，128 代表大卷组，1024 代表可伸缩卷组。

如何创建卷组？

使用以下命令，其中的 s partition_size 设置每个物理分区的大小（以 MB 为单位），partition_size 的范围是从 1 到 1024。（在 AIX V5.3 上是从 1 到 131072）.partition_size 变量必须是 2 的幂（例如，1、2、4、8）。对于标准卷组和大卷组，默认值是满足 “每个物理卷最多 1016 个物理分区” 限制的最低值。可伸缩卷组的默认值为满足 “每个物理卷最多容纳 2040 个物理分区” 限制的最低值。

mkvg -y name_of_volume_group -s partition_size list_of_hard_disks

如何修改卷组的特征？

可以使用以下命令修改卷组的特征：

chvg

如何创建逻辑卷？

输入以下命令：

mklv -y name_of_logical_volume name_of_volume_group number_of_partition

如何增加逻辑卷的大小？

例如，要想将 lv05 目录所表示的逻辑卷增加三个逻辑分区，输入：

extendlv lv05 3

如何显示属于某个卷组（例如，rootvg）的所有逻辑卷？

可以通过输入以下命令来显示属于 rootvg 的所有逻辑卷：

lsvg -l rootvg

如何列出有关逻辑卷的信息？

运行以下命令显示有关逻辑卷 lv1 的信息：

lslv lv1

如何删除逻辑卷？

可以运行以下命令删除逻辑卷 lv7：

rmlv lv7

rmlv 命令仅删除逻辑卷，但不删除其他实体，例如使用该逻辑卷的文件系统或分页空间。

如何镜像逻辑卷？

mklvcopy LogicalVolumeName Numberofcopies
syncvg VolumeGroupName
如何删除逻辑卷的拷贝？

可以使用 rmlvcopy 命令删除逻辑卷的逻辑分区拷贝。要想减少属于逻辑卷 testlv 的每个逻辑分区的拷贝数量，输入：

rmlvcopy testlv 2

现在此逻辑卷中每个逻辑分区最多只有两个物理分区。

查询有关卷组的信息

要想显示系统中的卷组，输入：

lsvg

要想显示 rootvg 的所有特征，输入：

lsvg rootvg

要想显示 rootvg 所使用的磁盘，输入：

lsvg -p rootvg

如何将磁盘添加到卷组中？

输入以下命令：

extendvg VolumeGroupName hdisk0 hdisk1 ... hdiskn

如何查明硬盘所支持的最大逻辑磁道组 (LTG) 大小？

可以使用带 -M 标志的 lquerypv 命令。此命令的输出给出以 KB 为单位的 LTG 大小。例如，在下面的示例中，hdisk0 的 LTG 大小为 256 KB。

/usr/sbin/lquerypv -M hdisk0
256

还可以在硬盘上运行 lspv 并查看 MAX REQUEST 的值。

syncvg 命令的作用是什么？

syncvg 命令用于同步过时的物理分区。它接受逻辑卷、物理卷或卷组名称作为参数。

例如，要想同步位于物理卷 hdisk6 和 hdisk7 上的物理分区，使用以下命令：

syncvg -p hdisk6 hdisk7

要想同步卷组 testvg 中的所有物理分区，使用以下命令：

syncvg -v testvg

如何替换某个磁盘？

extendvg VolumeGroupName  hdisk_new
migratepv hdisk_bad hdisk_new
reducevg -d VolumeGroupName hdisk_bad
如何克隆 rootvg（创建拷贝）？

可以运行 alt_disk_copy 命令将当前的 rootvg 复制到某个替代磁盘。下面的示例演示如何将 rootvg 克隆到 hdisk1。

alt_disk_copy -d hdisk1

网络

如何显示或设置网络参数的值？

no 命令设置或显示网络调优参数的当前值或下一次启动时的值。

如何获得计算机的 IP 地址？

输入以下命令之一：

ifconfig -a

host Fully_Qualified_Host_Name

例如，输入 host cyclop.austin.ibm.com。

如何确定服务器上的网络接口？

以下两个命令都显示网络接口：

lsdev -Cc if

ifconfig -a

要想获得有关某个特定网络接口（例如，tr0）的信息，运行以下命令：

ifconfig tr0

如何激活网络接口？

要想激活网络接口 tr0，运行以下命令：

ifconfig tr0 up

如何禁用网络接口？

要想禁用网络接口 tr0，运行以下命令：

ifconfig tr0 down

如何显示路由表、接口和协议信息？

要想显示因特网接口的路由表信息，输入：

netstat -r -f inet

要想显示因特网接口的接口信息，输入：

netstat -i -f inet

要想显示每个协议的统计数据，输入：

netstat -s -f inet

如何记录接收或发送的数据包？

要想记录每个接口上接收或发送的数据包，输入：

iptrace /tmp/nettrace

跟踪信息放在 /tmp/nettrace 文件中。

要想记录 en0 接口上通过 telnet 端口从远程主机 airmail 接收的数据包，输入：

iptrace -i en0 -p telnet -s airmail /tmp/telnet.trace

跟踪信息放在 /tmp/telnet.trace 文件中。

工作负载分区

如何创建工作负载分区？

要想用 IP 地址 xxx.yyy.zzz.nnn 创建工作负载分区 temp，输入：

mkwpar -n temp -N address= xxx.yyy.zzz.nnn

要想用规格说明文件 wpar1.spec 创建工作负载分区，输入：

mkwpar -f /tmp/wpar1.spec

如何为现有的工作负载分区 wpar1 创建新的规格说明文件？

要想为现有的工作负载分区 wpar1 创建新的规格说明文件 wpar2.spec，输入：

mkwpar -e wpar1 -o /tmp/wpar2.spec -w

如何启动工作负载分区？

要想启动工作负载分区 temp，输入：

startwpar temp

如何停止工作负载分区？

要想停止工作负载分区 temp，输入：

stopwpar temp

如何查看工作负载分区的特征？

要想查看所有工作负载分区的特征，输入：

lswpar

Name State Type Hostname Directory
---------------------------------------------------------------------------------
bar A S bar.austin.ibm.com /wpars/bar
foo D S foo.austin.ibm.com /wpars/foo
trigger A A trigger /

如何登录工作负载分区？

要想作为用户 foo 登录工作负载分区 wpar1，输入：

clogin wpar1 -l foo

如何在工作负载分区中运行命令？

要想作为用户 root 在工作负载分区 howdy 中运行 /usr/bin/ps 命令，输入：

clogin howdy -l root /usr/bin/ps

如何删除工作负载分区？

要想删除工作负载分区 temp，输入：

rmwpar temp

要想停止工作负载分区 temp 并删除在它的文件系统中保留的数据，输入：

rmwpar -p -s temp

注意：工作负载分区 (WPAR) 是 IBM AIX Version 6.1 中引入的一组全新的基于软件的系统虚拟化特性。

性能监视工具

如何显示虚拟内存统计数据？

要想显示自引导以来的虚拟内存统计数据汇总，输入：

vmstat

要想以 2 秒的时间间隔显示 5 个汇总报告，输入：

vmstat 2 5

要想显示所有工作负载分区自引导以来的统计数据汇总，输入：

vmstat -@ ALL

要想显示所有工作负载分区可用的所有虚拟内存统计数据，输入：

vmstat -vs -@ ALL

如何显示所有 TTY、CPU 和磁盘的统计数据？

要想显示所有 TTY、CPU 和磁盘自引导以来的一组统计数据，输入：

iostat

要想以 2 秒的时间间隔连续显示逻辑名为 disk1 的磁盘的磁盘报告，输入：

iostat -d disk1 2

要想以 2 秒的时间间隔显示逻辑名为 disk1 的磁盘的 6 个报告，输入：

iostat disk1 2 6

要想以 2 秒的时间间隔显示所有磁盘的 6 个报告，输入：

iostat -d 2 6

要想只显示所有工作负载分区的文件系统统计数据，输入：

iostat -F -@ ALL

要想显示系统上所有工作负载分区的系统吞吐量，输入：

iostat -s -@ ALL

如何显示本地和远程系统的详细统计数据？

输入以下命令：

topas

要想直接显示进程信息，输入：

topas -P

要想直接显示逻辑分区信息，输入：

topas -L

要想直接显示磁盘指标，输入：

topas -D

要想直接显示文件系统信息，输入：

topas -F

如何报告系统单元活动？

输入以下命令：

sar

要想报告前两个处理器的处理器活动，输入：

sar -u -P 0,1

这会产生下面这样的输出：

cpu %usr %sys %wio %idle
0 45 45 5 5
1 27 65 3 5
 
 

常用AIX论坛地址介绍


AIX论坛：
http://www.loveunix.net/style_images/1/logo4.gif[/img][/URL]《爱U家园》是大家的快乐空间
http://www.LoveUnix.net
http://www.passcisco.com/bbs/list.asp?boardid=29 ; AIX使用者论坛
http://www.chinaunix.net/cgi-bin/bbs/forums.cgi?forum=5 ; chinaunix的AIX论坛
http://www.aixchina.com ; AIX中国论坛
http://www.swg.com.cn/bbs/cgi-bin/leoboard.cgi ; 思达奇公司的AIX 技术区
http://www.itpub.net/forumdisplay.php?s=&forumid=29 ; itpub的UNIX论坛
http://www.ibmusers.com/ ; 银信公司网站
http://bbs.interconn.com.cn/cgi-bin/forums.cgi?forum=2

AIX资料下载：
http://www.redbooks.ibm.com/ ;
http://www-1.ibm.com/servers/eserver/pseries/library/hardware_docs/
http://www-900.ibm.com/cn/support/download/r6download.shtml
http://publib.boulder.ibm.com/pseries/hacmp/hacmp_index.html
http://www-1.ibm.com/servers/eserver/pseries/library/hacmp_docs.html
http://www.storage.ibm.com/hardsoft/products/ssa/docs/index.html
http://www.alphaworks.ibm.com/
http://www.ibm.com/certify

http://www.cnblogs.com/Mainz/articles/1027105.html
