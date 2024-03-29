# 环境搭建

学习Linux就需要在Linux系统环境里面进行，一般常用三种方式来搭建环境：

1. 下载Linux系统ISO镜像文件，在电脑中装双系统（不推荐，占用电脑硬件资源）；
2. 下载Linux系统ISO镜像文件，在虚拟机中装系统（不推荐，占用电脑硬件资源）；
3. 直接购买Linux云服务器（推荐）

这里就不讲解电脑装双系统了，自行百度，主要讲解第2、3种方案。

## 虚拟机安装

### 下载Linux

访问[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)搜索“centos”，点击第一个

![QQ截图20210724224011](Image/QQ截图20210724224011.png)

选择合适版本：

![QQ截图20210724224213](Image/QQ截图20210724224213.png)

选择文件类型：

![QQ截图20210724224418](Image/QQ截图20210724224418.png)

选择x86_64：

![QQ截图20210724224504](Image/QQ截图20210724224504.png)

选择包含dvd文件（标准版）下载：

![QQ截图20210724224644](Image/QQ截图20210724224644.png)

### VMware虚拟机

VMware Workstation是一款功能强大的桌面[虚拟计算机](https://baike.baidu.com/item/虚拟计算机/5732003)软件，让用户可在单一的桌面上同时运行不同的操作系统。因其可在一部实体机器上模拟完整的网络环境，以及可便于携带的[虚拟机](https://baike.baidu.com/item/虚拟机)器，其更好的灵活性与先进的技术胜过了市面上其他的虚拟计算机软件。

![fcd6dbfd44240e186fe7917765e08f71](Image/fcd6dbfd44240e186fe7917765e08f71.jpg)

因为官网下载较慢，VMware虚拟机可以直接在360软件管家中下载：

![QQ截图20210724230131](Image/QQ截图20210724230131.png)

安装完成后打开软件：

![QQ截图20210725033341](Image/QQ截图20210725033341.png)

选择“创建新的虚拟机”，选择前面我们下载好的centos镜像文件：

![QQ截图20210725033717](Image/QQ截图20210725033717.png)

设置用户名、密码：

![QQ截图20210725033825](Image/QQ截图20210725033825.png)

后面自定义选择安装位置，这样建立好了一个新的虚拟机，并且自动运行安装程序：

![QQ截图20210725034210](Image/QQ截图20210725034210.png)

### 账户切换

安装完成以后界面如下：其中“Linux”这个账户就是前面安装centos过程中设置的全名，如果要登录root户点击“Not listed?”：

![QQ截图20210725040410](Image/QQ截图20210725040410.png)

点击Linux输入之前设置的密码，点击“Sign In”登录：

![QQ截图20210725040801](Image/QQ截图20210725040801.png)

登录后界面：

![QQ截图20210725043546](Image/QQ截图20210725043546.png)

点击左上角的"Actitities"就可以看到预装的一些软件了：

![QQ截图20210725043614](Image/QQ截图20210725043614.png)

点击上图中红框中的命令行：**可以看到一个admin开头的命令头，这个admin就是前面设置的账户名，是一个普通权限的账户。**

![QQ截图20210725102252](Image/QQ截图20210725102252.png)

点击右上关机键，点击Linux名称，点击“Log Out”角退出登录：

![QQ截图20210725102613](Image/QQ截图20210725102613.png)

回到登录界面，点击“not listed?”，登录root用户（第一次进入：用户名“root”，密码“123456”）：

![QQ截图20210725040410](Image/QQ截图20210725040410.png)

![QQ截图20210725102949](Image/QQ截图20210725102949.png)

![QQ截图20210725103007](Image/QQ截图20210725103007.png)

和上面一样，点击左上角的"Actitities"，点击命令行：**可以看到一个root开头的命令头，是最高权限的账户。**

![QQ截图20210725103222](Image/QQ截图20210725103222.png)

## 云服务器

云服务器：**一台提供简单高效、安全可靠、处理能力可弹性伸缩的计算服务的远程电脑。**

优势：24小时全天候开机，稳定性有保障，真实的线上环境。

### 云服务器购买

云服务器推荐购买阿里云，这也是国内用的最多的云服务器，真实的线上环境：[阿里云官网](https://www.aliyun.com/?spm=5176.8789780.J_8058803260.1.175b45b5Dy7Bh1)

![QQ截图20210725105803](Image/QQ截图20210725105803.png)

点击“产品”，点击“云服务器ECS”：

![QQ截图20210725105901](Image/QQ截图20210725105901.png)

点击“立即购买”：

![QQ截图20210725110034](Image/QQ截图20210725110034.png)

这里就开始配置服务器的硬件了，价格越高硬件就越好，服务器的性能就越好，根据个人经济实实力来确定（注意选择安装的系统为centos，版本为8.4）：

![QQ截图20210725110220](Image/QQ截图20210725110220.png)

通常第一次购买云服务器的新人有活动可以免费使用云服务器，活动地址：https://www.aliyun.com/activity?spm=5176.8789780.J_8058803260.2.6b6a45b5sCuyTA

![QQ截图20210729004518](Image/QQ截图20210729004518.png)

订单标明了这台云服务器的配置和安装的系统及系统版本：

![QQ截图20210728235152](Image/QQ截图20210728235152.png)

### 云服务器配置

购买好云服务器后，点击“管理控制台”：

![QQ截图20210729004647](Image/QQ截图20210729004647.png)

在控制台里面就会看到一个服务器实例（**实例名称为一串可变的随机字符，不可变的公网IP为121.199.26.242**）：

![QQ截图20210729004827](Image/QQ截图20210729004827.png)

点击左侧栏“实例”选项，也可以看到该实例选项：

![QQ截图20210729005253](Image/QQ截图20210729005253.png)

点击该实例选项，可以看到该实例配置的详细信息：

![QQ截图20210730204441](Image/QQ截图20210730204441.png)

### 重置实例密码

**购买云服务器后首先要重置实例密码，这样我们才能连接我们的服务器。**

点击上图中“重置实例密码”，初次重置密码的用户名都是“root”（最高权限用户）：

![QQ截图20210730204832](Image/QQ截图20210730204832.png)

重置密码后会要求重启，点击“立即重启”即可：

![QQ截图20210730205051](Image/QQ截图20210730205051.png)

### 修改实例名称

如果我们想修改实例的名称，可以点击“修改实例名称”：

![QQ截图20210730210003](Image/QQ截图20210730210003.png)

输入自定义的名称，点击“确定”即可：

![QQ截图20210730210157](Image/QQ截图20210730210157.png)

### 设置安全组

**上面配置好以后，一定还需要设置阿里云的安全组，开放端口号，否则外界无法访问！**

点击实例上面的“安全组”选项：

![QQ截图20210730210607](Image/QQ截图20210730210607.png)

进入后，有三个选项卡，分别如下：

**内网入方向全部规则：控制外部方向连接云服务器的配置（需要配置）。**

**内网出方向全部规则：控制云服务器连接外部方向的配置（默认不改动）。**

**安全组列表：控制安全组配置规则的（需要配置）。**

点击“内网入方向全部规则”，界面如下：

![QQ截图20210730211248](Image/QQ截图20210730211248.png)

这里首先默认打开了3个端口，这里我们还可以增加一些端口，点击“安全组列表”，点击“安全组ID”：

![QQ截图20210731155602](Image/QQ截图20210731155602.png)

进入后，点击“手动添加”选项：

![QQ截图20210731160232](Image/QQ截图20210731160232.png)

输入想开启的端口号、源、描述，点击“保存”即可（源默认是0.0.0.0，所有人可访问）：

![QQ截图20210731160343](Image/QQ截图20210731160343.png)

这时端口就开启成功：

![QQ截图20210731160549](Image/QQ截图20210731160549.png)

我们可以把常用端口打开，列表如下：

| 端口 | 作用                  |
| ---- | --------------------- |
| 21   | FTP文件传输协议(控制) |
| 22   | SSH远程登录协议       |
| 80   | HTTP协议              |
| 443  | HTTPS协议             |
| 3306 | MySQL常用端口         |
| 6379 | Redis常用端口         |

