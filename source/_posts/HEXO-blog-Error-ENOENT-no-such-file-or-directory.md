---
title: HEXO blog Error ENOENT no such file or directory
tags:
  - blog
categories: blog
copyright: true
description: Error ENOENT no such file or directory-tomorrow-night.css
abbrlink: cb1473a2
date: 2023-09-14 22:20:04
update: 2023-09-14 22:20:04
---

## 问题描述

新电脑重新部署博客时，出现以下报错

![](https://s2.loli.net/2023/09/14/5DO6XURxpyCHlNd.png)

## 错误分析

从错误提示中，我们可以看到，是因为缺少tomorrow-night.css这个文件

但是如果我们只新建这一个文件，还会出现如下报错：

![](https://s2.loli.net/2023/09/14/DbSHdjhBsIyZT16.png)

并且这个时候博客的排版格式也会变得混乱，图片无法加载显示

## 解决办法

这是因为文件版本冲突造成的，直接用原来可以用的文件覆盖现在的文件即可，具体来说就是把 https://github.com/kdt2014/highlight.js/tree/main/styles styles文件夹直接全部替换原来/home/kdt/Documents/kdt2014.github.io/node_modules/highlight.js/styles的文件夹

