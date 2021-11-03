# 网络传输

## 网络配置

### 网络配置工具

网络配置工具 - **ifconfig**

```
ifconfig：查看和设置网卡信息（eth0第一网卡，eth1第二块网卡，lo回环网卡（虚拟））
ifconfig eth0 IP地址：设置网卡eth0指定的IP地址
setup：设置IP地址（DHCP[*]自动配置IP地址，没有DHCP服务就去掉*，重启network服务生效（service network restart），永久生效）
```

![QQ截图20211017223103](Image/QQ截图20211017223103.png)

### 配置IP

执行`ifconfig`命令，记录eth0中网卡MAC地址，即`HWaddr`的值

编辑ifcfg-eth0配置文件

```
vim /etc/sysconfig/network-scripts/ifcfg-eth0 
```

内容为：

注意：这里设置的IP不能与虚拟网卡VirtualBox、VMnet1、VMnet8中的IP起冲突。

```
DEVICE=eth0                                # 设备名称eth0
BOOTPROTO=static                           # 地址类型静态
HWADDR=00:50:56:2D:C7:70                   # 上面记录的HWaddr的值
TYPE=Ethernet                              # 网络类型
UUID=a003d5b9-f6c3-456c-b475-390bdc93f734  # 唯一标识
ONBOOT=yes                                 # 自动加载
NM_CONTROLLED=yes                          # NNetwork Manager托管
IPADDR=192.168.1.120                       # IP地址
NETMASK=255.255.255.0                      # 子网掩码
GATEWAY=192.168.1.1                        # 网关
```

退出保存后，重启network

```
service network restart
```

## 网络检查

### 端口查看

显示网络相关信息 - **netstat**

- **-l** - 监听
- **-r** - 路由
- **-n** - 显示IP地址和端口号
- **-tuln** - 查看监听端口
- **-an** - 查看所有网络连接（ESTABL LSHED连接状态，发起端口随机，目标端口固定）
- **-rn** - 查看路由表

### 连通性检查

网络可达性检查 - **ping**

```
ping IP地址：测试与指定IP地址是否网络相通
ping -c 4 IP地址：给指定的IP地址发送4个数据包
```

显示或管理路由表 - **route**。

查看网络服务和端口 - **netstat** / **ss**

```
[root ~]# netstat -nap | grep nginx
```

网络监听抓包 - **tcpdump**

## 文件传输

## 压缩解压

在Linux当中常见的压缩格式：`.zip`、`.gzip`、`.tbz`。

将文件或目录压缩为zip格式 - **zip 压缩后文件名称.zip 被压缩的文件或目录名称**

![QQ截图20210831010856](Image/QQ截图20210831010856.png)

将zip格式的文件解压 - **unzip 压缩文件.zip**

![QQ截图20210831011404](Image/QQ截图20210831011404.png)

将文件压缩为gzip格式 - **gzip 文件名称**

![QQ截图20210831012442](Image/QQ截图20210831012442.png)

将gzip格式的文件解压 - **gunzip 文件名称.gz**

![QQ截图20210831013042](Image/QQ截图20210831013042.png)

!> gzip格式不能压缩文件夹，且在压缩或解压后均不会保留源文件。

bzip2格式文件的压缩和解压方式和gzip格式完全一样。

!> bzip2格式不能压缩文件夹，且在压缩或解压后均不会保留源文件。

## 打包解包

前面提到，gzip格式、bzip2格式不能对文件夹进行压缩，如果我们使用tar打包命令将文件夹打包为一个文件，就可以进行压缩了。

?> tar常规打包不会对内容进行压缩，反而还会变大。

打包命令 - **tar 参数 打包后的文件名称 被打包文件名称**

- `-c`：打包
- `-x`：拆包
- `-t`：不拆包，查看内容
- `-f`：指定文件
- `-v`：查看过程
- `-z`：使用gzip压缩解压
- `-j`：使用bzip2压缩解压

```
常规打包解包：
tar -cvf test.tar test  将test文件夹打包为test.tar文件
tar -tf test.tar        不拆包查看test.tar文件里面的文件
tar -xvf test.tar       将test.tar文件解包

使用gzip压缩解压：
tar -zcvf test.tgz test 使用gzip方式将test文件夹打包并压缩为test.tgz文件
tar -zxvf test.tgz      使用gzip方式将test.tgz文件解压缩解包

使用bzip2压缩解压：
tar -jcvf test.tbz test 使用bzip2方式将test文件夹打包并压缩为test.tbz文件
tar -jxvf test.tbz      使用bzip2方式将test.tbz文件解压缩解包
```

![QQ截图20210901011137](Image/QQ截图20210901011137.png)



安全文件拷贝 - **scp 参数**

- **-r** - 拷贝文件夹

**scp是基于ssh协议在两台linux之间拷贝文件的命令，前提是需要知道目标主机的IP地址和用户名及其对应的用户密码。**

```
格式：
scp /路径/文件名称 用户@IP地址:/路径/文件名称

例子：将本机/usr下的file1.txt文件拷贝至目标主机tmp下并重命名为file2.txt，执行命令后需要输入root登录172.19.216.195主机的密码
scp /usr/file1.txt root@172.19.216.195:/tmp/file2.txt
```

文件同步工具 - **rsync**

> 说明：使用`rsync`可以实现文件的自动同步，这个对于文件服务器来说相当重要。关于这个命令的用法，我们在后面讲项目部署的时候为大家详细说明。

安全文件传输 - **sftp**

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
