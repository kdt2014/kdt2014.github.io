---
title: 如何在IPV4网络环境中使用IPV6网络
tags:
  - 网络
  - 教程
date: 2022-02-08 21:39:43
update: 2022-02-08 21:39:43
categories: 网络
copyright:
description:
---
# 前言

很多校园网pt用户在毕业后没有了IPV6网络，就再也无法顺畅的访问便利的资源站了。即使家里有运营商提供的IPV6地址，但是由于pt站疯了国内的V6 IP，同样没法正常访问。幸运的是，目前国外的IPV6地址还是可以使用的。下面将介绍如果在只有IPV4网络的情况下访问IPV6网站。

# 目录

 - 注册IPV6服务器代理商
 - 建立网络服务
 - 本地网络代理设置

## 注册IPV6服务器代理商

这一步理论上你可以使用任何一家的服务，只要他们提供IPV6 地址，我使用的是[vultr](https://www.vultr.com/?ref=9050063-8H)，使用我提供的链接可以得到100刀用于**首月**的测试，之后就需要你自己付费了，相当于免费用一个月。之后我选择的是最便宜的一个月6刀的服务，几个人合伙使用，妥妥的够用，甚至一半都用不了。
按照下图步骤开一个新的实例，一定记得勾选 Enable IPV6：

![](https://s2.loli.net/2022/02/08/YNl97eXfcOBGkHj.png)
![](https://s2.loli.net/2022/02/08/MCukRh9SKjFf4sb.png)
![](https://s2.loli.net/2022/02/08/S6zRvl1EoAGqej9.png)
![](https://s2.loli.net/2022/02/08/h7iQL4nOvSM6f9d.png)

然后稍等一两分钟，就可以看到新部署的实例了。

点击一下实例，就能够看到详情了，下图是我新开实例的信息，最重要的三点信息，IP, username，password，这些信息在我们远程连接服务器的过程中需要使用。

![](https://s2.loli.net/2022/02/08/IvYqsiyDQMVzjap.png)

## 建立网络服务

- 使用[MobaXterm](https://mobaxterm.mobatek.net/)作为远程 ssh登录工具，良心免费软件，强烈推荐。
- 按照以下步骤输入 IPV4 地址，并且点击OK
![](https://s2.loli.net/2022/02/08/dtQEihBKo4YeRrM.png)
- 在新的界面，login的用户名 root,回车，密码直接在网站上复制，然后回到mobaxterm的界面右键，自己选择一种操作模式，将密码复制进去，回车。
![](https://s2.loli.net/2022/02/08/lxyJ9oMGh2snwPk.png)
- 看到这个界面，我们就成功的连接到了远程服务器
![](https://s2.loli.net/2022/02/08/5Q4GqULpfwsMx1E.png)

- 服务器部署 
这一步你可以参考[我是教程](https://www.jamesdailylife.com/v2ray-vless-tcp-xtls)使用一键脚本部署，部署的命令：
    https://www.jamesdailylife.com/v2ray-vless-tcp-xtls
    wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh

需要注意的是，你需要一个域名，我的是在[狗爹](https://hk.godaddy.com/offers/godaddy?isc=gofhlbhk06&countryview=1&currencyType=HKD&cdtl=c_31722013.g_2972073157.k_kwd-30997737601:loc-200.a_.d_c&msclkid=2d3287737b29148cb308e57100c03be0&utm_source=bing&utm_medium=cpc&utm_campaign=zh-hk_corp-core_sem_bh_b_x_new_x_pros_intl_x_001&utm_term=godaddy&utm_content=GD%20Corp%20Core)注册的，找个最便宜的就行，一年也就10刀出头，或者你自己搜索找一些免费的域名。

## 本地网络代理设置
- 代理客户端
你可以使用[V2rayN](https://github.com/2dust/v2rayN/releases),下载最新版本，这里我们只需下载V2rayN
![](https://s2.loli.net/2022/02/08/mjC6zKedVNHO3SA.png)

然后打开软件，点击检查更新，Xray-core。这时候软件会自动下载一些东西。
等待自动下载完毕，点击设置--v2rayN设置-Core类型-Xray-core。
![](https://s2.loli.net/2022/02/08/JBlzZDvyL4uw1gU.png)

然后导入刚刚“服务器部署”那一步得到的配置链接
![](https://s2.loli.net/2022/02/08/w8PS97D6lvicHIE.png)
然后就能看到类似的配置出现在软件界面
![](https://s2.loli.net/2022/02/08/xvVoUOYqGIKwDl9.png)