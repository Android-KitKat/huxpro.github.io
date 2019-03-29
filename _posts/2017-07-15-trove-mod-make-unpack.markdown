---
layout:     post
title:      "宝藏世界模组开发指南——解包"
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
宝藏世界的游戏资源都被打包到后缀名为TFA的文件中。

我们不能直接对其进行编辑，需要使用游戏给我们的工具进行解包后才能编辑。
![TFA文件](/img/in-post/post-trove-mod-make-unpack/TFA文件.png)

首先，我们打开游戏目录。

中国版：`[游戏安装目录]\360游戏\trove\gameclient`

Steam版：`[Steam安装目录]\Steam\steamapps\common\Trove\Games\Trove\Live`
![游戏目录](/img/in-post/post-trove-mod-make-unpack/游戏目录.png)

按住Shift键并右键空白处，点击"在此处打开命令窗口(W)"。
![在此处打开命令窗口](/img/in-post/post-trove-mod-make-unpack/在此处打开命令窗口.png)

出现了CMD命令行窗口。
![命令行窗口](/img/in-post/post-trove-mod-make-unpack/命令行窗口.png)

输入命令行按回车进行解包。

## 格式：

    Trove.exe -tool extractarchive [目标路径] [输出路径]

## 例如：

### 解包蓝图

*大部分模组的制作只需要解包这个就可以了*

    Trove.exe -tool extractarchive blueprints extracted\blueprints

### 解包PopcornFX特效

    Trove.exe -tool extractarchive particles\vfx extracted\particles\vfx
    Trove.exe -tool extractarchive particles\vfx\particles extracted\particles\vfx\particles
    Trove.exe -tool extractarchive particles\vfx\textures extracted\particles\vfx\textures
    Trove.exe -tool extractarchive particles\vfx\textures\player extracted\particles\vfx\textures\player
    Trove.exe -tool extractarchive particles\vfx\meshes extracted\particles\vfx\meshes
    Trove.exe -tool extractarchive particles\vfx\atlasdefinitions extracted\particles\vfx\atlasdefinitions
    Trove.exe -tool extractarchive particles\vfx\Animations extracted\particles\vfx\Animations
    Trove.exe -tool extractarchive particles\vfx\Cache extracted\particles\vfx\Cache\Meshes
    Trove.exe -tool extractarchive particles\vfx\Config extracted\particles\vfx\Config
    Trove.exe -tool extractarchive particles\vfx\Editor\Thumbnails\Particles extracted\particles\vfx\Thumbnails\Particles
    Trove.exe -tool extractarchive particles\vfx\Editor\Thumbnails\Meshes extracted\particles\vfx\Thumbnails\Meshes
    Trove.exe -tool extractarchive particles\vfx\Editor\MaterialProxies extracted\particles\vfx\MaterialProxies

### 解包用户界面

    Trove.exe -tool extractarchive ui extracted\ui
    Trove.exe -tool extractarchive ui\ability_icons extracted\ui\ability_icons
    Trove.exe -tool extractarchive ui\crafting_icons extracted\ui\crafting_icons
    Trove.exe -tool extractarchive ui\fonts extracted\ui\fonts
    Trove.exe -tool extractarchive ui\meta_icons extracted\ui\meta_icons
    Trove.exe -tool extractarchive ui\skins extracted\ui\skins
    Trove.exe -tool extractarchive ui\store extracted\ui\store
    Trove.exe -tool extractarchive ui\classes extracted\ui\classes
    Trove.exe -tool extractarchive ui\tutorial extracted\ui\tutorial

### 解包预设文件(Metaforge)

    Trove.exe -tool extractarchive prefabs\placeable extracted\prefabs\placeable
    
    ~Blocks~
    Trove.exe -tool extractarchive prefabs\placeable\block\color extracted\prefabs\placeable\block\color
    Trove.exe -tool extractarchive prefabs\placeable\block\gameplay extracted\prefabs\placeable\block\gameplay
    Trove.exe -tool extractarchive prefabs\placeable\block\glass extracted\prefabs\placeable\block\glass
    Trove.exe -tool extractarchive prefabs\placeable\block\glow extracted\prefabs\placeable\block\glow
    Trove.exe -tool extractarchive prefabs\placeable\block\ice extracted\prefabs\placeable\block\ice
    Trove.exe -tool extractarchive prefabs\placeable\block\metal extracted\prefabs\placeable\block\metal
    Trove.exe -tool extractarchive prefabs\placeable\block\music extracted\prefabs\placeable\block\music
    Trove.exe -tool extractarchive prefabs\placeable\block\natural extracted\prefabs\placeable\block\natural
    Trove.exe -tool extractarchive prefabs\placeable\block\particles extracted\prefabs\placeable\block\particles
    Trove.exe -tool extractarchive prefabs\placeable\block\primal extracted\prefabs\placeable\block\primal
    Trove.exe -tool extractarchive prefabs\placeable\block\textured extracted\prefabs\placeable\block\textured
    Trove.exe -tool extractarchive prefabs\placeable\block\transmute extracted\prefabs\placeable\block\transmute
    /Blocks
    Trove.exe -tool extractarchive prefabs\placeable\collectible extracted\prefabs\placeable\collectible
    Trove.exe -tool extractarchive prefabs\plant extracted\prefabs\plant
    Trove.exe -tool extractarchive prefabs\placeable\crafting extracted\prefabs\placeable\crafting
    Trove.exe -tool extractarchive prefabs\placeable\deco extracted\prefabs\placeable\deco
    Trove.exe -tool extractarchive prefabs\placeable\mechanical extracted\prefabs\placeable\mechanical
    Trove.exe -tool extractarchive prefabs\placeable\npc extracted\prefabs\placeable\npc
    Trove.exe -tool extractarchive prefabs\placeable\portal extracted\prefabs\placeable\portal
    Trove.exe -tool extractarchive prefabs\placeable\quest extracted\prefabs\placeable\quest
    Trove.exe -tool extractarchive prefabs\placeable\sign extracted\prefabs\placeable\sign
    Trove.exe -tool extractarchive prefabs\placeable\tutorial extracted\prefabs\placeable\tutorial
    Trove.exe -tool extractarchive prefabs\placeable\vendor extracted\prefabs\placeable\vendor

解包后可打开输出路径查看结果。
![解包蓝图](/img/in-post/post-trove-mod-make-unpack/解包蓝图.png)
![解包结果](/img/in-post/post-trove-mod-make-unpack/解包结果.png)

参考资料：[http://forums.trovegame.com/showthread.php?25707-Guide-Comprehensive-Trove-Modding-Tutorial](http://forums.trovegame.com/showthread.php?25707-Guide-Comprehensive-Trove-Modding-Tutorial)

## 使用批处理解包
你也可以使用制作好的批处理来解包全部资源文件。  
不过这会比较耗时间。  
如果你只需要解包一部分，建议还是使用上面的命令来手动解包。

1. 下载[TroveExtract](/assets/in-post/post-trove-mod-make-unpack/TroveExtract.zip)。
2. 将`TroveExtract.bat`文件放入游戏目录，运行该文件。
3. 资源文件将被提取到游戏目录的`extracted`文件夹。
