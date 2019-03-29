---
layout:     post
title:      "宝藏世界模组开发指南——测试"
subtitle:   "宝藏世界模组开发指南"
date:       2017-07-23 16:49:20
author:     "Android"
header-img: "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      false
multilingual: false
tags:
    - 宝藏世界模组开发指南
---
编辑好文件后，需要载入到游戏中进行测试。

## 通过override文件夹载入
在[解包]({% post_url 2017-07-15-trove-mod-make-unpack %})的目标路径创建一个`override`文件夹，将想要加载到游戏的文件放入。  
游戏会自动将`override`文件夹内的文件载入到`override`文件夹所在的文件夹。
  
例如，[蓝图]文件存放在游戏目录的`blueprints`文件夹下。  
则在`blueprints`文件夹内创建一个`override`文件夹，将[蓝图]文件放入其中。  
`\blueprints\override`的文件会自动载入到`\blueprints`。

[蓝图]: {% post_url 2017-07-23-trove-mod-make-blueprint %}

重启游戏即可加载放入的文件。
  
如果你是覆盖已有的资源文件，那么被替换的内容就会变成你制作的内容。

如果你是新增的资源文件，你需要通过以下方法预览。

## 预览蓝图
*以下的蓝图名字不需要带扩展名，即不需要带 `.blueprint` 。*

### 武器
在聊天框输入`/weaponpreview [蓝图名字]`或`/wp [蓝图名字]`。

### 面具
在聊天框输入`/facepreview [蓝图名字]`。

### 帽子
在聊天框输入`/hatpreview [蓝图名字]`。

### 发型
在聊天框输入`/hairpreview [蓝图名字]`。

### 装饰
先在聊天框输入`/metaforge`，进入Metaforge。  
然后输入`/decopreview [蓝图名字]`。
