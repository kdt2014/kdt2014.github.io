---
title: 博客搭建记录
tags:
  - 网站
  - hexo
  - 记录
categories: 网站
copyright: true
description: 记录自己搭建博客的过程，方便以后查阅
abbrlink: ee940876
date: 2021-07-27 16:37:39
update:
---

# 前言
很早就有搭建博客记录生活的想法了，以前看过有人使用WordPress搭建，但是自己尝试了一遍没有成功，所以就一直搁置至今。

最近偶然间看到了有人使用GitHub+Hexo搭建博客，更加的方便易管理，而且自己已经有一个域名了。所以说干就干，下面是整个过程的记录。

# 搭建步骤
1. 注册GitHub，并新建一个仓库
2. 安装git
3. 安装Node.js
4. 安装Hexo
5. 发布第一篇博文
6. 注册域名，并在GitHub上绑定个性化域名
7. 安装网站美化主题
8. hexo指令简介


## 注册GitHub，并新建一个仓库

 [GitHub](https://github.com/)是全球最大的开源社区，在这里你能认识很多有趣的人，并从大佬那里学习很多知识。注册完成后点击屏幕右上角的“+”，然后点击New repository新建一个仓库，仓库的名称为：用户名.github.io，用户名就是你注册时给自己取的名字。Descritopns那里可以填写my personal website，或者其他任何你自己想写的内容。然后保持其他选项默认，点击底部的绿色按钮Create repository即可。
![](https://i.loli.net/2021/07/27/v8oBsiDPux4yGf2.png)

## 安装git ##

从[git](https://git-scm.com/download/win)官网下载对应的版本安装。有时间可以看看[廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)老师的git详细教程。这里我们暂时不需要学习很多指令，先把网站搭起来再慢慢学习。

在电脑硬盘里新建一个名为Hexo的文件夹，你可以放在任何你想放的位置。进入我们刚建立的空文件夹，鼠标右键，选择git bash here。
![](https://i.loli.net/2021/07/27/i5wYpmKHF41rgfD.png)

然后输入以下指令

	git config --global user.name "GitHub用户名"  #记得替换双引号中的内容
	git config --global user.email "GitHub注册邮箱"

接着生成ssh秘钥，这样GitHub就能够认识我们的电脑，方便以后的操作。

	ssh-keygen -t rsa -C "GitHub注册邮箱"  #记得替换双引号中的内容

操作过程中一路回车即可。

按照下图中的路径找到id_rsa.pub这个文件，用记事本打开，然后全选复制内容。打开github的[setting keys界面](https://github.com/settings/keys)，点击绿色的new SSH key按钮，将刚才复制的内容粘贴到key的框中，title一栏可以随意填写，不过我建议你填写正在使用的电脑名称，方便我们知道这是那台设备的ssh key。最后点击下方的 add ssh key即可。

![](https://i.loli.net/2021/07/27/9rjqGPLkCbUmouW.png)

接着我们输入以下指令来验证是否成功添加了SSH:

	ssh git@github.com

如果出现以下截图，说明成功：
![](https://i.loli.net/2021/07/27/FcAXR2Uy8edh7nr.png)

第一次设置的时候可能并不会直接出现这个界面，会有一段较长的文字显示，但是最后的文字是一样的，当时设置时忘记截图了。

## 安装Node.js ##

[Node.js下载网站](https://nodejs.org/en/download/)

从上面的网站下载对应的版本，执行安装即可。windows版本下载的.msi软件包和.exe程序一样，直接双击就能安装。没什么好说的，一路下一步，印象里安装前的最后一步问你是否勾选“自动安装依赖”之类的，我勾选了。

测试是否安装成功，打开命令行界面，输入：

	node -v

如果输出了版本号，说明安装成功。

我们在安装node.js时，也会同时安装npm，类似的，在命令行输入：

	npm -v

如果输出版本号，则安装成功。

## 安装Hexo ##

进入刚刚我们建立的Hexo文件夹内，按住shift键的同时点击鼠标右键，选择**“在windows终端打开”**，此步操作的目的是在你建立的博客文件夹目录下执行操作。

执行以下命令安装hexo：

	npm install -g hexo-cli 

耐心等待安装完成，印象中会在某个地方停顿好久，可以按一下回车键或者空格键，一定要等到程序完全安装结束。接着初始化博客：

	hexo init blog

## 发布第一篇博文 ##


下面就是激动人心的时刻了，发布我们的第一篇博文，跟着命令来吧：

	hexo new my first bolg
	hexo g
	hexo s

完成这些操作后，复制以下地址到浏览器地址栏：

	localhost:4000

就看到我们在博客中添加了一条标题为 my first blog的内容啦。同时在本地hexo/source/_posts目录下看到一个my first blog.md的文件。这个就是我们博客的内容了，可以通过Markdown编辑软件打开，编辑我们想要发布的内容。我使用的是[MarkdownPad2](http://markdownpad.com/)，关于Markdown的语法，你可以参考这个[十分钟学会Markdown](https://www.appinn.com/markdown/)。

注意，这里只是本地预览，我们还需要一些操作将hexo生成的网页真正的发布到互联网上，这里我们是借助github来实现。

在hexo文件夹下找到_config.yml，如下图所示，用文本编辑软件打开。这里安利一下[vs code](https://code.visualstudio.com/)，微软良心产品，各平台通用，不仅能编程，做个文本编辑器也是好用的。如果你实在不想安装软件，好吧，右键，选择用记事本打开。

![](https://i.loli.net/2021/07/27/WQ1BUgvT7a3cGsI.png)

找到下面代码的部分，将repo那部分改成自己的地址：

	deploy:
  		type: git
  		repo: https://github.com/你的ID/你的ID.github.io.git
  		branch: master

养成良好习惯，随手保存，Ctrl+S保平安。

接着安装git部署插件：

	npm install hexo-deployer-git --save

现在我们的博客已经和github建立了联系，而且可以方便的使用git将内容上传到github的仓库里了。

下面就让我们来验证一下吧，跟着下面的命令走：

	hexo clean
	hexo g
	hexo d

网站现在已经成功的部署到互联网上啦，下面我们来访问这个网站：

	你的ID.github.io

如果不出意外的话，现在你的博客已经成功上线啦！

## 安装网站美化主题 ##
默认的博客界面较为简陋，但是开放的互联网为我们提供了各式各样的美化主题，你可以访问[hexo官方主题网站](https://hexo.io/themes/)寻找自己喜欢的样式。

我使用的NexT主题，你完全可以按照[官方说明文档getting-started](https://theme-next.js.org/docs/getting-started/)来一步步安装，使用，个性化这个主题，当然也可以参照这里的中文记录。

在正式的操作开始前，先介绍两个概念，这对接下来的操作很重要：

**Hexo使用的主要配置文件有两个，都叫做_config.yml**

1. 第一个是在站点根目录下，其中包含Hexo的配置。
2. 第二个是在主题根目录下，它由NexT提供，包含了主题的配置。

我们称第一个文件为**网站配置文件**，第二个文件为**主题配置文件**。

好的，概念介绍完毕，继续我们的操作。

在hexo目录中打开命令行（我们已经对这个操作很熟悉了，实际上本篇博客的所有操作都是在这个目录中进行的），然后输入以下指令：

	git clone https://github.com/next-theme/hexo-theme-next themes/next

打开网站配置文件，将主题设定为next

![](https://i.loli.net/2021/07/27/aSgh1df38biv4Nu.png)

现在我们已经成功的安装并且开启了nex主题，那就来检验一下吧：

	hexo clean
	hexo g
	hexo s

在本地浏览器地址栏输入：

	localhost:4000

可以看到我们的网站已经换了一个主题，好看多了。

你还可以打开主题配置文件，选择next主题提供的不同样式：

![](https://i.loli.net/2021/07/27/yeG6FIUQznsWfuh.png)

还有更多的网站个性化设置，善用搜索，也许以后我也会慢慢更新。


## 个性化域名  ##

这个步骤并不是非做不可，但是对于那些想要彰显个性的同学，我们可以设置属于自己的个性化域名。

首先，你需要有一个属于自己的域名，国内可以去[阿里云域名](https://www.alibabacloud.com/zh/domain?utm_key=se_1006854129&utm_content=se_1006854129&gclid=Cj0KCQjw3f6HBhDHARIsAD_i3D8ivJ6aXXy9IXNUr0l1EoWpV5vrNNHlA1ogFasGGEvd7ecMGF_kDHUaAuFBEALw_wcB)注册一个自己喜欢的自定义域名，选便宜的买就行，土豪随意。我是在国外的[godaddy](https://hk.godaddy.com/offers/godaddy?isc=gofhlhk02&countryview=1&currencyType=HKD&gclid=Cj0KCQjw3f6HBhDHARIsAD_i3D9myp_cB1Bq_PqnheVnwliYTwt-v8_2LQGzfYYIwYi5k8lBY1rCjzMaApD6EALw_wcB&gclsrc=aw.ds)上购买的域名，接下来的设置展示也是以godaddy为例。

在域名提供商的DNS管理界面，增加4条A记录，记录名称@，值为4个IP地址，你也可以参考github的官方文档[Configuring an apex domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)来查找这4个IP地址：

	185.199.108.153
	185.199.109.153
	185.199.110.153
	185.199.111.153

设置好之后的界面类似下面这样：

![](https://i.loli.net/2021/07/27/3LOBN59tRThAybl.png)

接着添加一条CNAME记录，名称为:www，值为:你的id.github.io。

![](https://i.loli.net/2021/07/27/i3HjSoe8aRBZGsn.png)

然后登录GitHub，进入刚建立的仓库，点击settings，点击左边列表中选择pages，设置Custom domain，输入你的个性化域名，如下图所示：

![](https://i.loli.net/2021/07/27/PIOiw2rLA1m6xUf.png)

最后一步，在本地的hexo/source文件目录下，新建一个名称为CNAME文件，里面输入你的个性化域名，并将文件保存为所有文件类型。**注意不是保存为txt，是保存为所有文件类型。**

![](https://i.loli.net/2021/07/27/jnu48GlADyBLPRz.png)

好的，大功告成，现在让我们来验证一下吧，依次输入一下命令：

	hexo clean
	hexo g
	hexo d

这时候在浏览器地址栏输入自己的个性化域名即可开心的浏览自己的博客啦。

## hexo指令简介 ##

命令简写

hexo n "blog" #新建文章

hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令

hexo g #生成

hexo s #启动服务预览

hexo d #部署


hexo3连：

	hexo clean
	hexo g
	hexo d


# 写在最后 #

想搭建一个个人博客很快，半天时间就足够了。但是如果你想要它好看，符合自己的需求，还是需要花点功夫慢慢的拾到。不过最重要的一点不要忘记，我们建立博客的初衷是分享自己的内容，这才是最重要的。

