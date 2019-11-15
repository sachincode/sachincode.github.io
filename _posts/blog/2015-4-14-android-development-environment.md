---
layout: post
title: Android开发环境搭建
description: Android开发环境搭建：使用adt-bundle-windows。现在android开发官网主推Android Studio来开发android应用程序，但是之前广泛使用的是Eclipse，所以还是使用Eclipse来搭建环境吧。
category: blog
---

现在[android开发官网][2]主推Android Studio来开发android应用程序，但是之前广泛使用的是Eclipse，所以还是使用Eclipse来搭建环境吧。

## JAVA环境 ##
开发android应用需要Java开发环境，所以需要[下载JDK][3]安装，这里选择了使用Java 7，寻找jdk-7u71-windows-x64.exe（64位Windows系统）或jdk-7u71-windows-i586.exe（32位Windows系统）安装，然后设置环境变量。

计算机-->属性-->高级系统设置-->环境变量



1. 新建系统变量：变量名为 JAVA_HOME，变量值为Java的安装目录，我这里为 C:\Program Files\Java\jdk1.7.0_71
2. 在系统变量中寻找PATH变量并编辑，在其值后添加%JAVA_HOME%\bin;注意各个值之间使用英文下的;隔开
3. 新建系统变量：变量名为 CLASSPATH，变量值为 %JAVA_HOME%\lib\tools.jar;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib

配置完毕之后，通过cmd运行命令：java -version，出现以下画面，则说明安装成功。

![Java version](/images/android-env/javaenv.jpg)


## android环境 ##
现在android官网上主推Android Studio开发IDE，所以之前的开发软件下载连接不太好找了，这里指的是adt-bundle-windows压缩包系列，里面包含了android的SDK和eclipse，解压即可使用，比较方便，下载的话可以在迅雷直接新建下载链接http://dl.google.com/android/adt/adt-bundle-windows-x86-20140702.zip或者http://dl.google.com/android/adt/adt-bundle-windows-x86_64-20140702.zip即可，分别为32位和64位操作系统。

这里下载了adt-bundle-windows-x86-20140702，直接解压，这里我解压到了E盘。解压后文件夹目录结构为
E:\adt-bundle-windows-x86-20140702，文件架内包括两个子文件夹和一个exe文件，即eclipse、sdk、SDK Manager.exe。

然后设置环境变量，在系统变量中新建变量，变量名为ANDROID_SDK_HOME，变量值为刚才解压缩的文件夹中的sdk位置，即是E:\adt-bundle-windows-x86-20140702\sdk。

然后在系统变量path变量中添加值 %ANDROID_SDK_HOME%\tools;%ANDROID_SDK_HOME%\platform-tools

这里说明一下ANDROID_SDK_HOME系统变量的作用，在创建管理AVD的时候，开发者创建的虚拟设备保存在%ANDROID_SDK_HOME%\.android路径下，如果不设置则默认保存在C盘的系统用户中，可能会占用较大的空间。


## android SDK ##
打开adt-bundle-windows-x86-20140702文件夹中的eclipse并启动，设置工作空间。eclipse界面左上角已经包括了android的工具按钮，如下图所示。

![Eclipse](/images/android-env/eclipse.png)

点击左侧的小机器人按钮，启动Android SDK Manager，下载相应的SDK或工具。打开右侧的小机器人按钮Android Virtual Device Manager创建模拟器。

## 可能出现的问题 ##
由于我们是中国特色主义和谐社会，所以机器人这么暴力的东西还是抵御在长城的外围比较好，但是我们这群人可就遭殃了，还让不让人好好的玩机器人了，这就是出现的问题，看下图。

![Eclipse](/images/android-env/problem.jpg)

我要下载android开发的工具，但是竟然不能访问http://dl-ssl.google.com网站，导致无法下载。谢谢和谐社会。

### 解决方法一 ###
1. 访问http://tool.chinaz.com/  站长工具网站。
2. 选择超级ping。

	![tools](/images/android-env/tools.png)

3. 输入dl-ssl.google.com，只勾选“海外”。

	![ping](/images/android-env/ping.png)

4. 在cmd界面ping查询出来的IP地址，ping出一个地址即可。
5. 将74.125.129.93 dl-ssl.google.com写入到C:\Windows\System32\drivers\etc的hosts文件。
6. 重新打开Android SDK Manager开始下载。

### 解决方法二 ###
如果方法一不行，则可以试试这个。

1. 启动 Android SDK Manager ，打开主界面，依次选择「Tools」、「Options...」，弹出『Android SDK Manager - Settings』窗口；
2. 在『Android SDK Manager - Settings』窗口中，在「HTTP Proxy Server」和「HTTP Proxy Port」输入框内填入mirrors.neusoft.edu.cn和80，并且选中「Force https://... sources to be fetched using http://...」复选框。设置完成后单击「Close」按钮关闭『Android SDK Manager - Settings』窗口返回到主界面；
3. 依次选择「Packages」、「Reload」。

### 解决方法三 ###
如果SDK还是不能更新的话，那就翻墙吧，下个翻墙软件或者使用VPN，这就不在本文的范畴之内了。

### 解决方法四 ###
其实还有一种方法，就是利用其他人已经下载好的SDK，下载后直接放到自己的SDK目录中。
比如说我的SDK Manager已经下载了从android 2.1到 Android L Priview的内容。adt-bundle-windows-x86-20140702文件夹下的sdk目录已经14.2G了，并且用了很长时间上传到了我的360云盘中，可以将它下载下来，覆盖掉你的电脑上那个sdk目录。上传结束之后竟然不能共享，原因是超过了2000个文件文件夹。所以只好把sdk目录打压缩包再继续上传，赫然发现压缩速度相对于之前的不压缩直接上传速度快多了，压缩之后只有3.5G了，所以可以将[SDK压缩包][4]下载下来（（  访问密码 f2e0）），解压缩覆盖掉你的那个sdk目录吧。

至少可以这样试一下嘛，不过我没有这样做过，之前都是直接manager下载的。

注意的是sdk文件夹中的.android文件夹就是之前提到的，创建的AVD保存的文件夹，这里面还有我之前创建的AVD，我并没有删除掉。

![manager](/images/android-env/manager.jpg)



[1]:    {{ page.url}}  ({{ page.title }})
[2]: http://developer.android.com/
[3]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[4]: http://yunpan.cn/cVkRffPK6kmbz