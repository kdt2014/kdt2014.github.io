---
title: Ubuntu实时内核PREEMPT_RT kernel 安装英伟达驱动和CUDA
tags:
  - ubuntu
  - kernal
  - linux
categories: linux
copyright: true
description: Ubuntu实时内核PREEMPT_RT kernel 安装英伟达驱动和CUDA
abbrlink: 5b4739c
date: 2023-08-28 11:31:45
update: 2023-08-28 11:31:45
---

## 前言

[上一篇文章](https://www.gongsunqi.xyz/posts/6fc37114/)介绍了Ubuntu如何编译安装实时内核PREEMPT_RT kernel。

由于英伟达官方的驱动并不支持实时内核，因此当我们用普通方式安装英伟达驱动时便会遇到错误。

这里将介绍为实时内核的Ubuntu系统安装英伟达驱动和CUDA的方法。

## 准备工作

一个全新安装的Ubuntu系统，已经按照[上一篇文章](https://www.gongsunqi.xyz/posts/6fc37114/)安装了实时内核，并且没有安装任何英伟达驱动。

也可以按照以下方法卸载已经安装的驱动，然后重启

    sudo apt-get --purge remove nvidia*
    sudo apt-get --purge remove "*cublas*" "cuda*"
    sudo apt-get --purge remove libnvidia*
    reboot

## 下载驱动 

从[CUDA Toolkit 12.0 Downloads](https://developer.nvidia.com/cuda-12-0-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)下载runfile文件到本地。

下载[cuDNN](https://developer.nvidia.com/rdp/cudnn-archive),我们选择Download cuDNN v8.9.2 (June 1st, 2023), for CUDA 12.x ---> Local Installer for Linux x86_64 (Tar)

![](https://s2.loli.net/2023/08/28/NeqS5y7PMpujoLv.png)

## 安装

1.安装runfile

    # 1. Stop X-Server
    sudo service lightdm stop

    # 2. Blacklist Nouveau driver
    sudo nano /etc/modprobe.d/blacklist-nouveau.conf

    # Insert into file:
    blacklist nouveau
    options nouveau modeset=0

    # 3. Update kernel initramfs
    sudo update-initramfs -u
    reboot  

    # 4. Install driver!
    sudo IGNORE_PREEMPT_RT_PRESENCE=1 bash <*>.run  # Insert downloaded .run file

    # 5. Reboot
    sudo reboot

 安装过程中会弹出来一个对话框，让你选择安装的内容，默认安装即可。

 安装结束之后执行nvcc -v，会提示没有nvcc可执行，这并不是因为我们cudatoolkit没安装好，而是因为环境变量还没配置好。

2.cuda环境变量配置

    sudo nano ~/.bashrc

  将以下内容添加进文件最后
    
    export PATH=/usr/local/cuda-12.0/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-12.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

  保存退出后（Ctrl+x），更新一下环境变量：

    source ~/.bashrc
  这时候在执行 nvcc -V 就能够显示cuda版本了。

3.安装cudnn

  严格来讲cuDNN不能叫安装。它其实是对CUDA的一些补充，所以“安装”过程很简单。去英伟达官网下载对应CUDA12.0的cuDNN压缩包(这一步可能需要注册英伟达账号)。解压之后得到cuda目录，cuda目录下面有include和lib64两个子目录，将这两个目录下面的所有文件拷贝到CUDA 12.0安装路径对应的目录下面即可。

    tar -xvf cudnn** 
    cd cudnn-linux-x86_64-8.9.3.28_cuda12-archive
    #以下是安装命令     
    sudo cp -r /lib/* /usr/local/cuda-12.0（自己检查具体的版本修改路径）/lib64/
    sudo cp -r /include/* /usr/local/cuda-12.0（自己检查具体的版本修改路径）/include/
 
    #为更改读取权限：
    sudo chmod a+r /usr/local/cuda-12.0（自己检查具体的版本修改路径）/include/cudnn*
    sudo chmod a+r /usr/local/cuda-12.0（自己检查具体的版本修改路径）/lib64/libcudnn*

  注意操作要在相应的文件夹下进行哦！

4.检查cudnn是否安装成功

   cat /usr/local/cuda-12.0/include/cudnn_version.h | grep CUDNN_MAJOR -A 2

  ![](https://s2.loli.net/2023/08/28/nH1v8lZyd3LcpM6.png)

## 检查

检查内核

    uname -r

检查cuda

    nvcc -V

检查nvidia驱动

    nvidia-smi

最后得到 

![](https://s2.loli.net/2023/08/28/Dum7YsZi2k48SN5.png)

