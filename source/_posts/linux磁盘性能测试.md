---
title: linux磁盘性能测试
tags:
  - linux
categories: linux
copyright: true
description: linux磁盘性能测试
abbrlink: f8cc8ef6
date: 2023-04-13 21:52:31
update: 2023-04-13 21:52:31
---

## 工具

安装fio

    sudo apt install fio

## 性能测试

随机读4k Q1T1，即随机读取4K大小的数据，队列深度1，线程1

    fio -filename=/tmp/test_randread -direct=1 -iodepth 1 -thread  -rw=randread  -ioengine=psync -bs=4k -size=2G -numjobs=1 -runtime=60 -group_reporting -name=mytest

其中-filename=/tmp/test_randread 为我们要测试的文件的路径以及名称，tem是根目录下的一个文件夹，test_randread是我们测试过程中会生产的一个文件，不用管它。如果我们有多块硬盘要测试，比如我的根目录安装在傲腾905p中，同时一块970evoplus挂载在home的mydata文件下。如果我想测试970evo plus的性能，只需要执行下面的命令：

    fio -filename=/home/username/mydata/test_randread -direct=1 -iodepth 1 -thread  -rw=randread  -ioengine=psync -bs=4k -size=2G -numjobs=1 -runtime=60 -group_reporting -name=mytest

随机写4k：

    fio -filename=/home/username/Documents/test_randwrite -direct=1 -iodepth 1 -thread -rw=randwrite -ioengine=psync -bs=4k -size=2G -numjobs=1 -runtime=60 -group_reporting -name=mytest

这里建议在测试写性能的时候尽量不要是装系统的根目录分区，而是使用home分区。

顺序读：

    fio -filename=/home/username/Documents/seq_read -direct=1 -iodepth 1 -thread -rw=read -ioengine=psync -bs=16k -size=2G -numjobs=10 -runtime=60 -group_reporting -name=mytest

顺序写：

    fio -filename=/home/username/Documents/seq_write -direct=1 -iodepth 1 -thread -rw=write -ioengine=psync -bs=16k -size=2G -numjobs=10 -runtime=60 -group_reporting -name=mytest

混合随机读写：

    fio -filename=/home/username/Documents/read_write -direct=1 -iodepth 1 -thread -rw=randrw -rwmixread=70 -ioengine=psync -bs=16k -size=2G -numjobs=10 -runtime=60 -group_reporting -name=mytest -ioscheduler=noop