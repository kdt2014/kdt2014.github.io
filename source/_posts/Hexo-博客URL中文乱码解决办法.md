---
title: Hexo 博客URL中文乱码解决办法
tags:
  - 网站
  - 教程
categories: 网站
copyright: true
description: Hexo 博客URL中文乱码解决办法 ，博客文章唯一链接
abbrlink: 6cf92cc
date: 2023-02-02 10:39:07
update: 2023-02-02 10:39:07
---

# 前言

Hexo博客默认的URL生成方式是year/:month/:day/:title/，如果我们的标题中包含中文，那么URL就会出现乱码，并且如果更改标题，URL就会变动。这对使用URL分享文章非常不友好。因此，通过设置安装hexo-abbrlink插件的方式来固定标题，消除中文乱码。

## 安装hexo-abbrlink插件

在博客的根目录下，使用以下命令安装：

    npm install hexo-abbrlink --save

## 修改_config.yml文件

    permalink: posts/:abbrlink/ 
    # abbrlink config
    abbrlink:
    alg: crc32      #support crc16(default) and crc32
    rep: hex        #support dec(default) and hex

修改完成之后，执行：

    hexo clean
    hexo g -d
 
这样以前和之后生成的文章就会根据文章生成的时间戳自动产生标题。

