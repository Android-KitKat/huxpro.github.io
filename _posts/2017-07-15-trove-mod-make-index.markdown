---
layout:     post
title:      "宝藏世界模组开发指南——索引"
subtitle:   "宝藏世界模组开发指南"
date:       2017-07-15 20:16:46
author:     "Android"
header-img: "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      false
multilingual: false
tags:
    - 宝藏世界模组开发指南
---
## 目录
1 [解包]({% post_url 2017-07-15-trove-mod-make-unpack %})

2 编辑资源  
&nbsp;&nbsp;2.1 模型  
&nbsp;&nbsp;&nbsp;&nbsp;2.1.1 [使用MagicaVoxel]({% post_url 2017-07-19-trove-mod-make-magicavoxel %})  
&nbsp;&nbsp;&nbsp;&nbsp;2.1.2 [蓝图]({% post_url 2017-07-23-trove-mod-make-blueprint %})  
&nbsp;&nbsp;2.2 特效  
&nbsp;&nbsp;&nbsp;&nbsp;2.2.1 使用PopcornFX

3 加载  
&nbsp;&nbsp;3.1 [测试]({% post_url 2017-07-23-trove-mod-make-test %})  
&nbsp;&nbsp;3.2 [制作TMod文件]({% post_url 2017-08-13-trove-mod-make-tmod %})  
&nbsp;&nbsp;&nbsp;&nbsp;3.2.1 上传Mod到Steam创意工坊

4 补充  
&nbsp;&nbsp;4.1 [Q&A(问与答)](#qa问与答)

## 序言
![Trove Character](/img/in-post/post-trove-mod-make-index.png)

大家好，我是国际服League  Team俱乐部的Android。

我要开一个新坑——宝藏世界模组开发的中文教程。

目前已经完成了部分，后续内容也会慢慢补充完整(大概)。

<font color="Black" style="background-color:Black">不知道有生之年能不能填完这个坑呢。_(:3」∠)_</font>

## Q&A(问与答)
<h3>Q: 为什么我按照教程操作后，却没有出现相应文件。</h3>
A: 检查你的操作路径是否包含中文，如果有中文则改为英文。

<h3>Q: 为什么我文件名字和教程里的不一样？</h3>
A: 取消资源管理器的隐藏已知文件扩展名功能，具体操作方法可通过搜索引擎搜索"系统名字+显示扩展名"。

<h3>Q: 我在使用Trove的devtool时出现了未知错误。</h3>
A: devtool是不会返回执行结果的，你需要自行打开`%APPDATA%\Trove\DevTool.log`来查看错误原因。
