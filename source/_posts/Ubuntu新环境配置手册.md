---
title: Ubuntu新环境配置手册
tags:
  - Linux
categories: Linux
copyright: true
description: Ubuntu新环境配置手册
abbrlink: 1e127ae5
date: 2023-02-06 19:51:55
update: 2023-02-06 19:51:55
---

每次重装系统之后，都得需要花费大量的时间来重新配置环境，有些时候之前配置的方式已经忘记了，需要花时间搜索，这种方式效率很低，很可能搜到一些不可用的教程。
因此这篇博客用来记录自己配置环境的整个过程。

## 搜狗输入法

[下载](https://shurufa.sogou.com/linux)
[配置安装](https://shurufa.sogou.com/linux/guide)

安装后显示搜狗输入法，但是无法输入中文：

    sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
 
    sudo apt install libgsettings-qt1

这个命令，上面的配置安装说明后面有写。

## vscode 插件

1. Copilot 基于gpt3的AI代码生成
2. Mrakdown Preview Enhanced
3. Markdown PDF

## 安装美化主题

参考[美化](https://1145141919810.wang/2021-02-28/Ubuntu-20-04-LTS-%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96-%E2%80%94%E2%80%94-%E4%BB%BF-Big-Sur-%E9%A3%8E%E6%A0%BC/)

## Hexo博客迁移

[将HEXO博客迁移到一台新的电脑](https://www.gongsunqi.xyz/posts/d0b820b4/)

## 图床软件PicGo

[PicGo](https://github.com/Molunerfinn/PicGo)

[AppImage创建启动图标](https://bella722.github.io/post/3c4ff36.html)

## Qv2ray和Naiveproxy

[Qv2ray](https://github.com/Qv2ray/Qv2ray)

[NaiveProxy](https://www.dongvps.com/2022-10-27/naiveproxy%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE%E8%84%9A%E6%9C%AC%E5%8F%91%E5%B8%83%EF%BC%88%E5%8F%AF%E8%87%AA%E5%AE%9A%E4%B9%89%E7%AB%AF%E5%8F%A3%EF%BC%89/)

## 录屏软件

simplescreenrecord0.3.6版本:



## 快捷截图软件

flameshot

    sudo apt-get install flameshot

安装之后，4K显示器设置150%等非整数缩放会导致截图不完整等问题，解决方法：

    echo "export QT_AUTO_SCREEN_SCALE_FACTOR=1" >> ~/.profile

该命令的作用是开启QT的自动缩放功能。flameshot基于QT5.9+环境，QT内置了缩放功能，只是很多软件不默认开启。

## 微信

[DotChat](https://github.com/huan/docker-wechat)

这是一个在docker中运行的程序，因此需要安装docker：

    curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

[Docker教程](https://www.runoob.com/docker/ubuntu-docker-install.html)

docker 常用命令：

## bt下载transmission

[Transmission](https://transmissionbt.com/)