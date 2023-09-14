---
title: Ubuntu18.04上安装AX210驱动
tags:
  - linux
  - 教程
categories: Linux
copyright: true
description: Ubuntu18.04上安装AX210驱动
abbrlink: 79edb564
date: 2023-02-02 22:23:52
update: 2023-02-02 22:23:52
---

Intel 官网给出了在Linux下AX210所需要的最低环境：linux内核5.10+，而Ubuntu18.04内核版本为5.4，不符合要求。可以通过升级内核的方式安装，但存在较大的风险。因此选择不升级内核的方法进行驱动的安装。

**关闭主板security boot**
**关闭主板security boot**
**关闭主板security boot**

安装步骤：

- 更新软件列表

      sudo apt update
  
- 安装必要的包

      sudo apt install flex bison

- 下载backport仓库

      git clone https://github.com/intel/backport-iwlwifi.git
      cd backport-iwlwifi

- 进入iwlwifi-stack-dev文件并编译

      cd iwlwifi-stack-dev
      sudo make defconfig-iwlwifi-public
      sudo make
      sudo make install

    执行安装之后重启系统。

- 下载驱动文件

      git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
      cd linux-firmware/
      sudo cp iwlwifi-* /lib/firmware

- Load the iwlwifi module by running the following command

      sudo modprobe iwlwifi

- Verify that the Wi-Fi device is recognized by running the following command:

      lspci | grep Wireless


    这时设置里WiFi应该就可以使用了。但是这种方式蓝牙依然无效。