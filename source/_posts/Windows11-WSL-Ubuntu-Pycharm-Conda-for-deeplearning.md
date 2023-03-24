---
title: Windows11 + WSL Ubuntu + Pycharm + Conda for deeplearning
tags:
  - 教程
  - 深度学习
categories: 教程
copyright: true
description: Windows环境下使用Pycharm连接wsl ubuntu进行深度学习训练
abbrlink: 3c995b2a
date: 2023-03-22 19:56:16
update: 2023-03-22 19:56:16
---

## 目录
- 前言
- 安装wsl
- wsl安装anaconda并配置环境
- Pycharm连接wsl，并使用conda生成的环境



## 前言

通常来说在Linux系统下进行深度学习训练的效率要高于Windows系统，大家通常也是使用Linux常见的发行版本Ubuntu。但是Ubuntu对于日常使用不是很友好，于是就有了折中的方案，使用Windows Subsystem Linux (wsl)。

经过测试，在wsl中的训练效率相比Windows提升了大约25%。以下测试中均使用cuda118,唯一的区别是python版本两个是3.9，一个是3.10。

![Windows](https://s2.loli.net/2023/03/22/PQYkfEWDysUcCNZ.png "Windows_cu118_py39")

![ubuntu20](https://s2.loli.net/2023/03/22/ojpRTbrQJi4D1e8.png "ubuntu20.04_cu118_py39")

![ubuntu22](https://s2.loli.net/2023/03/22/O3Q95mYxHWcB1GT.png "ubuntu22.04_cu118_py310")

![interpreter](https://s2.loli.net/2023/03/22/oaiBn6FWzmxcbHf.png "Python Interpreter")

视频教程链接：[Bilibili](https://www.bilibili.com/video/BV1ok4y1t7XC/)，[Youtube](https://youtu.be/buyogP-KS5w)
## 安装wsl

这一部分参考之前的博客[windows 11安装wsl2，ROS以及窗口可视化](https://www.gongsunqi.xyz/posts/451c48f3/),只需要安装wsl2即可，安装ROS的部分不用理会。

## wsl安装anaconda并配置环境

在Windows11自带的终端中打开上一步安装好的Ubuntu系统，之后的操作就和使用在Ubuntu主机上使用命令行完全一样。

![](https://s2.loli.net/2023/03/22/ZpNOkRvFwSu8K9H.png)

- 安装anaconda

[anaconda3官方下载](https://www.anaconda.com/products/distribution),选择linux版本，鼠标放在其上方右键，复制链接。

![](https://s2.loli.net/2023/03/22/9PVLksuX6BCxaU8.png)

回到Ubuntu的terminal，输入：

    wget https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh

运行以上代码，将会下载anaconda3到wsl ubuntu中。

![](https://s2.loli.net/2023/03/22/yemLhduQx1rHBGP.png)

之后执行：

    sh Anaconda3-2023.03-Linux-x86_64.sh

只需要输入 sh A 然后按Tab键，系统会自动补齐下面内容。

接下来就是安装过程，只需要根据提示按回车或者输入yes即可。

- conda配置环境

1. conda创建虚拟环境

        conda create --name cu118py310 python=3.10  #--name 后面是创建环境的名字，按自己的习惯命名，python=XX，输入自己想用的版本号
        conda activate cu118py310 #激活刚刚创建的环境

    ![conda env](https://s2.loli.net/2023/03/23/imlkrNDYjoqIObA.png "创建虚拟环境")

    ![activate](https://s2.loli.net/2023/03/23/3ZOdr5pcqtUivIB.png "激活环境")

    [常用的conda命令](https://blog.csdn.net/u014628771/article/details/80066624)


2. 配置pytorch

    前往[pytorch官网](https://pytorch.org/get-started/locally/)，选择需要的环境(注意这里选择linux OS），复制conda命令,在terminal中粘贴，回车，安装环境：

      ![](https://s2.loli.net/2023/03/22/VWK7jPvda2rwYsg.png)

        conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

      ![pytorch环境](https://s2.loli.net/2023/03/23/DSwiAanLlV98M3j.png "配置pytorch环境")

wsl的环境配置到此就结束了。

## Pycharm连接wsl，并使用conda生成的环境

Pycharm专业版（社区版和教育版没有方便的wsl功能,软件的下载链接在下面），点击右下选择添加新的Interpreter，操作如下图所示：

![wsl interpreter](https://s2.loli.net/2023/03/23/217LZ495MFT6GCu.png "add wsl interpreter")

选择自己创建的Linux_distribution，然后Next:

![](https://s2.loli.net/2023/03/23/VvnQa8Zr6qYkSPD.png)

Virtualenv Enviroment--Existing--点击...--选择这个路径 \\wsl$\Ubuntu-22.04\home\username\anaconda3\envs\cu118py310\bin\python3，Create。

![](https://s2.loli.net/2023/03/23/3r8Fdsbcv7elPZ2.png)

等待片刻，新的环境就配置好了。然后就可以使用这个环境训练跑起来！

软件百度网盘：链接：https://pan.baidu.com/s/1YkT8CiObO3v2Pnmmld2pqA?pwd=ci4h 
提取码：ci4h
Onedrive: https://1drv.ms/u/s!Arq4VGYuCz4AieNcw-nrj4XXtrugzQ?e=kmmVwH
