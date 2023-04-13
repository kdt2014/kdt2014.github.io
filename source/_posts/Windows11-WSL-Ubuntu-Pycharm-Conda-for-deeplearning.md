---
title: Windows11 + WSL Ubuntu + Pycharm + Conda for deeplearning
tags:
  - 教程
  - 深度学习
categories: 教程
copyright: true
description: Windows环境下使用Pycharm连接wsl ubuntu进行深度学习训练
abbrlink: 3c995b2a
date: 2023-03-22 19:56:16
update: 2023-03-22 19:56:16
---

## 目录
- 前言
- 安装wsl
- wsl安装anaconda并配置环境
- Pycharm连接wsl，并使用conda生成的环境



## 前言

通常来说在Linux系统下进行深度学习训练的效率要高于Windows系统，大家通常也是使用Linux常见的发行版本Ubuntu。但是Ubuntu对于日常使用不是很友好，于是就有了折中的方案，使用Windows Subsystem Linux (wsl)。

经过测试，在wsl中的训练效率相比Windows提升了大约25%。以下测试中均使用cuda118,唯一的区别是python版本两个是3.9，一个是3.10。

![Windows](https://s2.loli.net/2023/03/22/PQYkfEWDysUcCNZ.png "Windows_cu118_py39")

![ubuntu20](https://s2.loli.net/2023/03/22/ojpRTbrQJi4D1e8.png "ubuntu20.04_cu118_py39")

![ubuntu22](https://s2.loli.net/2023/03/22/O3Q95mYxHWcB1GT.png "ubuntu22.04_cu118_py310")

![interpreter](https://s2.loli.net/2023/03/22/oaiBn6FWzmxcbHf.png "Python Interpreter")

视频教程链接：[Bilibili](https://www.bilibili.com/video/BV1ok4y1t7XC/)，[Youtube](https://youtu.be/buyogP-KS5w)
## 安装wsl

这一部分参考之前的博客[windows 11安装wsl2，ROS以及窗口可视化](https://www.gongsunqi.xyz/posts/451c48f3/),只需要安装wsl2即可，安装ROS的部分不用理会。


## 配置cudatoolkit和cudnn

在Windows11自带的终端中打开上一步安装好的Ubuntu系统，之后的操作就和使用在Ubuntu主机上使用命令行完全一样。

![](https://s2.loli.net/2023/03/22/ZpNOkRvFwSu8K9H.png)


  wsl2和windows11共用显卡驱动，因此我们只需安装cudatoolkit和cudnn。以后windows显卡驱动正常更新即可。

  conda命令安装后虽然也可以用cudnn，但是不是完整版，不能编译。如果你需要编译功能，还是需要安装完整版本的cudatoolkit。

  1. 安装cudatoolkit

      可直接去官网下载所需版本：
      https://developer.nvidia.com/cuda-toolkit-archive
      我安装是11.8版本，因为pytorch官方的conda安装命令最高到11.8~版本对应安装，出问题的可能性最小。

      注意安装的时候选择wsl2版本安装！
      注意安装的时候选择wsl2版本安装！
      注意安装的时候选择wsl2版本安装！

      cuda11.8 wsl2 ubuntu版本的[安装链接](https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local)

      ![](https://s2.loli.net/2023/04/03/7anfJr9zVOxDkYP.png)

      将nvidia官方给的命令，一条条复制到wsl2的ternimal中即可。中间如果遇到问题百度帮到你~

      安装结束之后执行nvcc -v，会提示没有nvcc可执行，这并不是因为我们cudatoolkit没安装好，而是因为环境变量还没配置好。
    
  2. cuda环境变量配置

          sudo nano ~/.bashrc

      将以下内容添加进文件最后
    
         export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}
         export LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

      保存退出后（Ctrl+x），更新一下环境变量：

         source ~/.bashrc
      这时候在执行 nvcc -V 就能够显示cuda版本了。

  3. 安装cudnn

      严格来讲cuDNN不能叫安装。它其实是对CUDA的一些补充，所以“安装”过程很简单。去英伟达官网下载对应CUDA 11.8的cuDNN压缩包(这一步可能需要注册英伟达账号)。解压之后得到cuda目录，cuda目录下面有include和lib64两个子目录，将这两个目录下面的所有文件拷贝到CUDA 11.8安装路径对应的目录下面即可。

      [cudnn下载链接](https://developer.nvidia.com/rdp/cudnn-archive)

      ![](https://s2.loli.net/2023/04/03/kMSPFbJ2yG3a9TX.png)

      下载8.8.1 for cuda11.x

      将文件保存到windows环境，然后直接复制到wsl2 ubuntu的home目录下，和在windows环境中复制粘贴一样操作。

      在wsl的ternimal中进入到home目录，然后解压下载的文件

          sudo tar -xvf cudnn**    #省略部分按tab自动补全

      然后把解压得到的文件分别拷贝到对应的文件夹：

          #以下是安装命令     
         sudo cp -r /lib/* /usr/local/cuda-11.8（自己检查具体的版本修改路径）/lib64/
         sudo cp -r /include/* /usr/local/cuda-11.8（自己检查具体的版本修改路径）/include/
 
         #为更改读取权限：
         sudo chmod a+r /usr/local/cuda-11.8（自己检查具体的版本修改路径）/include/cudnn*
         sudo chmod a+r /usr/local/cuda-11.8（自己检查具体的版本修改路径）/lib64/libcudnn*

      注意操作要在相应的文件夹下进行哦！

   4. 检查cudnn是否安装成功

           cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2

        ![](https://s2.loli.net/2023/04/13/oe8AZIixlOPXpUc.png)
      

## wsl安装anaconda并配置环境


- 安装anaconda

[anaconda3官方下载](https://www.anaconda.com/products/distribution),选择linux版本，鼠标放在其上方右键，复制链接。

![](https://s2.loli.net/2023/03/22/9PVLksuX6BCxaU8.png)

回到Ubuntu的terminal，输入：

    wget https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh

运行以上代码，将会下载anaconda3到wsl ubuntu中。

![](https://s2.loli.net/2023/03/22/yemLhduQx1rHBGP.png)

之后执行：

    sh Anaconda3-2023.03-Linux-x86_64.sh

只需要输入 sh A 然后按Tab键，系统会自动补齐下面内容。

接下来就是安装过程，只需要根据提示按回车或者输入yes即可。

### conda配置环境

1. conda创建虚拟环境

        conda create --name cu118py310 python=3.10  #--name 后面是创建环境的名字，按自己的习惯命名，python=XX，输入自己想用的版本号
        conda activate cu118py310 #激活刚刚创建的环境

    ![conda env](https://s2.loli.net/2023/03/23/imlkrNDYjoqIObA.png "创建虚拟环境")

    ![activate](https://s2.loli.net/2023/03/23/3ZOdr5pcqtUivIB.png "激活环境")

    [常用的conda命令](https://blog.csdn.net/u014628771/article/details/80066624)


2. 配置pytorch

    前往[pytorch官网](https://pytorch.org/get-started/locally/)，选择需要的环境（注意这里选择linux OS），复制conda命令,在terminal中粘贴，回车，安装环境：

      ![](https://s2.loli.net/2023/03/22/VWK7jPvda2rwYsg.png)

        conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

      ![pytorch环境](https://s2.loli.net/2023/03/23/DSwiAanLlV98M3j.png "配置pytorch环境")




## Pycharm连接wsl，并使用conda生成的环境

Pycharm专业版（社区版和教育版没有方便的wsl功能,软件的下载链接在下面），点击右下选择添加新的Interpreter，操作如下图所示：

![wsl interpreter](https://s2.loli.net/2023/03/23/217LZ495MFT6GCu.png "add wsl interpreter")

选择自己创建的Linux_distribution，然后Next:

![](https://s2.loli.net/2023/03/23/VvnQa8Zr6qYkSPD.png)

Virtualenv Enviroment--Existing--点击...--选择这个路径 \\wsl$\Ubuntu-22.04\home\username\anaconda3\envs\cu118py310\bin\python3，Create。

![](https://s2.loli.net/2023/03/23/3r8Fdsbcv7elPZ2.png)

等待片刻，新的环境就配置好了。然后就可以使用这个环境训练跑起来！

软件百度网盘：链接：https://pan.baidu.com/s/1YkT8CiObO3v2Pnmmld2pqA?pwd=ci4h 
提取码：ci4h
Onedrive: https://1drv.ms/u/s!Arq4VGYuCz4AieNcw-nrj4XXtrugzQ?e=kmmVwH
