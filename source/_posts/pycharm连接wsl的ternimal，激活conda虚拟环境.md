---
title: 配置pycharm中wsl的ternimal，激活conda虚拟环境
tags:
  - 教程
  - 深度学习
date: 2023-04-01 19:03:00
update: 2023-04-01 19:03:00
categories: 教程
copyright: True
description: 配置pycharm中wsl的ternimal，激活conda虚拟环境
---

本文的前提条件是你已经正确配置了wsl，如果不确定可以参考之前的教程[Windows11 + WSL Ubuntu + Pycharm + Conda for deeplearning](https://www.gongsunqi.xyz/posts/3c995b2a/)。

![](https://s2.loli.net/2023/04/01/O4AFiJQmlwjCRfU.png)

0. 打开pycharm
1. 点击左下部分的Ternimal
2. 点击下三角符号
3. 选择你安装了conda虚拟环境的wsl系统
4. 在ternimal中像在原生linux中使用相关命令，如 conda env list; conda activate myenv...

备注：pycharm为专业版2022.2