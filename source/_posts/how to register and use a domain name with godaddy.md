---
title: 如何在godaddy上注册并使用一个域名
tags:
  - 网络
date: 2022-02-09 17:29:13
update: 2022-02-09 17:29:13
categories: 教程
copyright: true
description: 如何在godaddy上注册并使用一个域名
---

首先登录[godaddy](https://hk.godaddy.com/offers/domains/godaddy-b)网站注册一个自己的账户，然后搜索一个自己喜欢的域名，找个最便宜的付款买了。
![](https://s2.loli.net/2022/02/09/eqiBTaJd4Mp93kl.png)

然后我的产品-管理DNS
![](https://s2.loli.net/2022/02/09/fP9sSEtkbA8FMZp.png)

新增
![](https://s2.loli.net/2022/02/09/qSLrA1o5OpWskHu.png)
类型-A; 名称-随你取，假设我们取anyname；内容值-你服务器的IP地址；TTL-1h
假设你的域名是yoursite.xyz
这样设置好之后，你服务器的ip地址就和anyname.yoursite.xyz建立了映射关系，你在命令行窗口 ping anyname.yoursite.xyz 就显示出你的服务器ip。