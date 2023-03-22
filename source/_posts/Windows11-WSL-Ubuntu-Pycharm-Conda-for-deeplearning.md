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

# 目录
- 前言
- 安装wsl
- wsl安装anaconda并配置环境
- Pycharm连接wsl，并使用conda生成的环境



# 前言

通常来说在Linux系统下进行深度学习训练的效率要高于Windows系统，大家通常也是使用Linux常见的发行版本Ubuntu。但是Ubuntu对于日常使用不是很友好，于是就有了折中的方案，使用Windows Subsystem Linux (wsl)。

经过测试，在wsl中的训练效率相比Windows提升了大约25%。以下测试中均使用cuda118,唯一的区别是python版本两个是3.9，一个是3.10。

![Windows](https://s2.loli.net/2023/03/22/PQYkfEWDysUcCNZ.png "Windows_cu118_py39")

![ubuntu20](https://s2.loli.net/2023/03/22/ojpRTbrQJi4D1e8.png "ubuntu20.04_cu118_py39")

![ubuntu22](https://s2.loli.net/2023/03/22/O3Q95mYxHWcB1GT.png "ubuntu22.04_cu118_py310")

![interpreter](https://s2.loli.net/2023/03/22/oaiBn6FWzmxcbHf.png "Python Interpreter")

# 安装wsl

这一部分参考之前的博客[windows 11安装wsl2，ROS以及窗口可视化](https://www.gongsunqi.xyz/posts/451c48f3/),只需要安装wsl2即可，安装ROS的部分不用理会。

# wsl安装anaconda并配置环境

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


