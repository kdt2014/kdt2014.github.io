---
title: 让自己通过Hexo建立的博客被谷歌搜索到
tags:
  - 网站
  - hexo
date: 2021-08-14 21:23:57
update: 2021-08-14 21:23:57
categories: 网站
copyright: true
description: 让自己通过Hexo建立的博客被谷歌搜索到
---

# 前言

一般我们建立博客的目的就是分享一些东西，那么如何让我们的博客被更多的人看到呢？那当然是被搜索引擎收录后，能够被更多的人用关键词检索到。

本文介绍如何让自己的博客被谷歌搜索引擎搜索到，如需知道如何被百度检索请参考[这篇文章](https://blog.csdn.net/sunshine940326/article/details/70936988/)

# 目录

- 本地配置
- 谷歌搜索配置

## 本地配置

在博客安装根目录，也就是你平时运行 hexo g等命令的那一层目录，执行以下代码：

    npm install hexo-generator-sitemap --save

安装完成后，在.deploy.git文件夹下能发现多了一个sitemap.xml的文件，以后我们每次运行hexo g这个命令时就会生成（更新）这个文件。

打开博客的配置文件（博客安装根目录下）_config.yml，找到以下内容，并将URL更改为自己的网站地址。

![](https://i.loli.net/2021/08/14/ZmsoERqd1va8O7K.png)

## 谷歌搜索配置

首先打开[谷歌搜索配置网站](https://search.google.com/search-console)，如果你没有谷歌账户，没关系注册一个。

点击左上角的三角箭头，然后添加资源，如下图所示：

![](https://i.loli.net/2021/08/14/zmE2BfK5DcC3JWP.png)

然后在下图中的位置填写你的网址，然后点击继续：

![](https://i.loli.net/2021/08/14/DNXbJk2P67YEVgh.png)

在弹出以下界面后，点击“前往资源界面”。

![](https://i.loli.net/2021/08/14/F7i2wcDLsATgUPr.png)

接下来的部分当时布置时我没有截图，只能凭记忆用语言描述以下，很简单的几步操作。

这时的谷歌界面应该是告诉你去DNS服务商那里添加一条TXT记录，然后给了你一串可以复制的代码。

这时打开你购买网址的服务商网站，在DNS解析那里添加一条TXT记录，然后将谷歌提供的内容粘贴进去，保存即可。如下图展示的是在cloudflare中添加TXT记录。

![](https://i.loli.net/2021/08/14/DbxK73CPE4qGtUw.png)

之后在谷歌搜索的console界面就能就能看到我们的网址，然后点击站点地图，添加你自己的网址：https://yoursite/sitemap

![](https://i.loli.net/2021/08/14/KDyd6srqfuXw5Vk.png)

然后就能看到谷歌提示，成功添加。如果你在执行这一步之前没有在配置文件_config.yml中修改url并在修改后执行 hexo g，hexo d，谷歌会报错的。这时你要删掉刚刚添加的站台地图网址，在完成以上动作后，重新添加就不会有报错了。

然后等待谷歌更新，就能收录你的博客内容了。需要一些时间（maybe 几十分钟，maybe更长）。




