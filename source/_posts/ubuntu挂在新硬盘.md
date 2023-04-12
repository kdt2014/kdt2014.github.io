---
title: ubuntu挂载新硬盘到home目录下
tags:
  - linux
  - 教程
categories: 教程
copyright: true
description: ubuntu挂载新硬盘到home目录下
abbrlink: ffe6c5d4
date: 2023-04-12 19:56:45
update: 2023-04-12 19:56:45
---

1.查看所有硬盘信息(找到需要挂载硬盘的路径,如/dev/nvme1n1)


    sudo fdisk -lu

2.格式化硬盘

    sudo mkfs -t ext4 /dev/nvme1n1


3.创建挂载目录

    sudo mkdir /home/usrname/mydata

    chmod -R 777 /home/usrname/mydata
  
  username是你自己的用户名

4.手动挂载分区(nvme1n1:想要挂载的分区 mydata:分区挂载的目录)

    mount /dev/nvme1n1 /home/usrname/mydata

5.查看想要挂载分区的UUID

    sudo blkid /dev/nvme1n1

6.修改开机挂载文件

    sudo nano /etc/fstab    

7.文档末尾添加挂载信息

    # [分区UUID] [挂载目录] [分区格式] [默认配置] [开机不检查硬盘] [交换分区]
    UUID=1234-1234-1234 /home/usrname/mydata ext4 defaults 0 0

8.取消挂载

    umount /home/usrname/mydata

9.查看硬盘挂载情况

    sudo lsblk

    df -kh 
