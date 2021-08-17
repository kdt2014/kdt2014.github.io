---
title: Qv2ray使用手册
tags:
  - 网络
  - 工具
date: 2021-08-17 14:20:27
update: 2021-08-17 14:20:27
categories:
copyright: 网络 
description: Qv2ray使用手册
---

# 前言 

Qv2ray是一个很好用的代理软件工具，界面美观，操作便捷。但是对于小白来说，第一次使用它的时候会遇到一些障碍，因此写了这篇文章用来介绍使用步骤。

# 目录

1. Qv2ray的下载与安装
2. 内核的选择
3. 增加你的配置

## Qv2ray的下载与安装

很不幸的是，就在我写这篇文章的时候（2021.8.17），去GitHub上看了一眼，该软件因为开发者内部矛盾，永久停更了（最后更新日期2021.8.17），版本停留在了2.7.0。不过你仍然可以访问他们的[GitHub网站](https://github.com/Qv2ray/Qv2ray/releases)下载自己需要的版本。为了以防万一，我下载了最后的版本，上传到百度云，你也可以通过百度云下载链接：https://pan.baidu.com/s/1WN19u_nsxwNBP_vrbwH6cw ，提取码：4scj

以Windows平台为例，下载.exe程序，然后安装，你可以选择自己喜欢的位置，或者像我一样，一路下一步。

## 内核的选择

如果你使用的是Project X下的v2ray-core，去[这个网址](https://github.com/v2ray/v2ray-core/releases) 下载对应系统版本的内核。

如果你使用的是Project X下的Xray-core, 那么首先你要做的就是去[XTLS的GitHub网站](https://github.com/XTLS/Xray-core/releases/tag/v1.4.2)下载最新的内核。

Xray-core完全兼容v2ray-core，所以为了更好的协议兼容性，强烈建议你更换为Xray-core。

还是以windows平台位例，下载下图中Xray-windows-64.zip文件夹（如果你是32位系统请下载32位的版本），然后放到任何一个你喜欢的位置，解压得到一个新的文件夹Xray-windows-64。

![](https://i.loli.net/2021/08/17/ISizLFW587joXna.png)

下面打开刚刚安装好的Qv2ray软件，然后参照下图进行内核的选择与替换，路径中出现的Xray-windows-64就是你刚刚解压得到的新文件夹。
![](https://i.loli.net/2021/08/17/O3lA5sRbacUP9X1.png)

## 增加你的配置

前两步完成后，就不需要变动了，以后使用我们只需要简单的增加配置文件即可。

将你的配置链接直接黏贴到相应的框框里，然后点击确定，就完成了配置的导入，具体步骤见下图。

![](https://i.loli.net/2021/08/17/ul4MAL1ti2mzGDs.png)

导入成功之后，在软件界面的左边就能看到你的服务了，直接双击该服务，就可以启动，当然你也可以点击软件界面上的三角符号来启动该服务，参见下图。

![](https://i.loli.net/2021/08/17/8nlmAyoXNzORFCw.png)

如果你没有配置链接，你也可以点击新建，手动录入相关的配置信息。如果你看不懂这句话，说明你不是服务的拥有者，没有配置信息。

本人不提供配置链接，请勿索要，谢谢。

# 写在最后

本文只是简单的提供如何使用链接添加服务器，这也是最经常使用最简单的方式。如果你需要知道更多该软件的使用方法，请善用[谷歌](https://www.google.com)和[百度](https://www.baidu.com)。

全文完！