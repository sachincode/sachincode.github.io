---
layout: post
title: 搭建魔兽世界1.12.3版私服
description: 对于魔兽老玩家来说，60年代的魔兽是一个永远的回忆，那里的每个角落都发生着一段故事，这里我将教您搭建一个60年代的魔兽私服，仅供个人娱乐，拒绝用于商业目的。
category: blog
---

对于魔兽老玩家来说，60年代的魔兽是一个永远的回忆，那里的每个角落都发生着一段故事，这里我将教您搭建一个60年代的魔兽私服，去走走你熟悉的地方。

**仅供个人娱乐，拒绝用于商业目的。**

## 单机版私服 ##

既然是搭建魔兽私服，那么你就得有服务端，那我去哪搞服务端呢？客官您别着急，我给你地址，[魔兽世界地球时代单机版][2],这里可以下载，访问密码是588c，当然这个服务器版本也是在网络上别人共享的，真是楼主好人一生平安啊。

有了服务端，那就好说了。下载下来解压缩到硬盘中，我解压到了C盘中，但是我不建议你解压到C盘，选择其他盘符吧。可以看到里面的文件列表：

![files](/images/wowserver/files.png)

其实可以看到里面已经有架设的教程了，我这里详细说明一下。

其中提到了，必须的环境是VC2012或者VC2010（推荐VC2010）和NET4.0，我的电脑是WIN7系统，因为是程序员，所以可能这些环境有了，所以这里就没装，没有问题，如果您启动报错了，那么就去安装了。NET 4.0应该是指NET 4.0 framework。

1、首先打开 游戏启动器.exe 文件。

2、然后设置好路径：

MySQL path:     C:\1.12.3\MySQL\bin
Apache path:    C:\1.12.3\Apache\bin

界面是这样子：

![restarter](/images/wowserver/restarter.png)

说明一下，MySQL是一个数据库，Apache是用来搭设WEB服务的，也就是稍后可以访问的注册帐号的网页，这个网页是PHP写的，在目录中也有PHP的相关文件，以及 www 目录下就是网页文件。

3、打开MySQL--(start the mysql server选项就是，停止stop，这是游戏数据服务）
  打开Apache--(start the apache server就是，这是游戏网站数据服务）

4、启动游戏服务端1.realmd.exe和2.mangosd.exe，(在文件夹里面启动，并非启动器里面）

注意，在启动的时候把exe文件前面的1.和2.去掉，否则启动2.mangosd.exe的时候会报错，是这个

![mangoaderror](/images/wowserver/mangoaderror.png)

其实报错之后确定，然后可以继续启动服务，而且也可以登录玩游戏，不知道这个错误有没有其他后遗症。所以还是把文件名改正确吧。启动之后类似这样子。

![realmd](/images/wowserver/realmd.png)

![mangoad](/images/wowserver/mangoad.png)

5、注册账号:
打开：网页浏览器输入127.0.0.1 注册账号

这里注册的帐号是普通玩家，其实这个服里面内置了几个帐号了，看来是别人玩的。这是数据库中的数据：

![account](/images/wowserver/account.png)

其中username列就是账户名，sha_pass_hash列是加密后的密码，明文是和账户名一样的，当然使用明文密码登录了，gmlevel列是账户的等级，3代表这是GM，2代表是高级管理员，1代表是管理员，0就是普通玩家了。

如果你创建了一个帐号，想把他变成GM等级怎么办，可以在mangosd.exe的命令行窗口中回车输入

    .account set gmlevel xxx 3

xxx为账号名字 3为权限等级 也就是GM完全权限

服务器文件夹中有几个实用的txt文件，可以自己查看。


6、进入游戏
下载[魔兽客户端][3],访问密码是7f24,下载[登录器][4],访问密码是a003。将客户端解压缩到硬盘，然后将登录其拷贝到客户端文件夹内，单击 单机登陆器.bat 进入游戏!

这个版本的服务器提供了一个召唤玩家机器人命令，前提是这个机器人是一个已经创建的角色。

    .bot add 你的机器人名字

目前为止，你可以登录游戏了，但是还仅限于在自己的电脑上登录，而局域网内的其他电脑就不行。后面解决的就是这个问题。

## 局域网私服 ##

单机版不够爽怎么办，想和局域网内的小伙伴一起玩怎么办，这里来解决。

首先，你需要工具Navicat for MySQL数据库管理软件，当然如果你程序员，当然可以用命令行搞定。

到网上去下载Navicat for MySQL软件，然后安装。[这里][5]有Navicat for MySQL的简单教程的，不过需要注册登录，你也可以百度其他教程。

启动Navicat for MySQL之后，我们单击左侧的 《连接》按钮,然后输入相关内容，连接数据库。输入什么别着急，我们往下看。

到你的服务端文件夹中，找到这样一个文件： realmd.conf

用记事本打开他，然后扫一下，从后往前翻，在110行，你会发现一个这样一句话。

    LoginDatabaseInfo = "127.0.0.1;3306;root;ascent;realmd"

这里的意思就是说登录客户端的时候的连接数据库的信息。127.0.0.1是一个保留IP地址，专门用来指本机的意思，就是自己这台电脑。3306是MySQL数据库的默认端口号，root是连接数据库的用户名，ascent是root的用户密码，realmd就是连接的数据库名称。如果你用Java JDBC写过程序，那就肯定想起了这么一句配置：

    jdbc:mysql://localhost:3306/realmd", "root", "ascent"

这里的localhost也是本机的意思，你也可以使用127.0.0.1代替。哈哈，说多了，这里将搭建私服，不要说JDBC了好嘛。

输入信息：

![navicat](/images/wowserver/navicat.jpg)

其中连接名是随便起的，建议用英文。填好之后下方的 连接测试 一下，应该可以联通的，然后确定就好了。确定之后可以看到这个界面，

![local](/images/wowserver/local.png)

然后右键点击选择打开连接就好了，是这个样子

![local2](/images/wowserver/local2.png)

可以看到这里面有很多数据库，其中就包括刚才用到的realmd数据库，另外重要的数据库是characters和mangos，scriptdev2这个数据库不知道是干什么的。剩下的三个information_schema、mysql、performance_schema数据库是MySQL自带的，不要去处理。这几个数据库都可以右键点击选择打开，我们打开realmd数据库。可以看到下面：

![realmdbase](/images/wowserver/realmdbase.png)

其中点开 表 这里，里面就是存储的数据表了，其中最重要的有两个表account和realmlist，account表就如可以看到的存储的是每一个账户的信息，你也可以在这里修改账户的等级。现在我们修改的是realmlist这个表。打开表可以看到信息，你看到了熟悉的一串数字了吧：127.0.0.1。

![realmlist](/images/wowserver/realmlist.png)

现在我们修改的就是这串数字，将它改为你的电脑的IP地址，什么？连你电脑IP也不知道，不要开玩笑了。cmd命令行里输入ipconfig，你可以看到的。例如我的是172.17.64.37，修改之后要记得保存啊，怎么保存呢，注意这个软件下面有 + - √ × 等这几个符号按钮，点击那个 √ 就可以保存了。

![realmlist2](/images/wowserver/realmlist2.png)

唉，我感觉我完全是教怎么使用这个数据库管理软件啊！

第一个需要修改的地方终于好了，修改之后将服务器**重启**一下吧。

接下来要修改的就是客户端了，有两个文件需要改，一个是realmlist.wtf，另一个是 单机登陆器.bat，这两个文件可以使用记事本打开修改，终于可以不用那么麻烦了。

先看没修改的realmlist.wtf内容

    SET realmlist 127.0.0.1 

然后把127.0.0.1 改为你刚才的服务器那台电脑的IP，就是刚才改的那个。我的改好后是：

    SET realmlist 172.17.64.37 

然后是没修改的 单机登陆器.bat

    @echo off
    echo SET realmlist 127.0.0.1 > realmlist.wtf
    rd /s /q WDB
    start wow.exe
    exit

也是改一下IP地址，我的改好之后是：

    @echo off
    echo SET realmlist 172.17.64.37 > realmlist.wtf
    rd /s /q WDB
    start wow.exe
    exit

好了，终于大功告成了，我相信你现在可以在局域网内登录了。

再多介绍一个表吧，characters数据库中的characters表，看名字就知道是干什么的了，果然没错，存储的就是各个玩家角色的信息。

![characters](/images/wowserver/characters.png)
  

## 公网私服 ##

到现在为止，我可以在局域网内登录游戏了，那如果我想在外网也可以登录怎么办呢，就当于是那些私服了。其实只要知道了怎么可以局域网内登录就好了，外网访问也是改IP的问题，我这里就不讲了，该干活去了。

祝各位小伙伴玩的愉快。
  

[1]:    {{ page.url}}  ({{ page.title }})
[2]: http://yunpan.cn/cVz4tw4RmCQ45
[3]: http://yunpan.cn/cVzN2My75sYcB
[4]: http://yunpan.cn/cVzN9HhA6bLwI
[5]: http://imooc.com/video/3193