---
layout:     post
title:      "宝藏世界模组开发指南——使用MagicaVoxel"
subtitle:   "宝藏世界模组开发指南"
date:       2017-07-19 12:00:00
author:     "Android"
header-img: "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      true
multilingual: false
tags:
    - 宝藏世界模组开发指南
---
<style type="text/css">
    img {
        display: inline !important
    }
</style>
这篇文章篇幅会比较长，不妨一边听着音乐一边看。  
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="330" height="450" src="//music.163.com/outchain/player?type=0&id=327031146&auto=0&height=430"></iframe>

## -目录-

- [目录](#-目录-)
- [体素模型](#-体素模型-)
- [选择编辑器](#-选择编辑器-)
- [基本界面](#-基本界面-)
- [三维坐标系](#-三维坐标系-)
- [显示区](#-显示区-)
  - [视角控制(透视视角)](#视角控制透视视角)
  - [界面介绍](#界面介绍)
    - [显示区的顶部](#显示区的顶部)
    - [显示区的底部](#显示区的底部)
- [调色板区](#-调色板区-)
- [画笔区](#-画笔区-)
  - [画笔类型](#画笔类型)
  - [画笔形状](#画笔形状)
    - [像素](#像素)
    - [面](#面)
    - [长方体](#长方体)
    - [线](#线)
    - [中心](#中心)
    - [图案](#图案)
  - [画笔工具](#画笔工具)
- [文件区](#-文件区-)
  - [文件区的顶部](#文件区的顶部)
  - [文件区的底部](#文件区的底部)
- [编辑区](#-编辑区-)
  - [工具(Tool)](#工具tool)
  - [选择(Select)](#选择select)
  - [旋转(Rot)](#旋转rot)
  - [翻转(Flip)](#翻转flip)
  - [偏移(Loop)](#偏移loop)
  - [比例(Scale)](#比例scale)
  - [重复(Repeat)](#重复repeat)
- [视图区](#-视图区-)
- [菜单区](#-菜单区-)
  - [杂项(Misc)](#杂项misc)
  - [形状(Shape)](#形状shape)
- [快捷键](#-快捷键-)

想要获取更多文章和后续更新，请关注[我的博客](/)和新浪微博[@Android_KitKat](https://weibo.com/u/1695436163)。

## -体素模型-

![体素模型](/img/in-post/post-trove-mod-make-magicavoxel/体素模型.png)  
宝藏世界的模型基本上都是体素(Voxel)模型。  
包括装备，坐骑，宠物，矿车，船。

<div id="container" style="width: 300px; height: 300px;"></div>
<script type="text/javascript" src="/js/libtroxel-1.9.min.js"></script>
<script type="text/javascript">
  var element = document.getElementById('container');
  var model = 'JiY7AVUAEAD486v/APn31v8B+MxQ/wP486v/A/n31v8wD/fN/wHTniL/B/8A//oB/99o/wGwYg//AEwfGf93/wD/+gCCOj3/A9OeIv8AakeN/wB3R41w/wCmAAGAAAGgAAGAAAGgAAGAAAH/AP8A/wD/AP8A/wD/AP8A/wD/AO4AAoAAAqAAAoAAAqAAAYAAAf8A/wD/AP8A/wD/AP8A/wD/AP8A7gACgAACoAACgAACoAABgAAB/wD/AP8A/wD/AP8A/wD/AP8A/wDIAAKAAAKgAAKAAAKgAAGAAAH/AP8AggADgAAD/wD/AP8A/wD/AP8A/wD/AOYAAoAAAqAAAoAAAqAAAYAAAf8AtwAEgAAEoAADgAAD/wD/AP8A/wD/AP8A/wD/AOYAAoAAAqAAAoAAAqAAAYAAAf8AkQAFgAAFoAAEgAAEoAADgAAD/wD/AP8A/wD/AP8A/wD/AOYAAoAAAqAAAoAAAqAAAYAAAewABYAABaAABYAABaAABIAABKAAA4AAA/8A/wD/AP8A/wD/AP8A/wDAAAKAAAKgAAKAAAKgAAKAAAKgAAGAAAHsAAWAAAWgAAWAAAWgAASAAASgAAOAAAP/AP8A/wD/AP8A/wD/AP8AwAACgAACoAACgAACoAABgAAB7AAFgAAFoAAFgAAFoAAFgAAFoAAEgAAEoAADgAAD/wD/AP8A/wD/AP8A/wD/AMAAAoAAAqAAAoAAAqAAAYAAAewABYAABaAABYAABaAABYAABaAABIAABKAAA4AAA/8A/wD/AP8A/wD/AP8A/wCaAAKAAAKgAAKAAAKgAAGAAAH/AJEABYAABaAABYAABaAABYAABaAABIAABKAAA4AAA/8A/wD/AP8A/wD/AP8A/wCaAAKAAAKgAAKAAAKgAAGAAAHsAAWAAAWgAAWAAAWgAAWAAAWgAAWAAAWgAASAAASgAAOAAAP/AP8A/wD/AP8A/wD/APUAAoAAAqAAAoAAAqAAAYAAAf8AkQAFgAAFoAAFgAAFoAAFgAAFoAAEgAAEoAADgAAD/wD/AP8A/wD/AP8A/wD/AJoAAoAAAqAAAYAAAf8AtwAFgAAFoAAFgAAFoAAFgAAFoAAEgAAEoAADgAAD/wD/AP8A/wD/AP8A/wD/AJoAAoAAAqAAAYAAAf8AkQAEgAAEoAAFgAAFoAAFgAAFjwAFBI0ABYAABY0ABAWPAASAAASgAAOAAAP/AP8A/wD/AP8A/wD/AP8AwAACgAACoAABgAAB7AADgAADoAAEgAAEoAAFgAAFjwAEBgSMAASAAASMAAQGBI8AA4AAA/8A/wD/AP8A/wD/AP8A/wDmAAKAAAKgAAKAAAKgAAGAAAHGAAOAAAOgAASAAASgAAWAAAWQAIADBAWKAASAAASKAAUEgAOQAAOAAAP/AP8A/wD/AP8A/wD/AP8A/wCLAAKAAAKgAAGAAAGgAAeAAAegAAeAAwegAAeAAAegAASAAASRAAcDBIAFiAAEgAAEiACABQQDB5EAA4AAA/8A/wD/AP8A/wD/AP8A/wD/ALEAB4AAB6AAB4AAB6AABoADBqAAB4AAB6AAB4AAB5EABwMEgQWFAAcAA4AAAwAHhQCBBQQDB/8A/wD/AP8A/wD/AP8A/wD/AMgAB4AAB6AABoAABqAABoADBqAABoAABqAAB4AAB5IABwMEgQWDAAQHAAOAAAMABwSDAIEFBAMH/wD/AP8A/wD/AP8A/wD/AP8AyQAHgAAHoAAHgAAHoAAGgAMGoAAHgAAHoAAHgAAHkgAHAwSCBYEABAMHhAAHAwSBAIIFBAMH/wD/AP8A/wD/AP8A/wD/AP8A7wAHgAAHoAAHgAMHoAAHgAAHuAAHAwSCBYEAAweGAAcDgQCCBQQDB/8A/wD/AP8A/wD/AP8A/wD/AP8AlACCA94ABwMEBYAEgAUABAMHhgAHAwQAgAWABAUEAwf/AP8A/wD/AP8A/wD/AP8A/wD/AJQAggOgAIIDnwAEggAEkgAHAwSABwQFAAMHgAAEggAEgAAHAwAFBIAHBAMHiQCAB4UABIIABIUAgAf/AP8A/wD/AP8A/wD/AP8A/wDzAIIDoACCA7kABwMHgAYHBAMHgQADggADgQAHAwQHgAYHAweIAAeABgeEAAOCAAOEAAeABgeUAASCAAT/AP8A/wD/AP8A/wD/AP8A/wDWAIIDoACCA5wAB4AAhAOAAAePAAcDB4AGBwQDgAeAAAeCAAeAAIAHAwQHgAYHAweIAAeABgeEAAeCAAeEAAeABgeUAAOCAAOeAAOCAAPEAASCAAT/AP8A/wD/AP8A/wD/AP8A5gCAA6AABACAAwAEngCEA5MABwOAB4ADB4wAB4ADgAcDB4oAgAeSAIAHlQAHggAHngAHggAHngADggADngAEggAE/wD/AP8A/wD/AP8A/wD/AOQABACAAwAEngADAIADAAOeAAeCAweTAAeBA4AHjgCAB4EDB98AB4IAB54AA4IAA54ABIIABP8A/wD/AP8A/wD/AP8A/wDkAASCAASeAAMAgAMAA54AB4IDB5QAgQeHAIADhwCBB+AAA4IAA54ABIIABP8A/wD/AP8A/wD/AP8A/wD/AIkABIIABKAAgAOgAIEDCIADngADAIADAAOeAAeCAAeeAAeCAAeeAAOCAAP/AP8A/wD/AP8A/wD/AP8A/wD9AIADoAAEggMEngADAIADAAOeAAOCAAP/AP8A/wD/AP8A/wD/AP8A/wD/AOwABACACQAEngAEggMEngAEAIADAAT/AP8A/wD/AP8A/wD/AP8A/wD/AKEAggmfAIQDngAHggMHngAHggMHnwCCA/8A/wD/AP8A/wD/ALcACoIACv8A2wCACYAAgAmeAIAJgACACcQAAwmAAAkDngADCYAACQOfAIIJnwCEA54AhAOeAAeCAweeAAeCAwefAIID/wD/AP8A/wD/AP8AtwAKggAKngAKggAK/wC1AIAJgACACZ4AgAmAAIAJnQAHAwmAAAkDB5wABwMJgAAJAwecAIADCYAACYADnQADggkDnQCGA5wAhgOcAIYDnACGA5wAhgOdAIQDnwCCC6EAgAv/AP8A/wD/AP8AxgCBCoAAgQqcAIEKgACBCp0ACoIACv8AjQAHhgAHmwAHAwmAAAkDB5wABgMJgAAJAwacAAYMCYAACQwGnAAHAwmAAAkDB50AgAuACoALnQALhAMLnAALhAMLnAALhAMLnAALhAMLnAALhAMLnAALhAMLnQCAC4ANgAv/AP8A/wD/AP8A6gCBCoAAgQr/ANgAB4YAB5oABAcDCYAACQMHBJoABAYDCYAACQMGBJsABgMJgAAJAwacAAcDCYAACQMHnQADggkDnQAOhAMOnAAOhAMOnAAOhAMOnACGA5sAC4YDC5sAC4QDC50AC4INC/8A/wD/AP8A/wDqAAoACoAACgAK/wDYAAeGAAeaAAOGAAOaAAQHAwmAAAkDBwSaAAQHAwmAAAkDBwSaAASAAwmAAAmAAwScAAOCCQOdAA6EAw6cAAaEAwacAA6AAwiBAw6bAAqGAwqaAAuGAwubAAuEAwudAAuCDQv/AP8A/wD/AP8A/wD/AMsAB4YAB5oAA4YAA5oABIYABJoABIYABJoABIYABJoABAADggkDAASbAA6EAw6cAA6EAw6cAA6EAw6bAAqGAwqaAAuGAwubAAuEAwudAAuCDQv/AP8A/wD/AP8A/wD/APEAB4YAB5oAA4YAA5oABIYABJoABIYABJoABAADggkDAASaAASGAwSbAAuEAwucAAuEAwucAAuEAwubAAuGAwubAAuEAwudAAuCDQv/AP8A/wD/AP8A/wD/APEAB4YAB5oAA4YAA5oABIYABJoABIYABJoABACAC4AKgAsABJoABAuEAwsEmgAEhgMEmwCGA5wAhgOcAIYDnAALhAMLnQCAC4ANgAv/AP8A/wD/AP8A/wD/APEAB4YAB5oAA4YAA5oAA4YAA5oABIYABJoABAADggkDAASaAASGAwSaAASGAwSbAIYDnACGA5wAhgOdAIQDoACAC6IAgAv/AP8A/wD/AP8A/wD/AM0AB4YAB5oAA4YAA5oAA4YAA5oABIYABJoAA4YAA5oAA4AAggmAAAOaAAQAhAMABJoABACEAwAEnACEA58AggPtAIAL/wD/AP8A/wD/AP8A/wDzAAeGAAeaAAOGAAOaAAOGAAOZAIAHhgCAB5gAgAeGAIAHmQADgACCCYAAA5oABACEAwAEnAAHggMHngAHggMH/wD/AP8A/wD/AP8A/wD/AOIAB4YAB5oAA4YAA5kAgAeGAIAHmACABoYAgAaYAIAGhgCABpgAgAeAAIIJgACAB5kAAwCEAwADmgADAAeCAwcAA5wAB4IDB58AggPrAA6CAA7/AP8A/wD/AP8A/wD/AMsAB4YAB5oAA4YAA5kAgAeGAIAHmACABoYAgAaYAIAGhgCABpgAgAeAAIIJgACAB5kAAwCEAwADmgAHAIQDAAecAIQDnwCCA6EAgAOgAA4AgAMADp4ADgCAAwAOoACAA6IAgAOiAIAD/wDdAA6CAA7/AP8A/wD/AP8AnQAHhgAHmgADhgADmQCAB4YAgAeYAIAHhgCAB5kAA4YAA5oAA4AAggmAAAOaAAcAAwmAAwkDAAecAIQDnwADCIADoACCA58ADoIDDp4ADoIDDp8AggOgAIIDnwAHggMHnwCCA6AAggPrAA6CAA6eAA6CAA7/AP8A/wD/AP8AnQAHhgAHmgADhgADmgADhgADmgADhgADmgADhgADmgAHgQCAB4EAB50AB4AGB6AAB4AGB6AACYADCaAACYADCaAACYADCaAACYADCaAAggOfAAeCAweeAIQDngAHggMHnwCAAwgDoACCA6AADoADDp8AgA6AAIAOngAOggAO6wCCBMQAgAOCAIADnACABoIAgAacAIAGggCABv8A/wD/ALoAB4YAB5oAB4YAB5oAB4YAB5oAB4YAB8QAgAahAAeABgehAIAHogCACaIAgAmiAIAJogCACaEAggOfAAeCAwefAIIDoACCA6AAggOgAIIDoQCAA+0AA4AAA58ABIIDBMMAgAOCAIADnACABoIAgAacAIAGggCABp0ABoIABv8A/wD/AP8A/wD/ANwACYIDCZ4ACYIDCZ8AggOfAA6CAw6eAA6CAw6fAIIDoACCA+sAA4IAA50ABAOCAAME/wD/AP8A/wD/AP8A/wD/AJcAhAmeAAkDgA8DCZ4ADoIDDp4ABoIDBp4ABoIDBp4ADoIDDp8AggPtAIAGnwAEAwCABgADBJ8AgAaiAIAG/wD/AP8A/wD/AP8A/wDQAIIJoAADgA8DnwAOggMOngAGggMGngAGA4AQAwaeAA6CAw6gAIAD7gCABp8ABAMAgAYAAwSfAIAGogCABv8A/wD/AP8A/wD/AP8A0ACCCaAAA4APA6AAggOfAA6CAw6eAA4DgBADDqAAgAP/AJEAA4IAA50ABAOCAAME/wD/AP8A/wD/AP8A/wD/AJkAgAShAAOADwOgAIIDoACCA6EAgAP/ALgAA4AAA58ABIIDBMMAgAOCAIADnACABoIAgAacAIAGggCABp0ABoIABv8A/wD/AP8A/wD/AN4AgASiAIAEogCABP8A/wCpAIIExACAA4IAgAOcAIAGggCABpwAgAaCAIAG/wD/AP8A/wD/AP8A/wCCAIAEogCABP8A/wD/AP8A/wD/AP8A/wD/AP8A8ACABKIAgAT/AP8A/wD/AP8A/wD/AP8A/wD/AP8AlQCABP8A/wD/AP8A/wD/AP8A/wD/AP8A/wCVAIAE/wD/AP8A/wCgAA==';
  Troxel.renderBase64(model, element, {
    rendererClearColor: 0xffffff
  });
</script>
这种由三维像素构成的模型。  
我们想要制作这种模型，就需要用到体素编辑器。

## -选择编辑器-

我推荐使用[MagicaVoxel](https://ephtracy.github.io/)，因为它好用而且免费，还可以直接导出我们需要的文件格式。  
你也可以使用[Qubicle Voxel Editor](http://store.steampowered.com/app/454550/Qubicle_Voxel_Editor/)，它的功能更加强大，不过它是收费的。

我这里就主要讲解MagicaVoxel的使用方法。

## -基本界面-

![MagicaVoxel界面](/img/in-post/post-trove-mod-make-magicavoxel/MagicaVoxel界面.png)

## -三维坐标系-

![三维直角坐标系](/img/in-post/post-trove-mod-make-magicavoxel/三维直角坐标系.png)  
要制作模型，那首先就要找到一个方法，来确定位置。  
MagicaVoxel使用的是三维直角坐标系，即坐标系的三个轴都相互垂直。

<p style="color: red;">X代表横向轴。</p>
<p style="color: green;">Y代表纵向轴。</p>
<p style="color: blue;">Z代表竖向轴。</p>

三个轴的相交点叫做原点。

## -显示区-

![显示区](/img/in-post/post-trove-mod-make-magicavoxel/显示区.png)

### 视角控制(透视视角)
`鼠标右键`拖动或按`Q`,`E`,`A`,`D`键可以旋转视角。  
`鼠标滚轮`或按`W`,`D`键可以缩放视角。  
`鼠标中键`拖动可以移动视角。

### 界面介绍

#### 显示区的顶部

要做模型，第一步当然是先给模型起一个名字。  
显示区正上方有一个写着Name的输入框，可以设置模型的名字。  
设置完之后它会让你选择保存位置。

名字栏右侧的小按钮，点击可以保存模型。  
灰色代表已经保存，橙色代表未保存。

左上角的`Model`和`Render`按钮可以切换模式，建模模式或是渲染模式。

右上角的Size输入框可以限定模型的边界大小，超出边界的像素将被删除。  
`F`按钮可以将边界适合模型尺寸，即边界贴合模型。

左上角的`▼`按钮可以打开动画界面。  
![动画界面](/img/in-post/post-trove-mod-make-magicavoxel/动画界面.png)  
`+`按钮可以创建帧，`-`按钮可以删除选择帧。  
`►`按钮长按可以正序播放动画，`◄`按钮长按可以倒序播放动画。

#### 显示区的底部

左下角的![截图](/img/in-post/post-trove-mod-make-magicavoxel/icon/screenshot.gif)按钮可以将显示内容保存为截图。  
![截图](/img/in-post/post-trove-mod-make-magicavoxel/icon/screenshot.gif)右侧的小按钮可以切换是否在截图中带有透明通道。

正下方的输入框是控制台，可以输入一些命令。  
你选择像素的时候它也会显示像素的坐标位置。

右下角的`Pers`,`Free`,`Orth`,`Iso`这几个按钮可以切换摄像机视角。  
分别对应透视，自由，正交和等距。

右下角的![标尺](/img/in-post/post-trove-mod-make-magicavoxel/icon/ruler.gif)按钮可以切换是否显示标尺。

右下角的![重置摄像机](/img/in-post/post-trove-mod-make-magicavoxel/icon/reset_camera.gif)按钮可以重置摄像机。

![标尺](/img/in-post/post-trove-mod-make-magicavoxel/icon/ruler.gif)左侧的两个小按钮是摄像机槽位，可以储存两个摄像机位置。  
按F5保存摄像机位置，按F7载入。

![重置摄像机](/img/in-post/post-trove-mod-make-magicavoxel/icon/reset_camera.gif)右侧的按钮可以切换是否自动重置摄像机。

整个显示区最底部，时不时会显示一些文字的文字栏是提示栏。  
可以对你当前的选择提供一些提示。

## -调色板区-

![调色板区](/img/in-post/post-trove-mod-make-magicavoxel/调色板区.png)  
在我们编辑模型之前，要先调整一下颜色。  
调色板每个格子都可以存放一个颜色。

选择一个格子后，展开最下方的卷展栏即可调整颜色。  
![调整颜色](/img/in-post/post-trove-mod-make-magicavoxel/调整颜色.png)  
左下角的![菜单](/img/in-post/post-trove-mod-make-magicavoxel/icon/menu.gif)按钮可以切换调色器，是使用HSV还是RGB。  
HSV就是通过色调，饱和度，明度来进行调色，而RGB就是通过红，绿，蓝进行调色。  
你也可以直接在下方的输入框输入RGB颜色代码。

底部的`Save`和`Open`按钮可以将调色板保存和载入。

调色板最上方的`0`,`1`,`2`,`3`按钮可以切换不同的调色板栏位，你一共可以使用四个栏位。

上方左侧的按钮`E`可以将所选颜色设置为视图的边框颜色，按钮`G`则是设置视图的地面颜色。

## -画笔区-

![画笔区](/img/in-post/post-trove-mod-make-magicavoxel/画笔区.png)  
调整好颜色后，就可以编辑模型了。  
*这里的操作方法都是调整好画笔后，在显示区 `左键` 或 `左键拖动` 就可以使用。*

### 画笔类型

`Attach`是增加像素。  
`Erase`是删除像素。  
`Paint`是给像素涂色。

它们都有一个相同的子菜单。

`Mirror`是镜像，即所选轴的所有操作都会对称。  
如果模型的边界大小限定为偶数则是偶数对称，限定为奇数则是奇数对称。

`Axis`是轴模式，可以把所选轴的操作最大化。

### 画笔形状

画笔区最上面的六个单字按钮，可以调整上述三个画笔的形状。  
部分形状选择后会多出子菜单，可以对形状进行具体调整。

#### 像素  
`V`是像素，顾名思义就是可以操作一个像素。  
像素会多出`Vox`菜单。  
输入框可以设置像素的大小，范围1-64。右侧的按钮可以拖动调整数值，上下箭头可以长按调整数值。  
`Cube`是方形像素，`Sphr`是圆形像素，点击可以切换。  
`3D`是三维像素，`2D`是二维像素，点击可以切换。

#### 面  
`F`是面，可以操作一个面。  
面会多出`Face`菜单。  
`Co`是从颜色上区分是否是一个面，`Ge`是从几何上区分是否是一个面，点击可以切换。  
`Pa`是使用调色板颜色，`Su`是使用原始表面颜色，点击可以切换。  
`4`是只通过上下左右判断面是否相连，`8`是通过上下左右和斜的左上右上左下右下来判断面是否相连，点击可以切换。

#### 长方体  
`B`是长方体，可以操作一个长方体。  
长方体没有子菜单。

#### 线   
`L`是线，可以操作一条线。  
线会多出`Line`菜单。  
`Straight`是直行模式，`Project`是投影模式，点击可以切换。  
直行模式就是直接连接拖动的两个点，而投影模式会依附现有模型来连接拖动的两个点。

#### 中心  
`C`是中心，可以操作一个从中心开始的图形。  
中心会多出`Center`菜单。  
`Circler`是画圆，`Square`是画矩形，点击可以切换。  
`O`是奇数直径，`E`是偶数直径，点击可以切换。

#### 图案  
`P`是图案，可以将选择的像素保存为图案。然后就可以操作一个图案的区域。  
图案会多出`Patt`菜单。  
先用像素创建好一个图案，然后用选择工具把像素选择。  
点击Patt菜单的![区域](/img/in-post/post-trove-mod-make-magicavoxel/icon/area.gif)就可以根据选择区域创建一个图案。  
`Raw`是使用原有图案颜色，`Pal`是使用调色板颜色，点击可以切换。

### 画笔工具

![移动](/img/in-post/post-trove-mod-make-magicavoxel/icon/move.gif)可以移动整个模型。

![区域](/img/in-post/post-trove-mod-make-magicavoxel/icon/area.gif)可以选取像素。  
该工具有一个子菜单![区域](/img/in-post/post-trove-mod-make-magicavoxel/icon/area.gif)。  
`Box`是长方体选区，Rect是矩形选区。

![区域](/img/in-post/post-trove-mod-make-magicavoxel/icon/region.gif)可以选取一片区域的像素。  
该工具有一个子菜单![区域](/img/in-post/post-trove-mod-make-magicavoxel/icon/region.gif)。  
`V`只会选取相邻的像素，`F`只会选取一个面，`A`是选取全部相同颜色的像素。  
`Col`是从颜色上判断是不是一块区域，`Geo`是从几何上判断是不是一块区域，点击可以切换。  
`4`是只通过上下左右判断区域是否相连，`8`是通过上下左右和斜的左上右上左下右下来判断区域是否相连，点击可以切换。

`<`按钮可以拾取点击的像素的颜色。

`-`按钮可以移除相同颜色的像素。

`>`按钮可以将相同颜色的像素全部替换为调色板颜色。

## -文件区-

![文件区](/img/in-post/post-trove-mod-make-magicavoxel/文件区.png)  
中间的部分不用说，当然就是文件列表了，点击就可以打开文件。  
它是在软件目录的`vox`文件夹下。  
里面有一些预设的模型。

### 文件区的顶部

`Model`和`Pattern`是选择打开模型的方式。  
`Model`是关闭当前文件，载入选择的文件。  
`Pattern`是将选择的文件作为图案画笔的图案，然后就可以用图案画笔将模型导入到另一个模型内。

`Save`是将当前模型保存。  
`As`是将当前模型另存为。  
`New`是新建模型，效果是用调色板颜色填充整个边界。  
`+`是为当前模型创建一个副本。

### 文件区的底部

`Open`是打开文件，只能打开vox格式的文件。  
`...`是导入文件，可以将其他格式的文件导入。  
![删除](/img/in-post/post-trove-mod-make-magicavoxel/icon/delete.gif)可以删除文件列表所选的文件。

底部有一个`Export`导出卷展栏，展开后有各种格式，点击可以将模型以所选格式导出。  
![导出界面](/img/in-post/post-trove-mod-make-magicavoxel/导出界面.png)

## -编辑区-

![编辑区](/img/in-post/post-trove-mod-make-magicavoxel/编辑区.png)  
最上面的![撤销](/img/in-post/post-trove-mod-make-magicavoxel/icon/undo.gif)和![恢复](/img/in-post/post-trove-mod-make-magicavoxel/icon/redo.gif)是撤销操作和恢复操作。

*以下所有操作，如果没有所选区域，则应用到整个模型。*

### 工具(Tool)

`Full`将整个模型全部填充为调色板颜色的像素。  
`Fill`将所选区域填充为调色板颜色。  
`Zero`将所选区域清空。  
`2X`将所选区域的像素放大到2倍大小。

### 选择(Select)

`All`全选所有像素。  
`Inv`反选所有像素。  
`None`取消选择像素。  
`Copy`复制所选区域内像素。  
`Cut`剪切所选区域内像素。  
`Paste`粘贴复制的像素。

### 旋转(Rot)

`X`所选区域的像素绕X轴旋转。  
`Y`所选区域的像素绕Y轴旋转。  
`Z`所选区域的像素绕Z轴旋转。

### 翻转(Flip)

`X`所选区域的像素沿X轴翻转。  
`Y`所选区域的像素沿Y轴翻转。  
`Z`所选区域的像素沿Z轴翻转。

### 偏移(Loop)

`+X`所选区域的像素在X轴+1。  
`-X`所选区域的像素在X轴-1。  
`+Y`所选区域的像素在Y轴+1。  
`-Y`所选区域的像素在Y轴-1。  
`+Z`所选区域的像素在Z轴+1。  
`-Z`所选区域的像素在Z轴-1。

### 比例(Scale)

输入框输入后按回车，可以将所选区域的像素大小调整到指定倍数。

格式: `[想要调整的轴] [倍数]`  
如果不指定轴则默认全部轴。  
例如: `XY 2`  
即所选区域的像素大小在X和Y轴上调整到两倍。

### 重复(Repeat)

输入框输入后按回车，可以将所选区域的像素在指定轴上重复指定次数。

格式: `[想要重复的轴] [次数]`  
如果不指定轴则默认全部轴。  
例如: `XY 2`  
即所选区域的像素在X和Y轴上重复两次。

## -视图区-

![视图区](/img/in-post/post-trove-mod-make-magicavoxel/视图区.png)  
视图区可以调整显示区的显示，点击可以切换。

`GD`是否显示地面。  
`Edge`是否显示边缘。  
`SW`是否显示阴影。  
`Grid`是否显示网格。  
`Frame`是否显示框架，左侧的输入框可以调整每一格占多少像素。

## -菜单区-

![菜单区](/img/in-post/post-trove-mod-make-magicavoxel/菜单区.png)  
菜单区包含一些特殊的操作。![就是有这种操作](/img/in-post/post-trove-mod-make-magicavoxel/就是有这种操作.png)  
*以下所有操作，如果没有所选区域，则应用到整个模型。*

### 杂项(Misc)

`Shell`删除模型不可见的像素，即删除模型内部的像素。就像它的名字一样，将模型掏空，变成空壳。![好像身体被掏空](/img/in-post/post-trove-mod-make-magicavoxel/好像身体被掏空.png)  
`I`将模型不可见的空间用调色板颜色的像素填充，即将模型内部填充。  
`Fract`将模型导入到当前每一个像素的位置，一个像素即是一个被导入的模型。  
`R`使用调色板所有格子的颜色为所选区域随机涂色。  
`Dilat`在所选区域外层附上一层调色板颜色的像素。  
`E`删除所选区域的外层。

### 形状(Shape)

抛弃当前模型，用指定形状填充模型边界。  
按钮分别对应以下形状。

`Elli`球形  
`Cyli`圆柱  
`Pyra`金字塔  
`Cone`椎体  
`Maze`迷宫  
`Perl`Perlin噪声(Perlin Noise)。一个不断变化的但相连的模型，类似洞穴。

## -快捷键-

如果所有操作都点来点去的未免太麻烦了，所以要勤用快捷键。

| 按键                    | 命令                            | 变化                                          |
| ----------------------- | ------------------------------- | --------------------------------------------- |
| >> 控制台               |                                 |                                               |
| TAB                     | 激活控制台                      |                                               |
| F6 / 6                  | 截图                            | +CTRL : 对于整个窗口                          |
| >> 摄像机               |                                 |                                               |
| 鼠标右键                | 旋转摄像机                      | =鼠标左键+M                                   |
| 鼠标中键                | 移动摄像机焦点                  |                                               |
| 鼠标右键+空格           | 移动摄像机焦点                  | =WASDQE+空格                                  |
| X+鼠标右键              | 设置摄像机焦点                  |                                               |
| K+鼠标右键              | 导航到90度的视角                |                                               |
| 鼠标右键+Ruler          | 摄像机角度固定为5的倍数         | *并找不到Ruler键*                             |
| WASDQE                  | 旋转摄像机/移动摄像机(自由视角) |                                               |
| 鼠标滚轮                | 放大/缩小                       |                                               |
| F5 / 5                  | 保存当前摄像机姿态              |                                               |
| F7 / 7                  | 载入当前摄像机姿态              |                                               |
| >> 模型文件             |                                 |                                               |
| Ctrl+S                  | 保存模型                        |                                               |
| Ctrl+Shift+S            | 另存为                          |                                               |
| Ctrl+O                  | 打开模型                        |                                               |
| Ctrl+Shift+O            | 导入模型                        |                                               |
| Ctrl+N                  | 新建模型                        |                                               |
| Ctrl+Shift+N            | 新建模型副本                    |                                               |
| >> 编辑                 |                                 |                                               |
| Ctrl+Z                  | 撤销                            |                                               |
| Ctrl+Y                  | 还原                            | =Ctrl+Shift+Z                                 |
| U                       | 填充模型                        |                                               |
| I                       | 涂色模型                        |                                               |
| 退格 / 删除             | 清空模型                        |                                               |
| >> 选择                 |                                 |                                               |
| Ctrl+A                  | 全选                            |                                               |
| Ctrl+R                  | 反选                            |                                               |
| Ctrl+D                  | 取消所有选择                    |                                               |
| Ctrl+C                  | 复制像素                        |                                               |
| Ctrl+X                  | 剪切像素                        |                                               |
| Ctrl+V                  | 粘贴像素                        |                                               |
| >> 画笔形状             |                                 |                                               |
| V                       | 像素形状画笔                    | +/- : 调整画笔大小                            |
| F                       | 面形状画笔                      |                                               |
| B                       | 长方体形状画笔                  |                                               |
| L                       | 线形状画笔                      |                                               |
| L                       | 中心形状画笔                    |                                               |
| P                       | 图案形状画笔                    | +/-, 9, 0 : 绕Z, X, Y轴旋转                   |
|                         |                                 | 方向键 / 翻页键 : 添加局部偏移到图案模型      |
|                         |                                 | Home : 将局部偏移复位到0                      |
| >> 画笔类型             |                                 |                                               |
| T                       | 增加画笔                        | +Shift : 暂时切换到擦除画笔                   |
| R                       | 擦除画笔                        | +Shift : 暂时切换到增加画笔                   |
| G                       | 涂色画笔                        |                                               |
| >> 画笔工具             |                                 |                                               |
| Ctrl+鼠标左键           | 移动模型                        | +Shift : 沿法线(远近)方向移动                 |
| N                       | 选择工具                        | +Shift : 增加选择; +Shift+Alt : 减少选择      |
| Alt+鼠标左键            | 拾取像素颜色                    |                                               |
| 鼠标左键 [渲染模式]     | 拾取景深的焦点                  |                                               |
| Alt+鼠标左键 [渲染模式] | 拾取像素的材质                  |                                               |
| >> 镜像模式             |                                 |                                               |
| 1                       | 镜像X轴                         |                                               |
| 2                       | 镜像Y轴                         |                                               |
| 3                       | 镜像Z轴                         |                                               |
| >> 轴模式               |                                 |                                               |
| Ctrl+1                  | 最大化X轴                       |                                               |
| Ctrl+2                  | 最大化Y轴                       |                                               |
| Ctrl+3                  | 最大化Z轴                       |                                               |
| >> 视图                 |                                 |                                               |
| Ctrl+U                  | 显示地面                        |                                               |
| Ctrl+E                  | 显示边缘                        |                                               |
| Ctrl+W                  | 显示阴影                        |                                               |
| Ctrl+G                  | 显示网格                        |                                               |
| Ctrl+F                  | 显示框架                        |                                               |
| Ctrl+B                  | 显示背景                        |                                               |
| >> 调色板               |                                 |                                               |
| Ctrl+拖动               | 复制颜色                        |                                               |
| Ctrl+Shift+拖动         | 填充格子                        |                                               |
| Alt+Shift+拖动          | 填充渐变格子                    |                                               |

<center><img src="/img/in-post/post-trove-mod-make-magicavoxel/对方向你扔了一个新浪微博.png" alt="对方向你扔了一个新浪微博"></center>
