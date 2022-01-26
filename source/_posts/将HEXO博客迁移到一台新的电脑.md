---
title: 将HEXO博客迁移到一台新的电脑
tags:
  - 网站
  - 教程
date: 2022-01-25 23:50:33
update: 2022-01-25 23:50:33
categories: 网站
copyright: true
description: 将HEXO博客迁移到一台新的电脑
---
# 前言

在一台电脑上部署好了自己的博客，但是我们有时候会需要在其他电脑上更新，比如我在实验室的台式机和自己的笔记本上都有更新博客的需求。
这篇内容将帮助我们解决这个需求！

# 目录

- 创建新的分支
- 新电脑上使用hexo
- 重要提示

## 创建新的分支

首先创建一个hexo分支，如图所示
![](https://s2.loli.net/2022/01/26/Aewlq74MVgtPbo6.png)

然后在setting中将hexo设置为默认分支，这样以后的数据就会同步到这个分支中
![](https://s2.loli.net/2022/01/26/LDWwNoQInAe9t61.png)

接下来我们在本地任意目录下，将刚才这个分支clone下来
使用git bash打开，输入以下命令：
  git clone git@github.com:xxxx/xxxx.github.io.git  记得换成自己的地址

将克隆下来的文件除了.git文件夹之外的所有文件都删除。电脑开启显示隐藏文件就能看到.git.

将之前写的博客源文件全部否复制过来，除了.deploy_git。

需要注意的是，复制过来的文件需要有一个名为.gitignore的文件，如果没有的话，自建一个，里面的内容填写下面所示：

    .DS_Store
    Thumbs.db
    db.json
    *.log
    node_modules/
    public/
    .deploy*/

如果你之前clone过theme中的主题文件，也要把主题中的.git删除。因为git是不能嵌套上传的！

之后分别执行以下命令：

    git add .
    git commit –m "add branch"
    git push 

这样我们就把本地的文件上传到GitHub了。

## 新电脑上使用hexo

- 安装git，参考上一篇教程 [安装git](https://www.gongsunqi.xyz/2021/07/27/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E8%AE%B0%E5%BD%95/#%E5%AE%89%E8%A3%85git)

- 安装Node.js，参考[安装Node.js](https://www.gongsunqi.xyz/2021/07/27/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E8%AE%B0%E5%BD%95/#%E5%AE%89%E8%A3%85Node-js)

- 安装Hexo，这里我们不需要初始化了，参考[安装Hexo](https://www.gongsunqi.xyz/2021/07/27/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E8%AE%B0%E5%BD%95/#%E5%AE%89%E8%A3%85Hexo)

- 同步到本地
在任意自己喜欢的文件夹下面执行：

    git clone git@………………

然后进入到同步下来的文件夹内：

    cd xxx.github.io
    npm install
    npm install hexo-deployer-git --save

- 生成部署

      hexo g
      hexo d

这样我们就在新电脑上设置完成了！

## 重要提示

以后每次写完博客，一定要把源文件同步到GitHub上：

    git add .
    git commit –m "xxxx"
   git push 

每次开始写新的博客之前，执行一下：

    git pull
