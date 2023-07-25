# 服务器的部署以及基本数据库的同步

## 一.服务器部署

### 1.登录服务器实例命令

```bash
# -p 指定服务器端口号，默认 22
# root 为登录的用户名
# 192.168.56.102 为服务器ip，也可使用域名
$ ssh root@192.168.56.102 -p 22
```

### 2.网络通讯基本原理

公网IP:公网IP地址是全球范围内唯一标识一个设备或网络的IP地址。它是在互联网上可公开访问的IP地址，用于标识网络设备（如计算机、路由器、服务器等）在公共互联网中的位置。(每个局域网内的设备都有各自的一个独有的ip和一个局域网内共同的公网ip)

查询方法:

本机IP:cmd下输入:ipconfig

公网ip:百度搜索:ip地址查询

![image-20230725192128683](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251921826.png)



### 3.服务器连接原理

1.一旦云服务器实例创建完成，它将被分配一个公网IP地址，以便用户可以通过公网访问它。

2.云服务器被分配一个公网IP地址，这个IP地址允许用户从互联网上访问服务器。为了能够正确将数据传递到云服务器，用户需要了解服务器上运行的服务或应用程序所监听的端口号。用户在连接云服务器时，需要指定目标服务器的公网IP地址和正确的端口号。

3.要连接云服务器，用户需要在本地计算机或设备上运行支持远程连接的客户端软件。常见的远程连接协议包括SSH（Secure Shell）和RDP（Remote Desktop Protocol）。

4.远程连接协议： SSH协议用于远程连接Linux或类Unix系统的云服务器。用户使用SSH客户端软件通过互联网连接到云服务器，提供用户名和密码或SSH密钥进行身份验证，一旦成功认证，用户就可以在云服务器上执行命令和管理服务器。

### 4.服务器宝塔面板的安装

![image-20230725193153230](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251931287.png)

**#可点击在线安装也可以在服务器终端(RDP或者实例远程)进行安装**

#### **Centos安装脚本**

yum install -y wget && wget -O install.sh https://download.bt.cn/install/install_6.0.sh && sh install.sh ed8484bec

#### **Ubuntu/Deepin安装脚本**

wget -O install.sh https://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh ed8484bec

#### **Debian安装脚本**

wget -O install.sh https://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh ed8484bec

#### **万能安装脚本**

if [ -f /usr/bin/curl ];then curl -sSO https://download.bt.cn/install/install_panel.sh;else wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh;fi;bash install_panel.sh ed8484bec



### 5.软件商店宝塔页面安装软件



![image-20230725193943549](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251939715.png)



### 6.访问服务器内部一个html页面

#### 1.服务器公网IP添加站点

![image-20230725195124360](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251951432.png)

#### 2.添加html测试文件,注意根目录

![image-20230725195443796](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251954857.png)

#### 3.查看,输入正确路径

![image-20230725195735594](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307251957663.png)

## 二.数据库部署

### 1.端口与服务器配置

需要在服务器安全规则与宝塔面板开放3306端口(否则可能会连接失败,显示拒绝接入)

![image-20230725200810222](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252008258.png)

![image-20230725200623678](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252006739.png)

### 2.本地打开cmd窗口

,登录服务数据库(数据库权限需要修改可进入ip/或任意ip)#否则可能会连接失败,显示拒绝接入)



##还有一种第一次连接成功但是之后会失败的情况:

![image-20230725204129352](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252041397.png)

这种情况解决方法为使用完数据库后,未退出,短时间再次相同用户登录会有延迟



### 3.登录mysql

cmd输入:

mysql -u 用户名 -p -h 服务器ip

mysql -u joker -p -h8.130.92.162

![image-20230725201351922](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252013004.png)

### 4.备份数据库

备份所有数据库和表结构

```sql
mysqldump -u root -p --all-databases >文件名.sql
```

![image-20230725201948675](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252019711.png)



### 5.上传数据库

在宝塔数据库导入



![image-20230725203147833](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307252031899.png)

### 6.检查上传的数据库

完



