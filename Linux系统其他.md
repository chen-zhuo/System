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
    
```

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



