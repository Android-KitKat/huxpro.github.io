---
layout:     post
title:      "救命！3ds Max一撤销就崩溃。"
subtitle:   "Help! 3ds Max crashes on undo."
date:       2019-04-12 21:00:00
author:     "Android"
header-img: "img/in-post/post-3dsmax-virus-crashes-on-undo/header.png"
header-mask:  0.3
catalog:      true
multilingual: false
tags:
    - 3ds Max
---
# 描述

今天上课做模型，发现一旦撤销，3ds Max就会直接崩溃。

这…… 做模型哪有不撤销的。

难道是3ds Max这个版本有问题，可之前还能用。

于是查了一下，3ds Max居然还能有病毒的。

平时不运行奇怪软件的我竟然也中招了。

~~老师我真的不是在摸鱼，软件中了病毒做不了呀。~~

这个病毒会存在于场景文件。当你打开感染病毒的场景时，会在脚本加载目录创建病毒脚本，并设置 系统 + 隐藏 文件属性。

病毒将会导致撤回时崩溃，自动删除摄像机、灯光、材质，以及感染每一个打开的场景。

感染之后还会强制保存，就算关闭场景时选择不保存也依然会保存，以便将病毒感染。

这简直就是"3ds Max大师一命难度"。

> [打开场景]
>
> "这样子做行不行呢？"
>
> "看来不行。"
>
> (既然撤销会崩溃，那就直接关闭场景不保存吧，真是机智如我。)
>
> ([文件已保存])
>
> [再次打开场景]
>
> "什么！我不是没保存吗，我的模型~"

而且场景会多两个空白的对象，但是删不掉。

![场景资源管理器](/img/in-post/post-3dsmax-virus-crashes-on-undo/场景资源管理器.png)

# 解决方法

我中的病毒是vrdemat系列。

Autodesk官方接到反馈后，制作了杀毒脚本。

官方论坛：[关于最近出现的病毒，临时解决方案。][官方论坛]

下载[ALC_CRP_fixup.zip](/assets/in-post/post-3dsmax-virus-crashes-on-undo/ALC_CRP_fixup.zip)，解压`ALC_fixup.ms`和`CRP_fixup.ms`到`<3ds Max安装目录>\scripts\Startup`文件夹下。

重新打开3ds Max，会提示发现病毒脚本，选择`是`清除文件。

![发现病毒脚本](/img/in-post/post-3dsmax-virus-crashes-on-undo/发现病毒脚本.png)

这样，3ds Max的病毒就被清除了。

但如果感染病毒前，曾经打开过场景文件，这些文件也会被感染病毒。

在安装杀毒脚本的情况下，重新打开这些文件。脚本会提示发现病毒节点，选择`是`清除节点。

![发现病毒节点](/img/in-post/post-3dsmax-virus-crashes-on-undo/发现病毒节点.png)

**不过注意，这只是暂时从内存中清除了病毒。原文件依然被感染了病毒，需要再次`保存`或者`另存为`。**

也小心不要把感染病毒的场景文件发给别人，毕竟这个病毒脚本实在太丧心病狂了。

[官方论坛]: https://forums.autodesk.com/t5/maya-3ds-max-zong-he-tao-lun-qu/guan-yu-zui-jin-chu-xian-de-bing-du-lin-shi-jie-jue-fang-an/td-p/7297624 "关于最近出现的病毒，临时解决方案。"