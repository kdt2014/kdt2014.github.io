---
title: Ubuntu安装Nodejs
tags:
  - 网站
  - 教程
categories: 网站
copyright: true
description: Ubuntu安装指定版本的Nodejs
abbrlink: 7a25054b
date: 2023-02-02 10:51:15
update: 2023-02-02 10:51:15
---

- 更新软件源

    sudo apt update

- 在 Ubuntu安装 Node.js 14

    curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -

想安装15版本的就把上面的14改成15

- 安装nodejs

    sudo apt -y install nodejs

- 验证安装的 Node.js 版本

    node  -v

    v14.19.1