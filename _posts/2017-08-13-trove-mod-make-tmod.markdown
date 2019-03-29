---
layout:     post
title:      "宝藏世界模组开发指南——制作TMod文件"
subtitle:   "宝藏世界模组开发指南"
date:       2017-08-13 07:21:14
author:     "Android"
header-img: "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      false
multilingual: false
tags:
    - 宝藏世界模组开发指南
---
TMod文件是宝藏世界的模组文件格式，它可以将你编辑的资源打包为单个文件。  
还可以增加作者, 描述, 封面, 标签等信息。

相比将多个资源文件放入对应的`override`文件夹来载入，TMod文件只需要放入游戏目录的`mods`文件夹即可。

所以在发布你的Mod之前，一定要打包为TMod文件。  
![模组列表](/img/in-post/post-trove-mod-make-tmod/模组列表.png)

## 准备
### 资源文件
在打包之前要确保你修改的资源文件可以通过[override文件夹]({% post_url 2017-07-23-trove-mod-make-test %}#通过override文件夹载入)载入。

### 封面
其次，要为你的模组添加一个封面，格式可以是png, jpg或是blueprint。  
封面的大小是400 x 230，放入游戏目录的`\ui\override`文件夹。

*虽然资源文件放在`override`文件夹下，但是实际上是载入到了`override`文件夹所在的目录。*  
*例如有一个文件是 `ui\override\HelloWorld.png` ，而它实际上被载入到了 `ui\HelloWorld.png` 。*  
*所以下列操作需要填写目录时，请忽略override文件夹进行填写。*

## 打包
接下来，你可以通过以下方法之一来生成你的TMod文件。

*进行以下操作后，可到游戏目录的 `mods` 文件夹查看生成的模组文件。*

### 在游戏中
这种方法不能精确控制打包哪些资源文件，它会打包所有通过override文件夹载入的资源文件。

在聊天窗口输入以下指令。  
`/buildmod title="模组名称" author="作者名称" notes="模组注释" preview="预览图片路径" tags="标签1,标签2"`

指令参数中，除了`title`参数必须要指定，其他参数均是可选的。

例如：  
`/buildmod title="你好,世界!" author="Android" notes="我的第一个模组。" preview="ui/HelloWorld.png"`

![BuildMod指令](/img/in-post/post-trove-mod-make-tmod/BuildMod指令.png)  
执行后，聊天区域会显示被打包的资源文件。  
之后会提示指定名称的模组已创建完成。

### 在命令行
这种方法可以精确的指定打包哪些资源文件。  
但是值得吐槽的是，如果你执行的命令内包含中文则会出现乱码。

在游戏目录空白处Shift+右键，在此处打开命令窗口。  
输入命令行:  
`Trove.exe -tool buildmod -title "模组名称" -author "作者名称" -notes "模组注释" -preview "预览图片路径" -tags "标签a,标签b,标签c,标签d" - <文件1> <文件2>`

指令参数中必须要包含`title`,`author`以及要包含的文件。  
命令最后的文件那一部分，你需要填写模组要包含的所有资源文件，包括封面。

例如:  
`Trove.exe -tool buildmod -title "HelloWorld!" -author "Android" -notes "My first mod." -preview "ui/HelloWorld.png" - ui/HelloWorld.png blueprints/equipment_weapon_1h_sword_001.blueprint`

### 在命令行引用YAML文件
这种方法可以精确的指定打包哪些资源文件，而且看起来更加易读。  
个人强烈建议使用这种方法。

首先，我们在任意目录创建一个文本文件，将其扩展名命名为.yaml。  
*字符编码必须为UTF-8。*

然后，按照以下格式编辑YAML文件。  
{% highlight yaml %}
---
title: 模组名称
author: 作者名称
notes: 模组注释
previewPath: 预览图片路径
files:
- 文件1
- 文件2
tags:
- 标签1
- 标签2
...
{% endhighlight %}

YAML文件中必须要指定`title`,`author`以及`files`。  
`files`中你需要填写模组要包含的所有资源文件，包括封面。

例如:  
{% highlight yaml %}
---
title: 你好,世界!
author: Android
notes: 我的第一个模组。
previewPath: ui/HelloWorld.png
files:
- ui/HelloWorld.png
- blueprints/equipment_weapon_1h_sword_001.blueprint
...
{% endhighlight %}

然后，在游戏目录空白处Shift+右键，在此处打开命令窗口。  
输入命令行:  
`Trove.exe -tool buildmod -meta "YAML文件路径"`

例如:  
`Trove.exe -tool buildmod -meta "D:\TroveMod\HelloWorld\HelloWorld.yaml"`

## 验证
首先打开`%APPDATA%\Trove\Trove.cfg`文件，找到`[System]`(没有就添加一个)。  
在这一节下添加新的一行`UseOverrides=false`，以禁用通过override载入资源。  
之后如果需要恢复，可以删除这一行或者将`false`改为`true`。

接下来就可以将TMod文件放到游戏目录的`mods`文件夹，重启游戏验证你的TMod文件有无问题。  
如果没有问题，你就可以将模组分享给其他人了。
