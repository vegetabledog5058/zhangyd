# **GitHub + PicGo + Typora 搭建个人图床**



## #1.注册一个Github账号**

------



首先你需要一个github账号，如果没有的话，先注册。

（需科学上网注册，过程省略）



------



## #2. 配置Github



------



### 2.1 创建一个新仓库，用于存放图片。

![image-20230723180740746](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231839314.png)



![image-20230723181014674](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231839412.png)

------

### 2.2 生成一个token，用于picGo访问github



### 方法：

1. 首先登录到您的GitHub账户。
2. 在页面右上角，点击您的个人头像或账户图标。
3. 从下拉菜单中选择 "Settings"（设置）。
4. 在左侧导航栏中，点击 "Developer settings"（开发者设置）。
5. 在下拉菜单中，选择 "Personal access tokens"（个人访问令牌）。
6. 输入您的GitHub账户密码，以进行身份验证。
7. 点击 "Generate new token"（生成新令牌）按钮。
8. 在 "Token description"（令牌描述）字段中，为您的令牌取一个描述性的名称，以便稍后识别此令牌的用途。
9. 根据您的需求，选择令牌的 "Expiration"（过期时间）和所需的权限范围。
10. 点击 "Generate token"（生成令牌）按钮。
11. 生成后，您将看到一个长字符串，这就是您的GitHub Token。请务必复制此Token并妥善保存，因为一旦页面刷新，您将无法再查看此Token的值。

![image-20230723184031599](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231840694.png)

![image-20230723180130596](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231801681.png)

![image-20230723180547964](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231805090.png)

![image-20230723181151632](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231811697.png)

------



## #3. 下载picGo，并进行配置



------

网址：[PicGo is Here | PicGo](https://picgo.github.io/PicGo-Doc/zh/guide/#下载安装)

选择一个下载源下载

![image-20230723181420797](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231814945.png)

这里用山东大学镜像Windows为例；（如果不能正常打开用管理员或者兼容模式打开

![image-20230723181820951](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231818054.png)

------



**安装完成后进入这里设置（很重要！！！）**

用户名点击GitHub右上角头像显示的名字就是用户名



------

![image-20230723183104285](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231831373.png)

设置完可以先在这里测试是否能够上传成功，如果提示成功就可以进行下一步，不成功大概率是上图的设置没有填写正确。

![image-20230723183513187](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231836596.png)



成功提示



![image-20230723184320700](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231843778.png)

------

成功后需要设置几个地方

------

![image-20230723184608237](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231846310.png)

![image-20230723184633733](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231846807.png)

![image-20230723184650577](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231846633.png)



## 

------

## #4.图床接入

------

打开`Typora`，找到偏好设置，点击图像，按照①②③④⑤配置。其中**④**处注意下，路径为你的**Typora.exe**所在位置。

![image-20230723184846982](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231848063.png)



之后点击⑥处，出现如下结果表示配置成功！



![image-20230723184926258](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231849311.png)



------

之后就可以自由使用Typoral了，在本地插入或复制到Typoral的图片会自动变成网页链接，并自动上次到仓库



------

![image-20230723185159638](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231851766.png)

------



## #5.经验分享



------



### 5.1 仓库地址搞错

之前讲过仓库地址为 haichuangdianzi/xp01，一开始在用的时候图方便直接复制下图中的名字！复制出来的名字斜杠两侧是有空格的！

![image-20230723185623357](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231856408.png)



5.2 未初始化readme文件
这个具体过程在2.4步骤中描述过了，其实很多教程也描述过了要初始化，但是在现在的页面没有这个选项就给忽略了，但是后来我又是怎么知道是把这个重要的的步骤忽略了呢？换句话说，如果大家在配置的时候出现了问题应该怎么样去排查错误呢？这边给大家介绍一个方法，查看日志！！根据如下两张图打开日志。日志会清楚的记录出错的原因。
![image-20230723185656413](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231856489.png)

![image-20230723185712360](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231857411.png)



### 5.3 私人令牌

再次强调下私人令牌只生成一次！！有的小伙伴觉得已经在PigGo中配置了应该不需要了。不一定！有可能你下次打开PigGo时信息没了！所以请妥善保存



### 5.4 以前笔记中的图片怎么处理

在下图中能看到我以前的图片都存放在c盘某个文件夹，现在想都传到gitee中怎么办，重新截图？NO！直接在图片中点击右键，选择上传图片！

![image-20230723185945644](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231859717.png)



![image-20230723190024593](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/202307231900655.png)



------

至此结束  

------

