---
title: Youtube-dl油管下载神器
date: 2021-08-02 21:08:05
update: 
tags:
- 工具
- youtube-dl
categories: 工具
copyright: true
description: Youtube-dl油管下载神器
---

# 前言 #

之前我都是通过浏览器插件来下载油管上的视频，但是过段时间要么插件失效，要么需要付费。前段时间偶然发现了一个在GitHub上开源的油管视频下载神器[youtube-dl](https://github.com/ytdl-org/youtube-dl), 这篇文章就用来记录使用心得（当然你也可以直接去GitHub上看官方文档，as u like)。

# 安装步骤 #

1. 安装ffmpeg
2. 安装Python
3. 安装youtube-dl
4. 下载

## 安装ffmpeg ##

Fmpeg 是领先的多媒体框架，能够解码、编码、转码、混合、解密、流媒体、过滤和播放人类和机器创造的几乎所有东西。简单来说，我们需要这个软件来帮我们自动处理一些从youtube上下载的软件，最终实现得到一个.mp4文件（也可能是其他格式）。

- 登录[下载网址](https://www.gyan.dev/ffmpeg/builds/),在release处点击第一个链接下载压缩文件，如下图所示（可能随着时间的流逝版本不一样），放在你想放的位置。

 ![](https://i.loli.net/2021/08/02/VxP2en8gp9OYQdS.png)

- 解压刚刚下载的压缩包，然后将解压后的文件夹复制粘贴到C盘根目录，或者任何你喜欢的位置。

    我的安装路径如下图所示：

![](https://i.loli.net/2021/08/02/CDdbzESapRxYngr.png)

- 定位到\bin文件夹，然后鼠标放到窗口的地址栏，复制这个路径，如我的就是：C:\ffmpeg-4.4-full_build\bin。

- 此电脑-属性-高级系统设置-环境变量-在系统变量里选中Path-编辑-新建，然后将刚刚复制的路径黏贴进去。之后点击确定-确定-确定。

![](https://i.loli.net/2021/08/02/tpHqWkV1Pam8nfR.png)
![](https://i.loli.net/2021/08/02/Ovf58xrdy9oHQMa.png)
![](https://i.loli.net/2021/08/02/B23R59qiQbIF7ve.png)

## 安装Python ##

如果你已经安装过Python，直接跳过这一步。如果没安装过，请跟着步骤来。

- update 2021.9.11 我换了一个已经安装了Python的台式机，但是安装下一步的youtube-dl的时候出错了。卸载Python，然后按照下面的步骤重新安装就可以正常使用了。

- [Python官网](https://www.python.org/downloads/)下载最新的安装包
![](https://i.loli.net/2021/08/02/fDwFpOb5XdYicj8.png)

- 点击安装，**记得勾选一开始界面最下面的“add to path"那个选择框**，点击安装，等待安装完成，最后点击下方的解除长度限制“disable path length limit”（我因为为了写这篇博客卸载后重装的，所以截图中并没有这个选项）。

![](https://i.loli.net/2021/08/02/62XJ7SapAoc4gHy.png)
![](https://i.loli.net/2021/08/02/PMBIkX5bc2SrLGR.png)


## 安装youtube-dl ##

如果你的可以正常访问YouTube，请按照这个步骤来，打开电脑的命令行界面，输入以下命令：

	pip install youtube-dl

如果你在国内需要翻墙，那么我们需要先确定一些事情。

- 打开自己的代理软件，运行（务必运行代理）
- 查看http代理的地址和端口，下图所示是Qv2ray，V2rayNG在软件界面最下方可以直接看到。

![](https://i.loli.net/2021/08/02/K6qFpkN4EJjbhLM.png)

然后打开电脑的cmd命令行界面，依次输入以下命令：

	set http_proxy=http://127.0.0.1:8889 #一定记得把ip地址和端口改成自己代理软件中查到的
	pip install youtube-dl
	set http_proxy=
	pause

没有问题的话，就应该安装完成了。

## 下载 ##

下载这个文件夹，链接: https://pan.baidu.com/s/1JL2gB9E1qqPAYgY6sUBWKw 提取码: pjuw。

![](https://i.loli.net/2021/08/02/PcoHBYqENDkjU5u.png)

里面包含上图所示的这些东西。


- 如果你需要代理环境，请用记事本打开上图被圈出来的三个文件，然后将代理部分的ip和端口改成自己软件中显示的。这一步类似安装youtube-dl时我们做的事情。**请务必，将框选出来的三个文件都打开检查一遍！**

![](https://i.loli.net/2021/08/02/fEbBSNkqo73zH5x.png)

- 如果你不需要代理，那么同样打开这三个文件，将所以和set_proxy有关的语句都注释掉即可。


注释的方法也很简单，在语句前面加一个英文输入法状态下的:即可。再啰嗦一句，**请务必，将框选出来的三个文件都打开检查一遍！**

	:set http_proxy=http://127.0.0.1:8889
	:set http_proxy=

OK！ 随便打开一个油管视频，然后将地址复制到_url.txt这个文件里，然后运行_run.bat，视频就会以最高质量下载到youtube-dl-videos文件夹中。

结束！！

最后，感谢[团叽的OO的视频团叽的OO的视频](https://www.bilibili.com/video/BV1AB4y1F7nG?from=search&seid=13837731026935348595)，本文教程属于该视频的文字总结版本。因为担心他的视频也许有一天会找不到，故此做一个文字备份。


