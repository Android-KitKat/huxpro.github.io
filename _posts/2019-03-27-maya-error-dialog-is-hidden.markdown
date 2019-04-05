---
layout:     post
title:      "关于退出Maya，报错\"确认退出\"或\"文件保存\"对话框被隐藏的解决办法"
subtitle:   "Maya"
date:       2019-03-27 22:00:00
author:     "Android"
header-img: "img/in-post/post-maya-error-dialog-is-hidden/header.png"
header-mask:  0.3
catalog:      true
multilingual: false
tags:
    - Maya
---
# 前言

差不多两年没更新博客了，一直想找个机会写篇文章，终于有个内容能写了。



我之前给同学发了个Maya安装包。

他在退出Maya，询问是否保存的时候，软件直接报错崩溃了。

但是我自己就没有这个问题。



不过最近帮同学在电脑上装好Maya，测试时也出现了这个问题。

# 症状

**软件:** Autodesk Maya 2014

**系统:** Windows 10 Version 1803

Maya大部分功能正常，但退出软件询问是否保存时，报错崩溃。

报错信息为` "确认退出"或"文件保存"对话框被隐藏。` 

![错误信息](/img/in-post/post-maya-error-dialog-is-hidden/错误信息.png)

# 分析

首先网上查了一下，回答是检查Maya版本是32位的还是64位的，要与系统相匹配，以及软件安装路径是否包含中文。

检查了一下，系统是64位的，Maya也是安装的64位。安装路径也不包含中文。

![系统版本](/img/in-post/post-maya-error-dialog-is-hidden/系统版本.png)

![Maya版本](/img/in-post/post-maya-error-dialog-is-hidden/Maya版本.png)

![安装路径](/img/in-post/post-maya-error-dialog-is-hidden/安装路径.png)



这就很奇怪了，于是想能不能看看Log之类的东西，也许可以看出什么原因。

在Maya的脚本编辑器里可以看到输出信息。

尝试复现错误，发现输出信息里有个包含中文的路径。

![脚本编辑器](/img/in-post/post-maya-error-dialog-is-hidden/脚本编辑器.png)

这个路径是系统的用户目录，Maya的配置文件就保存在`文档`的`maya`文件夹里。

那么很有可能就是因为这个，要解决问题就得把用户目录改成英文的。

# 修复

想要直接给用户目录改名是改不了的，所以只能用另寻它法。

首先**以管理员权限**打开命令提示符，运行命令启用内置管理员用户

```
NET USER Administrator /ACTIVE:YES
```

提示`命令成功完成`。

![命令提示符](/img/in-post/post-maya-error-dialog-is-hidden/命令提示符.png)



注销当前用户，登陆到`Administrator`，期间可能会初始化用户配置，稍等片刻即可。

打开系统盘下的`用户`文件夹，这时候就可以直接将自己的用户目录重命名成英文的了。

**如果提示已被占用可以重启电脑，然后直接登陆`Administrator`再试。**



然后按`Win+R`键，运行`regedit`，打开注册表编辑器。

![运行](/img/in-post/post-maya-error-dialog-is-hidden/运行.png)

依次展开到`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`。

`ProfileList`下的目录对应系统中的用户，目录中的`ProfileImagePath`值代表用户目录的路径。

![注册表编辑器](/img/in-post/post-maya-error-dialog-is-hidden/注册表编辑器.png)

找到对应自己用户的目录，右键`ProfileImagePath`点击修改，将值改成之前自己重命名后的目录。

![编辑字符串](/img/in-post/post-maya-error-dialog-is-hidden/编辑字符串.png)



这样用户目录就修改完成了。

注销`Administrator`，登陆自己的用户。

再次**以管理员权限**打开命令提示符，运行命令禁用内置管理员用户

```
NET USER Administrator /ACTIVE:NO
```



最后检查一下环境变量和其他软件，因为修改了用户目录，所以看看修改后的设置是否正确。

**现在退出Maya应该就不会报错崩溃了。**

# 补充

## 释放用户配置占用的空间

由于修改用户目录的过程中，我们登陆了`Administrator`用户，所以会产生相关的用户配置文件。

如果你以后不再需要登陆`Administrator`用户，可以删除用户配置文件来节省空间。



**首先如果你刚刚登陆过`Administrator`用户，记得先注销并重启一次电脑，避免文件占用。**

然后右键`此电脑`点击`属性`或打开`控制面板`的`系统`。

点击左侧的`高级系统设置`，切换到`高级`选项卡，再点击`用户配置文件`的`设置`。

![用户配置文件](/img/in-post/post-maya-error-dialog-is-hidden/用户配置文件.png)

找到`Administrator`的配置文件，如果看不全可以拖一下`名称`列旁边的那条杠，点击`删除`。

这样就删掉了用户配置文件。
