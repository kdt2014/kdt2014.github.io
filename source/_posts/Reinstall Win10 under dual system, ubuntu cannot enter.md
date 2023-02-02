---
title: 双系统下重装Win10，ubuntu无法进入
tags:
  - 系统
  - 记录
categories: 系统
copyright: true
description: 双系统下重装Win10，ubuntu无法进入
abbrlink: 92a850f6
date: 2021-08-05 13:11:31
update:
---

自己笔记本有两个固态硬盘，一个盘装win10，一个盘装ubuntu，都是UEFI引导，硬盘都是GPT分区。

前段时间因为修改注册表之前没备份，把电脑搞坏了，就重装了win10。然后悲剧了，系统引导里没有了ubuntu。网上找遍各种方法，最终找到了使用ubuntu安装U盘引导修复的方法。

1. 使用[rufus](http://rufus.ie/zh/)+U盘制作[Ubuntu](https://ubuntu.com/download/desktop)的系统安装盘。我制作的时候选择的分区类型是GPT，不是默认的MBR,这个具体要看你是如何安装的系统。
2. 插入做好的Ubuntu系统盘，重启电脑，进入BIOS设置，选择U盘作为第一启动项
3. 进入后，选择试用Ubuntu，然后记得一定给系统联网 
4. 打开命令行，输入以下命令：

		sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt-get update  

5. 再接着输入：

		sudo apt-get install -y boot-repair && boot-repair  

耐心等待，在弹出来的对话框中选择第一个“Recommended repair”，接着它可能会提示你什么，点yes即可。稍等片刻，修复完毕。重启电脑，拔掉U盘，就能看到那个熟悉的系统选择界面了。


本文参考：https://blog.csdn.net/weixin_42718092/article/details/88794952

