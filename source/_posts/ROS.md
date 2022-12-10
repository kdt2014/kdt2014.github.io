---
title: windows 11安装wsl2，ROS以及窗口可视化
date: 2022-12-10 18:27:58
update: 
tags:
- 系统
- 记录
categories: 系统
copyright: true
description: wsl2 ROS GUI
---
 目的：在windows系统上安装ubuntu系统、安装linux版本的ROS，并且可以使用ubuntu系统中安装软件的图形界面。

- 安装WSL2

请遵循微软官方的安装说明，[wsl2安装](https://learn.microsoft.com/zh-cn/windows/wsl/setup/environment)。

请注意，默认安装的是Ubuntu最新版的，如需安装其他版本，请参照上述说明，到软件商店安装。

- 安装ROS

[ROS](http://wiki.ros.org/melodic/Installation/Ubuntu)，请移步ROS官网安装说明，和在ubuntu主机上安装没有区别。

- 运行

打开win11自带的终端，如下图所示，选择你想要开启的 ubuntu系统版本，点击等待片刻，即可开机。

![终端](https://s2.loli.net/2022/12/10/wiFdS25tg1DhAlY.png)

运行ROS

![roscore](https://s2.loli.net/2022/12/10/qcGPNrO2jmDbuQJ.png)

运行rviz

![rviz](https://s2.loli.net/2022/12/10/nRP29ukhsQi4Sxb.png)

这样你就可以像在Ubuntu主机上一样使用ROS了。