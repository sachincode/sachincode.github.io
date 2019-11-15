---
layout: post
title: Android开发环境搭建 -（2）
description: 使用Eclipse来做android开发的另一种方式是使用独立的SDK，然后给Eclipse添加ADT插件。所以这次使用下载installer_r24.1.2-windows.exe的方式来搭建环境。
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
在[android开发官网][2]下载android SDK，这里选择推荐的Windows平台的installer_r24.1.2-windows.exe，官网需要翻墙。下载后，直接运行安装程序安装，在安装过程中更改了安装目录，我这里为E:\androiddevelop；安装完成后的目录结构为下图所示：

![android dir](/images/android-env/androiddir.jpg)


然后设置环境变量，在系统变量中新建变量，变量名为ANDROID_SDK_HOME，变量值为刚才解压缩的文件夹中的sdk位置，即是E:\androiddevelop

然后在系统变量path变量中添加值 %ANDROID_SDK_HOME%\tools;%ANDROID_SDK_HOME%\platform-tools

这里说明一下ANDROID_SDK_HOME系统变量的作用，在创建管理AVD的时候，开发者创建的虚拟设备保存在%ANDROID_SDK_HOME%\.android路径下，如果不设置则默认保存在C盘的系统用户中，可能会占用较大的空间。


到安装目录运行SDK Manager，一开始什么平台和工具也没有，需要下载下来。

##eclipse##
访问www.eclipse.org下载标准版本的eclipse。

这里下载了eclipse-SDK-3.7.2-win32.zip

##ADT插件##
为eclipse安装ADT插件，有两种方式，在线安装和下载后本地安装。

###在线安装###

打开eclipse,点击Help->Install New Software->输入 https://dl-ssl.google.com/android/eclipse/  回车,安装前两项即可，也可全部安装。

按照步骤，应该会显示这样的界面：

![adt right](/images/android-env/adtright.jpg)

但是我们在天朝，所以结果就是这样的界面：

![adt error](/images/android-env/adterror.jpg)

看了吧，解析不出来，所以怎么办呢，翻墙或者下载ADT本地安装吧。

###本地安装###

一个ADT的下载链接，在[百度云上][4]，这个版本是ADT-23.0.0.zip。

下载到本地之后，再回到刚才的安装插件界面，点击旁边的ADD按钮，找到刚才下载的ADT包的位置，如图所示：

![adt error](/images/android-env/adtlocation.jpg)

确定之后，好了，可以解析到插件了，您看：

![adt right](/images/android-env/adtright2.jpg)

这时再选择安装插件安装就好了。

注意安装的时候把下方的“Contact all update sites during install to find required software”选择框取消掉，否则安装时候还会连接网站，导致卡住。

安装完成之后在eclipse界面上将会出现两个可爱的机器人图标。

![preference](/images/android-env/eclipse.png)

然后,点击Window->preferences->选择sdk的安装路径。

![preference](/images/android-env/prefer.jpg)

至此，android环境搭建完成。

## 可能出现的问题 ##
由于我们是中国特色主义和谐社会，所以机器人这么暴力的东西还是抵御在长城的外围比较好，但是我们这群人可就遭殃了，还让不让人好好的玩机器人了，这就是出现的问题，看下图。

![Eclipse](/images/android-env/problem.jpg)

我要下载android开发的工具，但是竟然不能访问http://dl-ssl.google.com网站，导致无法下载。谢谢和谐社会。

解决方法请参考上一篇文章。



[1]:    {{ page.url}}  ({{ page.title }})
[2]: http://developer.android.com/
[3]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[4]: http://pan.baidu.com/s/1nfXnC