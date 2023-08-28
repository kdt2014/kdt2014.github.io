---
title: Gazebo添加模型
tags:
  - ROS
  - 教程
categories: ROS
copyright: true
description: 使用Blender创建3D模型并添加到Gazebo环境中
abbrlink: cb441177
date: 2023-02-08 13:57:18
update: 2023-02-08 13:57:18
---

# 在gazebo中添加模型（图片）

## 1.前言

在使用Gazebo仿真的过程中常常需要导入用户自定义的模型，特别是一些独特的具有严格尺寸的Mark图标(Apritag, Chessboard等)。目前在Gazebo中一共支持3种模型导入方式，分别是urdf， sdf和3D model，其中最简单的是直接通过CAD绘制出相关的3D model后直接导入模型。在本文中将详细描述相关方法，并编写相应的模型描述文件。

## 2.环境

- Ubuntu 18.04
- Gazebo 9
- Blender 3.4.1

## 3.贴图模型制作

使用各平台支持良好的免费3D建模软件[Blender](https://www.blender.org/)制作，使用snap方式安装：

    sudo snap install blender --classic

启动界面如下图1：
![](https://s2.loli.net/2023/02/07/iu4QaTjUKqd1Y8N.png)

删除初始默认立方体后选择添加 -> 网格 -> 立方体，如图2所示：

![](https://s2.loli.net/2023/02/07/YFNK7jAGsz9gotx.png)

点击界面右上角部分，调整立方体大小，如下图3、图4所示：

![](https://s2.loli.net/2023/02/07/vOZdPCIFo6A8WxL.png)

![](https://s2.loli.net/2023/02/07/qigf764hKF5TYCl.png)

设置尺寸为 x: 0.01m，y: 0.124m，z: 0.16m，设置位置z:0.08，结果如图5所示：

![](https://s2.loli.net/2023/02/07/qE9X81DszQHKTJ3.png)


设置好尺寸后我们设置UV贴图，即贴图图片与3D立方体之间的映射关系，在此我们只贴立方体的一面作为标定板。选择界面上方的UV Editing进入UV编辑模式，如下图6所示：

![](https://s2.loli.net/2023/02/07/WeV51lSqQJdnHE6.png)

注意，这个图左侧为立方体6个面的展开图，因此你可以看到6个正方形相连在一起的图形。右侧为立方体，通过鼠标点击此立方体周围的空白区域，可以取消选定，这时左边左边立方体的6个面展开图就会消失。通过长按鼠标左键选着立方体的一个面作为我们放置贴图的面，这时左边的立方体张开图就只有一个正方形，用鼠标左键与shift键以此点击4个定点，选中该面，结果如图7:
![](https://s2.loli.net/2023/02/07/gD7FbiIGYm1wW2A.png)

在右边区域上方顶栏选着UV--智能UV投射：
![](https://s2.loli.net/2023/02/07/vGIiJyfZqFKULgp.png)

直接确定即可，不需要更改什么。

单击右侧材质选项，点击新建，为立方体新建材质，在基础色选项中选择图像纹理，在图像图像选项中选择打开，选择本地贴图图像。

## 4.模型文件编写

新建文件夹并命名为模型名称。在该文件夹下分别新建model.config，xxx.sdf文件，meshes与materials文件夹，在meshes文件夹下放置3d模型的dae格式文件，在materials文件夹下新建textures文件夹，并将贴图图像文件放入。文件从属关系如下所示。\

    ├── cat_wall.sdf
    ├── materials
    │   └── textures
    │       └── cat_wall.png
    ├── meshes
    │   └── cat_wall.dae
    └── model.config

此处的cat_wall即为模型名称，同时也是上诉所有文件都放置的文件夹。

model.config文件内容如下所示：

    <?xml version="1.0"?>

    <model>
    <name>cat_wall</name>
    <version>1.0</version>
    <sdf version='1.6'>cat_wall.sdf</sdf>

    <author>
        <name>kdt</name>
        <email>kongdt@outlook.com</email>
    </author>

    <description>
        A plane with a reference texture on it depicting a cat.
    </description>
    </model>

    最重要的，一定要修改的是sdf文件的名称，其余作者信息和模型描述可不管。

sdf文件如下所示：

    <?xml version='1.0'?>
    <sdf version="1.6">
    <model name="cat_wall">
    <static>true</static>
        <link name="link">
        <visual name="visual">
            <geometry>
            <mesh>
                <uri>model://cat_wall/meshes/cat_wall.dae</uri>
            </mesh>
            </geometry>
        </visual>
        </link>
    </model>
    </sdf>   

其中为模型名称，在gazebo中也将以该名称显示。在中填入dae模型文件地址。其中model://acircles_pattern为当前文件夹地址。

由此模型描述文件以全部完成，可放置在./gazebo/models文件夹下，在重启gazebo后便可以在插入模型选项中找到该模型。

但由Blender建立的模型在gazebo中显示光泽较黯,可在文本方式下打开dae文件，找到以下选项卡，将数值由0 0 0 1改为0.5 0.5 0.5 0.5。下示为修改后内容:

    <emission>
        <color sid="emission">0.5 0.5 0.5 0.5</color>
    </emission>

有些教程中，将数值全部给1，会过曝。

重新启动gazebo插入模型查看效果，结果如下图：

![](https://s2.loli.net/2023/02/07/TW5s7mbOPgLrHtd.png)


