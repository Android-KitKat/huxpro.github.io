---
layout:     post
title:      "宝藏世界模组开发指南——蓝图"
subtitle:   "宝藏世界模组开发指南"
date:       2017-07-23 15:44:45
author:     "Android"
header-img: "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      false
multilingual: false
tags:
    - 宝藏世界模组开发指南
---
## 蓝图文件
宝藏世界大部分的模型都以蓝图格式储存，它的文件扩展名是`.blueprint`。  
也就是说我们想让宝藏世界读取我们的模型，就需要先转换为蓝图文件。  
蓝图文件包含了材质信息。

## 文件结构
蓝图文件包含多个Qubicle文件。  
Qubicle文件的扩展名是`.qb`。  
![Qubicle文件](/img/in-post/post-trove-mod-make-blueprint/Qubicle文件.png)

所以你得将你的模型[导出]({% post_url 2017-07-19-trove-mod-make-magicavoxel %}#文件区的底部)为Qubicle文件。

每个Qubicle文件都有不同的作用。  
除了原始模型以外，还有定义材质的材质贴图。

| 文件名              | 类型       | 示例                                            |
|:-------------------:|:----------:|:-----------------------------------------------:|
| 类型_分类_名字.qb   | 原始模型   | equipment_weapon_1h_sword_excalibur_morgan.qb   |
| 类型_分类_名字_t.qb | 类型贴图   | equipment_weapon_1h_sword_excalibur_morgan_t.qb |
| 类型_分类_名字_a.qb | 透明贴图   | equipment_weapon_1h_sword_excalibur_morgan_a.qb |
| 类型_分类_名字_s.qb | 高光贴图   | equipment_weapon_1h_sword_excalibur_morgan_s.qb |

它们形状相同且位置重叠，但颜色不相同。  
每个类型都有特定颜色代表其特殊含义。

*所有模型都要包含连接点。*  
连接点是一个只有一格的像素点，用来在游戏中确定模型位置。

## 原始模型
原始模型定义了模型形状和模型颜色。  
我们主要就是在这里做好模型，然后再到材质贴图中涂色来定义材质。

<table style="text-align:center">
  <thead>
    <tr>
      <th>含义</th>
      <th>RGB</th>
      <th>十六进制</th>
      <th>颜色</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>连接点</td>
      <td>255,000,255</td>
      <td>#FF00FF</td>
      <td bgcolor="#FF00FF">&nbsp;</td>
    </tr>
    <tr>
      <td>模型颜色</td>
      <td>任意</td>
      <td>任意</td>
      <td>任意</td>
    </tr>
  </tbody>
</table>

## 类型贴图(Type)
![类型贴图](/img/in-post/post-trove-mod-make-blueprint/类型贴图.png)  
按照列表顺序，除去连接点，从左到右依次排列。
<table style="text-align:center">
  <thead>
    <tr>
      <th>含义</th>
      <th>RGB</th>
      <th>十六进制</th>
      <th>颜色</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>连接点</td>
      <td>255,000,255</td>
      <td>#FF00FF</td>
      <td bgcolor="#FF00FF">&nbsp;</td>
    </tr>
    <tr>
      <td>固体(默认)</td>
      <td>255,255,255</td>
      <td>#FFFFFF</td>
      <td bgcolor="#FFFFFF">&nbsp;</td>
    </tr>
    <tr>
      <td>玻璃</td>
      <td>128,128,128</td>
      <td>#808080</td>
      <td bgcolor="#808080">&nbsp;</td>
    </tr>
    <tr>
      <td>瓷砖玻璃</td>
      <td>064,064,064</td>
      <td>#404040</td>
      <td bgcolor="#404040">&nbsp;</td>
    </tr>
    <tr>
      <td>发光固体</td>
      <td>255,000,000</td>
      <td>#FF0000</td>
      <td bgcolor="#FF0000">&nbsp;</td>
    </tr>
    <tr>
      <td>发光玻璃</td>
      <td>255,255,000</td>
      <td>#FFFF00</td>
      <td bgcolor="#FFFF00">&nbsp;</td>
    </tr>
  </tbody>
</table>

## 透明贴图(Alpha)
![透明贴图](/img/in-post/post-trove-mod-make-blueprint/透明贴图.png)  
按照列表顺序，除去连接点，从左到右依次排列。

*只有类型贴图为玻璃,瓷砖玻璃,发光玻璃时有效。*
<table style="text-align:center">
  <thead>
    <tr>
      <th>含义</th>
      <th>RGB</th>
      <th>十六进制</th>
      <th>颜色</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>连接点</td>
      <td>255,000,255</td>
      <td>#FF00FF</td>
      <td bgcolor="#FF00FF">&nbsp;</td>
    </tr>
    <tr>
      <td>固体(默认)</td>
      <td>255,255,255</td>
      <td>#FFFFFF</td>
      <td bgcolor="#FFFFFF">&nbsp;</td>
    </tr>
    <tr>
      <td>稍微透明</td>
      <td>240,240,240</td>
      <td>#F0F0F0</td>
      <td bgcolor="#F0F0F0">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>208,208,208</td>
      <td>#D0D0D0</td>
      <td bgcolor="#D0D0D0">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>176,176,176</td>
      <td>#B0B0B0</td>
      <td bgcolor="#B0B0B0">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>144,144,144</td>
      <td>#909090</td>
      <td bgcolor="#909090">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>112,112,112</td>
      <td>#707070</td>
      <td bgcolor="#707070">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>080,080,080</td>
      <td>#505050</td>
      <td bgcolor="#505050">&nbsp;</td>
    </tr>
    <tr>
      <td>|</td>
      <td>048,048,048</td>
      <td>#303030</td>
      <td bgcolor="#303030">&nbsp;</td>
    </tr>
    <tr>
      <td>非常透明</td>
      <td>016,016,016</td>
      <td>#101010</td>
      <td bgcolor="#101010">&nbsp;</td>
    </tr>
  </tbody>
</table>

## 高光贴图(Specular)
![高光贴图](/img/in-post/post-trove-mod-make-blueprint/高光贴图.png)  
按照列表顺序，除去连接点，从左到右依次排列。
<table style="text-align:center">
  <thead>
    <tr>
      <th>含义</th>
      <th>RGB</th>
      <th>十六进制</th>
      <th>颜色</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>连接点</td>
      <td>255,000,255</td>
      <td>#FF00FF</td>
      <td bgcolor="#FF00FF">&nbsp;</td>
    </tr>
    <tr>
      <td>粗糙(默认)</td>
      <td>128,000,000</td>
      <td>#800000</td>
      <td bgcolor="#800000">&nbsp;</td>
    </tr>
    <tr>
      <td><font color="#c00">固体*</font></td>
      <td>255,255,255</td>
      <td>#FFFFFF</td>
      <td bgcolor="#FFFFFF">&nbsp;</td>
    </tr>
    <tr>
      <td>金属</td>
      <td>000,128,000</td>
      <td>#008000</td>
      <td bgcolor="#008000">&nbsp;</td>
    </tr>
    <tr>
      <td>水</td>
      <td>000,000,128</td>
      <td>#000080</td>
      <td bgcolor="#000080">&nbsp;</td>
    </tr>
    <tr>
      <td>彩虹</td>
      <td>128,128,000</td>
      <td>#808000</td>
      <td bgcolor="#808000">&nbsp;</td>
    </tr>
    <tr>
      <td>光滑</td>
      <td>128,0,128</td>
      <td>#800080</td>
      <td bgcolor="#800080">&nbsp;</td>
    </tr>
  </tbody>
</table>
*当在类型贴图使用玻璃或透明贴图使用透明时，应将高光贴图设置为固体。*

## 文件转换
蓝图文件和Qubicle文件是可以相互转换的。

### Qubicle文件转换为蓝图文件
确保所有文件都是Qubicle格式，如果不是请先从体素编辑器导出qb文件。  
确保模型与其材质贴图文件位于同一目录，并且文件名正确。

将原始模型的文件拖动到游戏目录的`devtool_convert_to_blueprint.bat`文件上。  
程序会自动加入其他相应的材质贴图文件。  
![拖动文件](/img/in-post/post-trove-mod-make-blueprint/拖动文件1.png)

转换完成后，蓝图文件将出现在模型文件所在目录。

### 蓝图文件转换为Qubicle文件
在游戏目录新建`qbexport`文件夹。

将蓝图文件拖动到游戏目录的`devtool_dungeon_blueprint_to_QB.bat`文件上。  
![拖动文件](/img/in-post/post-trove-mod-make-blueprint/拖动文件2.png)

转换完成后，Qubicle文件将出现在游戏目录的`qbexport`文件夹。

参考资料: [http://trove.wikia.com/wiki/Material_Map_Guide](http://trove.wikia.com/wiki/Material_Map_Guide)
