查看命令的说明和位置 - **whatis** / **which** / **whereis**。

```
[root ~]# whatis ps
ps (1)        - report a snapshot of the current processes.
[root ~]# whatis python
python (1)    - an interpreted, interactive, object-oriented programming language
[root ~]# whereis ps
ps: /usr/bin/ps /usr/share/man/man1/ps.1.gz
[root ~]# whereis python
python: /usr/bin/python /usr/bin/python2.7 /usr/lib/python2.7 /usr/lib64/python2.7 /etc/python /usr/include/python2.7 /usr/share/man/man1/python.1.gz
[root ~]# which ps
/usr/bin/ps
[root ~]# which python
/usr/bin/python
```

1. 查找文件和查找内容 - **find** / **grep**。

    > **说明**：`grep`在搜索字符串时可以使用正则表达式，如果需要使用正则表达式可以用`grep -E`或者直接使用`egrep`。

#### 管道和重定向

1. 管道的使用 - **|**。

    例子：查找当前目录下文件个数。

    ```
    [root ~]# find ./ | wc -l6152
    ```

    例子：列出当前路径下的文件和文件夹，给每一项加一个编号。

    ```
    [root ~]# ls | cat -n     1  dump.rdb     2  mongodb-3.6.5     3  Python-3.6.5     4  redis-3.2.11     5  redis.conf
    ```

    例子：查找record.log中包含AAA，但不包含BBB的记录的总数

    ```
    [root ~]# cat record.log | grep AAA | grep -v BBB | wc -l
    ```

2. 别名


1. **alias**

    ```
    [root ~]# alias ll='ls -l'[root ~]# alias frm='rm -rf'[root ~]# ll...drwxr-xr-x  2 root       root   4096 Jun 20 12:52 abc...[root ~]# frm abc
    ```

2. **unalias**

    ```
    [root ~]# unalias frm[root ~]# frm sohu.html-bash: frm: command not found
    ```


### 配置服务

我们可以Linux系统下安装和配置各种服务，也就是说我们可以把Linux系统打造成数据库服务器、Web服务器、缓存服务器、文件服务器、消息队列服务器等等。Linux下的大多数服务都被设置为守护进程（驻留在系统后台运行，但不会因为服务还在运行而导致Linux无法停止运行），所以我们安装的服务通常名字后面都有一个字母`d`，它是英文单词`daemon`的缩写，例如：防火墙服务叫firewalld，我们之前安装的MySQL服务叫mysqld，Apache服务器叫httpd等。在安装好服务之后，可以使用`systemctl`命令或`service`命令来完成对服务的启动、停止等操作，具体操作如下所示。

1. 启动防火墙服务。

    ```
    [root ~]# systemctl start firewalld
    ```

2. 终止防火墙服务。

    ```
    [root ~]# systemctl stop firewalld
    ```

3. 重启防火墙服务。

    ```
    [root ~]# systemctl restart firewalld
    ```

4. 查看防火墙服务状态。

    ```
    [root ~]# systemctl status firewalld
    ```

5. 设置/禁用防火墙服务开机自启。

    ```
    [root ~]# systemctl enable firewalldCreated symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.[root ~]# systemctl disable firewalldRemoved symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
    ```

### 计划任务

1. 在指定的时间执行命令。

    - **at** - 将任务排队，在指定的时间执行。
    - **atq** - 查看待执行的任务队列。
    - **atrm** - 从队列中删除待执行的任务。

    指定3天以后下午5点要执行的任务。

    ```
    [root ~]# at 5pm+3daysat> rm -f /root/*.htmlat> <EOT>job 9 at Wed Jun  5 17:00:00 2019
    ```

    查看待执行的任务队列。

    ```
    [root ~]# atq9       Wed Jun  5 17:00:00 2019 a root
    ```

    从队列中删除指定的任务。

    ```
    [root ~]$ atrm 9
    ```

2. 计划任务表 - **crontab**。

    ```
    [root ~]# crontab -e* * * * * echo "hello, world!" >> /root/hello.txt59 23 * * * rm -f /root/*.log
    ```

    > 说明：输入`crontab -e`命令会打开vim来编辑Cron表达式并指定触发的任务，上面我们定制了两个计划任务，一个是每分钟向/root目录下的hello.txt中追加输出`hello, world!`；另一个是每天23时59分执行删除/root目录下以log为后缀名的文件。如果不知道Cron表达式如何书写，可以参照/etc/crontab文件中的提示（下面会讲到）或者用搜索引擎找一下“Cron表达式在线生成器”来生成Cron表达式。

    和crontab相关的文件在`/etc`目录下，通过修改`/etc`目录下的crontab文件也能够定制计划任务。

    ```
    [root ~]# cd /etc[root etc]# ls -l | grep cron-rw-------.  1 root root      541 Aug  3  2017 anacrontabdrwxr-xr-x.  2 root root     4096 Mar 27 11:56 cron.ddrwxr-xr-x.  2 root root     4096 Mar 27 11:51 cron.daily-rw-------.  1 root root        0 Aug  3  2017 cron.denydrwxr-xr-x.  2 root root     4096 Mar 27 11:50 cron.hourlydrwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.monthly-rw-r--r--   1 root root      493 Jun 23 15:09 crontabdrwxr-xr-x.  2 root root     4096 Jun 10  2014 cron.weekly[root etc]# vim crontab  1 SHELL=/bin/bash  2 PATH=/sbin:/bin:/usr/sbin:/usr/bin  3 MAILTO=root  4  5 # For details see man 4 crontabs  6  7 # Example of job definition:  8 # .---------------- minute (0 - 59)  9 # |  .------------- hour (0 - 23) 10 # |  |  .---------- day of month (1 - 31) 11 # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ... 12 # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat 13 # |  |  |  |  | 14 # *  *  *  *  * user-name  command to be executed
    ```

### 网络访问和管理

1. 安全远程连接 - **ssh**。

    ```
    [root ~]$ ssh root@120.77.222.217The authenticity of host '120.77.222.217 (120.77.222.217)' can't be established.ECDSA key fingerprint is SHA256:BhUhykv+FvnIL03I9cLRpWpaCxI91m9n7zBWrcXRa8w.ECDSA key fingerprint is MD5:cc:85:e9:f0:d7:07:1a:26:41:92:77:6b:7f:a0:92:65.Are you sure you want to continue connecting (yes/no)? yesWarning: Permanently added '120.77.222.217' (ECDSA) to the list of known hosts.root@120.77.222.217's password: 
    ```

    

4. 网络配置工具（旧） - **ifconfig**。

    ```
    [root ~]# ifconfig eth0eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500        inet 172.18.61.250  netmask 255.255.240.0  broadcast 172.18.63.255        ether 00:16:3e:02:b6:46  txqueuelen 1000  (Ethernet)        RX packets 1067841  bytes 1296732947 (1.2 GiB)        RX errors 0  dropped 0  overruns 0  frame 0        TX packets 409912  bytes 43569163 (41.5 MiB)        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 
    ```

5. 网络配置工具（新） - **ip**。

    ```
    [root ~]# ip address1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00    inet 127.0.0.1/8 scope host lo       valid_lft forever preferred_lft forever2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000    link/ether 00:16:3e:02:b6:46 brd ff:ff:ff:ff:ff:ff    inet 172.18.61.250/20 brd 172.18.63.255 scope global eth0       valid_lft forever preferred_lft forever
    ```

6. 网络可达性检查 - **ping**。

    ```
    [root ~]# ping www.baidu.com -c 3PING www.a.shifen.com (220.181.111.188) 56(84) bytes of data.64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=1 ttl=51 time=36.3 ms64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=2 ttl=51 time=36.4 ms64 bytes from 220.181.111.188 (220.181.111.188): icmp_seq=3 ttl=51 time=36.4 ms--- www.a.shifen.com ping statistics ---3 packets transmitted, 3 received, 0% packet loss, time 2002msrtt min/avg/max/mdev = 36.392/36.406/36.427/0.156 ms
    ```

7. 显示或管理路由表 - **route**。

8. 查看网络服务和端口 - **netstat** / **ss**。

    ```
    [root ~]# netstat -nap | grep nginx
    ```

9. 网络监听抓包 - **tcpdump**。

10. 安全文件拷贝 - **scp**。

```
[root ~]# scp root@1.2.3.4:/root/guido.jpg hellokitty@4.3.2.1:/home/hellokitty/pic.jpg
```

1. 文件同步工具 - **rsync**。

    > 说明：使用`rsync`可以实现文件的自动同步，这个对于文件服务器来说相当重要。关于这个命令的用法，我们在后面讲项目部署的时候为大家详细说明。

2. 安全文件传输 - **sftp**。

    ```
    [root ~]# sftp root@1.2.3.4root@1.2.3.4's password:Connected to 1.2.3.4.sftp>
    ```

    - `help`：显示帮助信息。
    - `ls`/`lls`：显示远端/本地目录列表。
    - `cd`/`lcd`：切换远端/本地路径。
    - `mkdir`/`lmkdir`：创建远端/本地目录。
    - `pwd`/`lpwd`：显示远端/本地当前工作目录。
    - `get`：下载文件。
    - `put`：上传文件。
    - `rm`：删除远端文件。
    - `bye`/`exit`/`quit`：退出sftp。

### 进程管理

1. 查找与指定条件匹配的进程 - **pgrep**。

    ```
    [root ~]$ pgrep mysqld3584
    ```

2. 通过进程号终止进程 - **kill**。

    ```
    [root ~]$ kill -l 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR111) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+338) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+843) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+1348) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-1253) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-758) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-263) SIGRTMAX-1  64) SIGRTMAX[root ~]# kill 1234[root ~]# kill -9 1234
    ```

    例子：用一条命令强制终止正在运行的Redis进程。

    ```
    ps -ef | grep redis | grep -v grep | awk '{print $2}' | xargs kill
    ```

3. 查询后台进程 - **jobs**。

    ```
    [root ~]# jobs[2]   Running                 mongod &[3]-  Stopped                 cat[4]+  Stopped                 redis-server
    ```

13. 查看当前运行级别 - **runlevel**。

    ```
    [root ~]# runlevelN 3
    ```

14. 实时监控进程占用资源状况 - **top**。

    ```
    [root ~]# toptop - 23:04:23 up 3 days, 14:10,  1 user,  load average: 0.00, 0.01, 0.05Tasks:  65 total,   1 running,  64 sleeping,   0 stopped,   0 zombie%Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 stKiB Mem :  1016168 total,   191060 free,   324700 used,   500408 buff/cacheKiB Swap:        0 total,        0 free,        0 used.   530944 avail Mem...
    ```

    - `-c` - 显示进程的整个路径。
    - `-d` - 指定两次刷屏之间的间隔时间（秒为单位）。
    - `-i` - 不显示闲置进程或僵尸进程。
    - `-p` - 显示指定进程的信息。

### 系统诊断

1. 系统启动异常诊断 - **dmesg**。

2. 查看系统活动信息 - **sar**。

    ```
    [root ~]# sar -u -r 5 10Linux 3.10.0-957.10.1.el7.x86_64 (izwz97tbgo9lkabnat2lo8z)      06/02/2019      _x86_64_        (2 CPU)06:48:30 PM     CPU     %user     %nice   %system   %iowait    %steal     %idle06:48:35 PM     all      0.10      0.00      0.10      0.00      0.00     99.8006:48:30 PM kbmemfree kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty06:48:35 PM   1772012   2108392     54.33    102816   1634528    784940     20.23    793328   1164704         0
    ```

    - `-A` - 显示所有设备（CPU、内存、磁盘）的运行状况。
    - `-u` - 显示所有CPU的负载情况。
    - `-d` - 显示所有磁盘的使用情况。
    - `-r` - 显示内存的使用情况。
    - `-n` - 显示网络运行状态。

3. 查看内存使用情况 - **free**。

    ```
    [root ~]# free              total        used        free      shared  buff/cache   availableMem:        1016168      323924      190452         356      501792      531800Swap:             0           0           0
    ```

4. 虚拟内存统计 - **vmstat**。

    ```
    [root ~]# vmstatprocs -----------memory---------- ---swap-- -----io---- -system-- ------cpu----- r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st 2  0      0 204020  79036 667532    0    0     5    18  101   58  1  0 99  0  0
    ```

5. CPU信息统计 - **mpstat**。

    ```
    [root ~]# mpstatLinux 3.10.0-957.5.1.el7.x86_64 (iZ8vba0s66jjlfmo601w4xZ)       05/30/2019      _x86_64_        (1 CPU)01:51:54 AM  CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle01:51:54 AM  all    0.71    0.00    0.17    0.04    0.00    0.00    0.00    0.00    0.00   99.07
    ```

6. 查看进程使用内存状况 - **pmap**。

    ```
    [root ~]# ps  PID TTY          TIME CMD 4581 pts/0    00:00:00 bash 5664 pts/0    00:00:00 ps[root ~]# pmap 45814581:   -bash0000000000400000    884K r-x-- bash00000000006dc000      4K r---- bash00000000006dd000     36K rw--- bash00000000006e6000     24K rw---   [ anon ]0000000001de0000    400K rw---   [ anon ]00007f82fe805000     48K r-x-- libnss_files-2.17.so00007f82fe811000   2044K ----- libnss_files-2.17.so...
    ```

7. 报告设备CPU和I/O统计信息 - **iostat**。

    ```
    [root ~]# iostatLinux 3.10.0-693.11.1.el7.x86_64 (iZwz97tbgo9lkabnat2lo8Z)      06/26/2018      _x86_64_       (1 CPU)avg-cpu:  %user   %nice %system %iowait  %steal   %idle           0.79    0.00    0.20    0.04    0.00   98.97Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtnvda               0.85         6.78        21.32    2106565    6623024vdb               0.00         0.01         0.00       2088          0
    ```


### 远连接

**注意：这里针对的是虚拟机，如果是购买的服务器，记住服务器的公网IP就行了。**

##### 虚拟机配置

Workstation——虚拟机——设置——网络适配器——NAT模式——确定

##### ssh

ssh是一个远程登录协议，默认端口号是22

```
yum install sshd-service  # 安装sshd服务
```

配置ssh

```
vim /etc/ssh/sshd_config
```

编辑内容为：

```
Port 22					# 端口号22Protocol 2				# ssh2类型PermitRootLogin yes	    # 允许任何类型登录
```

PermitRootLogin可以限定root用户通过ssh的登录方式，如禁止登陆、禁止密码登录、仅允许密钥登陆和开放登陆，以下是对可选项的概括：

| 参数类别             | ssh登陆 | 登录方式       | 交互shell          |
| -------------------- | ------- | -------------- | ------------------ |
| yes                  | 允许    | 没有限制       | 没有限制           |
| without-password     | 允许    | 除密码以外     | 没有限制           |
| forced-commands-only | 允许    | 仅允许使用密钥 | 仅允许已授权的命令 |
| no                   | 不允许  | N/A            | N/A                |

启动ssh服务

```
service sshd status		  # 查看sshd服务状态service sshd start		  # 启动sshd服务service sshd restart      # 重启sshd服务service sshd stop		  # 停止sshd服务
```

##### 配置IP

执行`ifconfig`命令，记录eth0中网卡MAC地址，即`HWaddr`的值

编辑ifcfg-eth0配置文件

```
vim /etc/sysconfig/network-scripts/ifcfg-eth0 
```

内容为：

**注意：这里设置的IP不能与虚拟网卡VirtualBox、VMnet1、VMnet8中的IP起冲突。**

```
DEVICE=eth0									# 设备名称eth0BOOTPROTO=static							# 地址类型静态HWADDR=00:50:56:2D:C7:70					# 上面记录的HWaddr的值TYPE=Ethernet								# 网络类型UUID=a003d5b9-f6c3-456c-b475-390bdc93f734	# 唯一标识ONBOOT=yes									# 自动加载NM_CONTROLLED=yes							# NNetwork Manager托管IPADDR=192.168.1.120						# IP地址NETMASK=255.255.255.0						# 子网掩码GATEWAY=192.168.1.1							# 网关
```

退出保存后，重启network

```
service network restart
```

##### 端口查看

```
netstat：显示网络相关信息（-l监听，-r路由，-n显示IP地址和端口号，-tuln查看监听端口，-an查看所有网络连接（ESTABL LSHED连接状态，发起端口随机，目标端口固定），-rn查看路由表）
```

##### 网络配置

```
ifconfig：查看和设置网卡信息（eth0第一网卡，eth1第二块网卡，lo回环网卡（虚拟））ifconfig eth0 192.168.8.250：设置虚拟网卡eth0的IP地址为192.168.8.250setup：设置IP地址（DHCP[*]自动配置IP地址，没有DHCP服务就去掉*，重启network服务生效（service network restart），永久生效）
```

##### 连接测试

```
ping 192.168.1.1：测试与192.168.1.1的IP地址是否网络相通（它会一直ping，ctrl+c停止）ping -c 4 192.168.1.1：给192.168.1.1的IP地址发送4个数据包
```



6、文件搜索
    find
    用法如下：
    find   在哪找   怎么找   找什么
    在哪找：就是一个路径，默认是当前路径
    怎么找：按照名字、大小、用户，其实就是参数
        -name : 按照名字找
        -size : 按照大小找
        -user : 按照用户找
        -group : 按照组找
        -maxdepth : 查找最大目录级别
        -mindepth : 查找最小目录级别
    找什么：1.mp3  *.txt

    find / -name dudu.pyfind / -size 10k     等于10k的文件             +10k     大于10k的文件            -10k     小于10k的文件find / *.txt -user liuyanfind / -maxdepth 3 -mindepth 2 -name *.txt  找指定级别的文件

day09-linux

1、文件内容搜索
    grep 内容 文件路径
    参数：
    -i ：忽略大小写
    --color=auto : 颜色自动提示，将grep设置为默认颜色提示，其实就是可以给grep指令器别名
        vi ~/.bashrc
        添加一句  alias grep='grep --color=auto'
        source ~/.bashrc
    -n : 显示内容出现的行号
    -l : 显示内容出现的文件名
    -c : 显示出现该内容的次数

    也可以写正则表达式, 注意使用 -P    13838384380    \d{11}    ^1\d{10}    3456789    ^1[3-9]\d{9}    test@qq.com   duduxixi@163.com  lalahehe@sina.cn    \w+@\w+\.(com|cn|net)grep 王者荣耀 1.txtgrep 王者荣耀 *.txtgrep 王者荣耀 ~/.txtgrep -P '1[3-9]\d{9}' 3.txt 

2、管道
    格式： 指令1 | 指令2
    指令1的输出作为指令2的输入，指令2的输出显示到屏幕中
    常用的管道指令有：
        ls -l /etc | less
        ls -l /etc | head -5
        ls -l /etc | tail -5
        ls -l /etc | head -10 | tail -5
        ls -l /etc | grep 找的内容
3、搭建主机信任
    密码学的内容，加密-解密，用到一个东西  秘钥
    加密-解密秘钥相同-对称加解密
    加密-解密秘钥不相同-非对称加解密
    一对儿秘钥：公钥和私钥
    公钥：给你们，你们拿的都是公钥
    私钥：我自己拥有，
    公钥加密-私钥解密，私钥加密-公钥解密
    实现免密码登录，linux1登录linux2，实现免密码登录
    （1）在linux1上，生成公钥和私钥
        ssh-keygen   一路敲enter即可
    （2）来到生成秘钥的文件中
        id_rsa : 私钥
        id_rsa.pub : 公钥
    （3）复制公钥
    （4）来到linux2中
        vi ~/.ssh/authorized_keys
        将公钥粘贴进来即可
    这样在通过linux1登录linux2的时候就实现了免密码登录
6、scp
    scp：基于ssh的cp，cp是实现本机之间来回拷贝，scp在两台linux之间进行拷贝
    scp的用法：
        scp 源路径 目标路径
        scp 1.txt root@ip地址:路径
        如果发送文件夹，需要添加 -r 选项
    linux和linux之间使用scp进行互发，如果搭建了主机信任，不用输入密码
    winscp，实现windows和linux之间使用scp进行互发
        安装，使用即可，左边：windows目录，右边：linux目录，相互拖动即可
2、服务和进程相关指令
    linux的启动等级，打开这个文件   vi /etc/inittab
    0 : 关机等级
    1 : 单用户模式
    2 : 多用户的无网络模式
    3 : 多用户模式，有网络
    4 : 保留模式
    5 : 界面模式
    6 : 重启模式
    

    切换等级   init 0   init 1   init 6
    查看当前等级  runlevel   who -r
    whoami  : 我是谁，查看当前用户
    
    查看随开机启动的服务
    chkconfig --list
    赵灵儿
    随开机启动的服务，我们给他们起了一个非常好听的名字，守护进程（daemon）
    sshd   httpd   mysqld  其实就是一个随机开机启动的服务
    
    开启、关闭服务
        要有控制开启、关闭服务的脚本，比如iptables（防火墙）
        /etc/init.d/iptables start | stop | restart
        /etc/init.d/network start | stop | restart
        经常找脚本，太不方便了，将服务脚本放到  /etc/init.d ,如果支持服务模式，那么就可以使用如下指令开启和关闭
        service iptables start | stop | restart
        service network start | stop | restart
    
        一般情况，安装服务的时候，控制服务的脚本在安装包就有，但是有的没有，比如nginx没有
        自己按照的服务，你就可以将脚本放到  /etc/init.d 里面，然后通过service控制它的开启和关闭  service nginx start
    
    自己按照的服务随开机启动
        chkconfig nginx on   默认设置的等级为2345
        chkconfig nginx off
        还得给脚本权限，权限一般设置为755
        通过chkconfig --list 查看有没有配置成功
    
    进程相关指令
        top ： 实时查看系统的运行情况
        w ：查看系统的当前用户的链接情况
        free : -h  内存的使用情况
        ps : 查看进程相关信息
            ps -ef | grep ssh
            ps aux | grep ssh
        kill : 杀死一个进程
            kill -9 进程id
        netstat -lnp : 查看网络和端口使用情况
            netstat -lnp | grep 80

### 服务管理

启动服务（以docker服务为例）

```
systemctl start docker.service
```

关闭服务

```
systemctl stop docker.service
```

重启服务

```
systemctl restart docker.service
```

显示服务状态

```
systemctl status docker.service
```

设置服务自启动

```
systemctl enable docker.service
```

禁止服务自启动

```
systemctl disable docker.service
```

查看服务是否自启动

```
systemctl is-enabled docker.service
```

列出所有自启动服务

```
systemctl list-unit-files|grep enabled
```

列出系统所有服务的启动情况

```
systemctl list-units --type=service
```



