###### <font color = orange>MySQL教程</font><br/>——<br />MySQL安装部分<sup>卷1</sup><br/>`已最新版本|V1.0`<br/>**星空**<br/>*COPYRIGHT ⓒ 2024-2026. 王道版权所有*

[TOC]

# 安装步骤

> ~(Gn!)~
>
> <span style=color:yellow;background:red>**注意**</span>：建议大家都安装`Ubuntu22.04`的版本，在该版本下再安装<span style=color:yellow;background:red>**MySQL8.0**</span>版本的数据库。
>
> 1. 查看当前是否安装了MySQL程序
>
> ```shell
> $ dpkg -l |grep mysql
> ```
>
> 执行以上命令，如果执行后什么都没有，则进入到MySQL的安装步骤
>
> 2. 如果执行以上命令，显式如下，就证明MySQL已经安装完毕，直接使用MySQL即可。
>
> ![image-20240222161216287](assets/image-20240222161216287.png)
>
> 3. 执行以下命令安装MySQL
>
> ```shell
> # 安装MySQL的服务器端
> $ sudo apt install -y mysql-server-8.0
> # 安装MySQL客户端依赖包，后面通过C语言编程时使用
> $ sudo apt install libmysqlclient-dev
> ```
>
> 安装完成后，MySQL服务会自动启动
>
> 4. 使用如下命令检查MySQL的状态
>
> ```shell
> $ sudo systemctl status mysql
> ```
>
> ![image-20240222162913169](assets/image-20240222162913169.png)
>
> 至此，你已经成功的安装好了MySQL服务器。

# 安全配置

> ~(Gn!)~
>
> 默认情况下，安装MySQL是<span style=color:yellow;background:red>**没有设置密码**</span>的，需要我们自己设置密码。
>
> 1. 通过sudo权限登录MySQL
>
> ```shell
> # 由于安装时没有设置密码，输入以下命令，直接回车就可以登录成功
> $ sudo mysql
> ```
>
> ![image-20240222164006168](assets/image-20240222164006168.png)
>
> 2. 修改密码
>
> 通过以下SQL语句修改root用户的密码为"<span style=color:yellow;background:red>**1234**</span>"
>
> ```mysql
> mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '1234';
> mysql> update mysql.user set host='%' where user='root';
> mysql> flush privileges;
> ```
>
> ![image-20240222165447005](assets/image-20240222165447005.png)
>
> ![image-20240222165517317](assets/image-20240222165517317.png)
>
> 3. 重新登录
>
> 使用以下命令重新登录，不再需要加上sudo权限
>
> ```shell
> $ mysql -uroot -p
> ```
>
> 输入完成后，按回车，之后输入我们设置好的密码"<span style=color:yellow;background:red>**1234**</span>"，就可以正常登录了。
>
> ![image-20240222165621341](assets/image-20240222165621341.png)

# 安装Navicat

> ~(Gn!)~
>
> 1. 下载
>
> 这里已经给大家准备好了，只需要从网盘上下载下来即可。
>
> 链接：https://pan.baidu.com/s/1DXARuGFPa4_GSRACw6X4Aw?pwd=rk1t 
> 提取码：rk1t
>
> <img src="assets/image-20240223094443557.png" alt="image-20240223094443557" style="zoom:50%;" />
>
> 2. 安装
>
> 在Windows上双击<span style=color:yellow;background:red>**navicat161_premium_cs_x64.exe**</span>，开始安装navicat客户端
>
> 2.1 弹出以下窗口，点击“下一步”
>
> <img src="assets/image-20240223095021690.png" alt="image-20240223095021690" style="zoom:50%;" />
>
> 2.2 弹出以下窗口，勾选“我同意”后，点击“下一步”
>
> <img src="assets/image-20240223095158072.png" alt="image-20240223095158072" style="zoom:50%;" />
>
> 2.3 弹出以下窗口，在1位置可以修改程序存储的位置，之后点击“下一步”
>
> <img src="assets/image-20240223095310246.png" alt="image-20240223095310246" style="zoom:50%;" />
>
> 2.4 弹出以下窗口，点击“下一步”
>
> <img src="assets/image-20240223095529207.png" alt="image-20240223095529207" style="zoom:50%;" />
>
> 2.5 弹出以下窗口，点击“安装”
>
> <img src="assets/image-20240223095628133.png" alt="image-20240223095628133" style="zoom:50%;" />
>
> 2.6 安装的过程稍做等待，即可看到以下窗口，点击“完成”，就安装好了Navicat客户端了。
>
> <img src="assets/image-20240223095813408.png" alt="image-20240223095813408" style="zoom:50%;" />
>
> 3. 破解
>
> 3.1 破解时，先找到<span style=color:yellow;background:red>**NavicatCracker.exe**</span>程序，右键以“管理员身份运行”该程序，可看到以下窗口，点击“<span style=color:yellow;background:red>**Pahtch!**</span>”
>
> <img src="assets/image-20240223100156955.png" alt="image-20240223100156955" style="zoom:50%;" />
>
> 3.2 确认弹框选择“是”；之后再点击“<span style=color:yellow;background:red>**Generate!**</span>”,会生成一个序列号。再点击“<span style=color:yellow;background:red>**Copy**</span>”
>
> <img src="assets/image-20240223101332929.png" alt="image-20240223101332929" style="zoom:50%;" />
>
> 3.3 打开先前安装好的“**Navicat Premium**”软件，点击“<span style=color:yellow;background:red>**注册**</span>”,弹出以下窗口，将序列号粘贴过去，再点击“<span style=color:yellow;background:red>**激活**</span>”
>
> <img src="assets/image-20240223101637288.png" alt="image-20240223101637288" style="zoom:50%;" />
>
> 3.4 弹出一下窗口，点击“手动激活”
>
> <img src="assets/image-20240223101916891.png" alt="image-20240223101916891" style="zoom:50%;" />
>
> 3.5 弹出以下窗口
>
> <img src="assets/image-20240223101959751.png" alt="image-20240223101959751" style="zoom:50%;" />
>
> 3.6 拷贝其中的“<span style=color:yellow;background:red>**请求码**</span>”，粘贴到破解程序中的“<span style=color:yellow;background:red>**Request Code**</span>”中，之后点击“<span style=color:yellow;background:red>**Generate Activation Code**</span>”,生成激活码；最后将“<span style=color:yellow;background:red>**Activation Code**</span>”区域中生成的激活码复制粘贴到Navicat中，点击“<span style=color:yellow;background:red>**激活**</span>”，这样就完成了破解。
>
> ![image-20240223102432577](assets/image-20240223102432577.png)
>
> 3.7 当再次打开Navicat时， 就可以正常使用了。
>
> ![image-20240223103014691](assets/image-20240223103014691.png)

# 常见问题

> ~(Gn!)~
>
> 1. Navicat无法远程连接MySQL服务器
>
> <img src="assets/image-20240223103945565.png" alt="image-20240223103945565" style="zoom:50%;" />
>
> 2. 通过<span style=color:yellow;background:red>**Xshell**</span>连接Ubuntu服务器，在命令行下输入以下命令
>
> ```shell
> $ sudo netstat -ntlp|grep mysql
> ```
>
> 得到如下的结果
>
> ![image-20240223104246186](assets/image-20240223104246186.png)
>
> 其中服务器监听的IP地址为127.0.0.1,就说明无法通过远程连接来访问的。
>
> 3. 修改配置文件
>
> ```shell
> $ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
> ```
>
> 打开配置文件后，找到"bind-address"和"mysqlx-bind-address"配置项，在其前面加上 “#” 号
>
> <img src="assets/image-20240223104915083.png" alt="image-20240223104915083" style="zoom:50%;" />
>
> 4. 重启MySQL服务器
>
> ```shell
> # 重启
> $ sudo systemctl restart mysql
> # 再次查看MySQL服务器的监听状态
> $ sudo netstat -ntlp|grep mysql
> ```
>
> ![image-20240223104634084](assets/image-20240223104634084.png)
>
> 发现MySQL服务器的IP地址如上显示，就说明可以远程连接了。
>
> 5. 回到<span style=color:yellow;background:red>**Navicat Premium**</span> 软件，点击“<span style=color:yellow;background:red>**测试连接**</span>”，发现已经可以正常连接了。
>
> <img src="assets/image-20240223105417281.png" alt="image-20240223105417281" style="zoom:50%;" />

# The End