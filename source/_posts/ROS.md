---
title: windows 11安装wsl2，ROS以及窗口可视化
tags:
  - 系统
  - wsl2
  - Linux
  - ROS
categories: Linux
copyright: true
description: wsl2 ROS GUI
abbrlink: 451c48f3
date: 2022-12-10 18:27:58
update:
---
 目的：在windows系统上安装ubuntu系统、安装linux版本的ROS，并且可以使用ubuntu系统中安装软件的图形界面。

- 安装wsl2

请遵循微软官方的安装说明，[wsl2安装](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)。

请注意，第四步的内核更新包非常重要，如果缺少，将无法正常使用图形化界面。

完成上面的安装，并且设置好账户和密码之后，需要对wsl功能进行升级，以便使用GUI界面。

以管理员身份打开PowerShell（不知道怎么操作，请百度），然后输入以下命令：

    wsl --update

然后重启wsl使之生效：

    wsl --shutdown

再重新打开ubuntu子系统就可以使用图形界面了。

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