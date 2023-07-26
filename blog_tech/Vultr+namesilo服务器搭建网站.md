# Vultr+namesilo服务器搭建网站

## 一.vultr服务器的部署

### 1.注册账号以及购买VPS

注册成功后在支付宝购买(最低10$)

此处可以领取100$测试金额,但是最少充值10$后才可以使用 (https://www.vultr.com/?ref=9513606-8H)

![image-20230726205324773](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262053916.png)

之后点击蓝色+,第一个,部署新服务器

![image-20230726210038660](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262100781.png)

选择云计算,CPU选择inter性能较好一点

![image-20230726210007696](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262100799.png)

地区选择亚洲会更稳定(新加坡,韩国均可以),或者选择美国;镜像根据需要选择UBUNTU乌班图V20会更稳定

![image-20230726210256285](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262102376.png)

根据需要选择服务器配置,配置越高价格越贵,之后关闭自动备份(否则会增加6$),下面除了IPV6选择都需要加$

![image-20230726210543928](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262105996.png)



这里可以填写自己服务器介绍和名字,SSH可以不管,安全组不加是默认全部(全部选择后最低配最便宜6$)

![image-20230726211017683](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262110761.png)

之后可以在产品中查看自己实例

### 2.服务器的登录以及宝塔面板的安装

产品点击自己购买的实例查看地址以及密码,用户名为root,密码默认安全密码,可以复制

![image-20230726211706338](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262117477.png)

之后填写正确ip后点击连接

![image-20230726211932598](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262119694.png)

然后会弹出用户名与密码,填写实例页面的用户名(root)与密码

![image-20230726212123465](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262121539.png)

登录成功后会在这里提示用户名

![image-20230726212424098](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262124162.png)

之后进入宝塔官网,LINUX选择你购买服务器时选择的操作系统,复制安装代码到服务器控制终端,等待安装(需要输入两次yes确认安装)

![image-20230726212639170](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262126294.png)

安装成功后复制终端提示的内网地址浏览器打开登录;输入终端提示的账户密码(不用理会外网地址)

运维服务器在国外,登录时用点方法会快一些

登录成功后来到软件商店下载这几个常用

![image-20230726213156669](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262131782.png)

接下来该购买域名了

## 二.域名的购买与解析

#### 1.购买

进入namesilo注册(www.namesilo.com)

之后点击marketplace,选择自己想要的域名(根据后缀不同价格会不同)

![image-20230726213544623](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262135807.png)

一般来说越长的会越便宜

![image-20230726213826253](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262138393.png)

点击add后来到购物车,在箭头出输入优惠码可以便宜1$,但是最低1$,无法1-0=0;

![image-20230726214033038](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262140260.png)

#### 2.解析

之后来到个人账户,显示你的域名数量,点击箭头进入管理

![image-20230726214308478](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262143588.png)

来到页面点击这里

![image-20230726214353727](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262143761.png)

点击"你的域名格式"这边的DNS类型解析域名

这些域名系统（Domain Name System，DNS）记录类型，用于在域名系统中存储不同类型的信息。每个记录类型用于指定特定的功能和目的

- A记录（Address Record）：将域名映射到IPv4地址。它允许将域名解析为对应的IPv4地址，使得用户可以通过使用域名访问网站，而不必记住IP地址。
- AAAA记录（IPv6 Address Record）：类似于A记录，但用于将域名映射到IPv6地址。IPv6是下一代IP地址格式，支持更多的IP地址空间。
- CNAME记录（Canonical Name Record）：创建域名的别名，使得一个域名可以指向另一个域名。常用于实现重定向和简化多个域名指向同一主机的配置。
- MX记录（Mail Exchange Record）：指定接收该域名电子邮件的邮件服务器。当有人发送邮件到该域名时，MX记录会告诉邮件服务器该如何路由这些邮件。
- TXT记录（Text Record）：允许在域名中存储任意文本信息。常用于验证域名的所有权，设置SPF（Sender Policy Framework）规则来防止电子邮件欺诈等。
- SPF记录（Sender Policy Framework）：用于指定允许发送电子邮件的服务器列表，帮助防止伪造邮件发送者。
- SRV记录（Service Record）：指定提供特定服务的服务器的位置。常用于识别服务的位置和端口。
- CAA记录（Certification Authority Authorization）：用于限制可签发指定域名证书的认证机构。可以增强域名的安全性，减少证书被不信任机构签发的风险。 

![image-20230726214744585](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262147709.png)

这里以IPV4为例,

![image-20230726215612935](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262156994.png)记住解析的子域名的HOSTNAME;如www,后续

## 三.建站

### 1.添加域名

来到宝塔的网站,点击添加站点

![image-20230726215752818](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262157904.png)

然后提交后可以看见你的域名,点击你的域名

![image-20230726215943880](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262159924.png)

之后再次点击这里,也就是你的域名,就来到你的网站了(可以用wordpress搭建,本教程不细述)

![image-20230726220057776](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262200850.png)

然后显示如图就成功了

![image-20230726220331097](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262203204.png)

### 2.申请SSL

但是缺少证书,所以显示不安全,这里是因为两个协议不同的区别:

http和https的区别:

HTTP（HyperText Transfer Protocol）和HTTPS（HyperText Transfer Protocol Secure）是两种用于传输数据的协议，它们有以下主要区别：

- 安全性：
  •	HTTP：是一种不安全的协议，数据在传输过程中以明文形式发送，容易被中间人窃听和篡改，存在安全风险。
  •	HTTPS：是基于TLS/SSL协议的安全版本，通过数据加密和身份验证，确保数据在传输过程中是加密的和安全的，有效防止中间人攻击。
- 数据传输方式：
  •	HTTP：数据以明文形式传输，不进行加密处理。
  •	HTTPS：数据在传输过程中经过SSL/TLS加密，保障数据的机密性。
- 默认端口：
  •	HTTP：默认端口为80。
  •	HTTPS：默认端口为443。
- 证书要求：
  •	HTTP：不需要数字证书。
  •	HTTPS：服务器需要使用经过认证的数字证书，证书由受信任的第三方机构颁发，用于验证服务器身份和建立加密通道。
- URL前缀：
  •	HTTP：URL以”http://“开头。
  •	HTTPS：URL以”https://“开头。
- 网站标识：
  •	HTTP：在浏览器地址栏中没有额外的标识，通信为普通文本传输。
  •	HTTPS：在浏览器地址栏中会显示一个锁形状的图标或者绿色的安全标识，表示该网站是通过安全连接进行通信。



![image-20230726220420158](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262204273.png)

这时候可以来到刚才的页面,进入SSL

![image-20230726220545135](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262205201.png)



点击如图这里,选择你的域名进行申请证书

![image-20230726220852555](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262208618.png)



成功

![image-20230726221133342](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262211383.png)最后返回在你原来的网站http中加入s,用https登录你的页面

![image-20230726221224121](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307262212151.png)

然后你就可以发现不安全不见了



------

​                                                                                 end

------

