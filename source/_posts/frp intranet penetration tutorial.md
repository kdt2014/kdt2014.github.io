---
title: frp内网穿透教程，ssh远程连接
tags:
  - 网络
  - ssh
date: 2022-03-06 14:32:04
update: 2022-03-06 14:32:04
categories: 网络
copyright: true
description: frp内网穿透教程
---
# 前言
有时候我们需要从公网中远程连接自己的设备（SSH，远程桌面，远程文件等)，虽然诸如teamviewer和向日葵等可以较为方便的实现连接操作，但是网络不稳定，操作卡顿的现象却让我们十分难受。

[frp](https://github.com/fatedier/frp/blob/master/README_zh.md)内网穿透可以帮助我们实现自己的需求，它是一个专注于内网穿透的高性能的反向代理应用，支持 TCP、UDP、HTTP、HTTPS 等多种协议。可以将内网服务以安全、便捷的方式通过具有公网 IP 节点的中转暴露到公网。具体介绍请点开前面的链接查看官方文档。

先简单看一下技术原理，参见下图[1]：

![frp实现原理](https://s2.loli.net/2022/03/06/RuEgZyrfo4AjPB1.png)

图中VPS即是frps(service)，待远程连接的电脑就是frpc(client)。

我们需要借助一台VPS(虚拟主机)来完成中转任务。

# 准备工作
- 一台VPS(或者你有公网IP的实体主机)，可以参考之前的文章，[vultr新建虚拟主机](https://www.gongsunqi.xyz/2022/02/08/%E5%A6%82%E4%BD%95%E5%9C%A8IPV4%E7%BD%91%E7%BB%9C%E7%8E%AF%E5%A2%83%E4%B8%AD%E4%BD%BF%E7%94%A8IPV6%E7%BD%91%E7%BB%9C/#%E6%B3%A8%E5%86%8CIPV6%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BB%A3%E7%90%86%E5%95%86)
- 待远程连接的电脑

# VPS服务器端部署

假设你VPS上装的是Debian或者Ubuntu的64位系统，这里他俩并没有什么区别。

- 远程ssh连接上服务器
- 下载[frp](https://github.com/fatedier/frp/releases)到vps，执行以下命令：
      wget https://github.com/fatedier/frp/releases/download/v0.39.1/frp_0.39.1_linux_amd64.tar.gz
  ps:本教程更新时frp最新版本是V0.39.1，请点击前方连接到官网下载最新版
- 解压:
       tar -zxvf frp_0.39.1.0_linux_amd64.tar.gz
- 复制到新的frp文件夹： 
      cp -r frp_0.39.1.0_linux_amd64 frp
- 进入新目录：
      cd frp
- 查看文件
      ls -a
  里面会包含frps, frps.ini, frpc, frpc.ini 等文件

- 这里我们是部署服务器端，所以删除客户端client的文件：
      rm frpc
      rm frpc.ini

- 修改服务器端文件配置，打开frps.ini
      vim frps.ini
- 填写以下内容[1]：
      [common]
      bind_port = 7000
      dashboard_port = 7500
      token = mypwd
      dashboard_user = root
      dashboard_pwd = 123456
      vhost_http_port = 10080
      vhost_https_port = 10443

## 一些解释
1. “bind_port”表示用于客户端和服务端连接的端口，这个端口号我们之后在配置客户端的时候要用到。
2. “dashboard_port”是服务端仪表板的端口，若使用7500端口，在配置完成服务启动后可以通过浏览器访问 x.x.x.x:7500 （其中x.x.x.x为VPS的IP）查看frp服务运行信息。
3. “token”是用于客户端和服务端连接的口令，请自行设置并记录，稍后会用到。
4. dashboard_user”和“dashboard_pwd”表示打开仪表板页面登录的用户名和密码，自行设置即可。
5. vhost_http_port”和“vhost_https_port”用于反向代理HTTP主机时使用，本文不涉及HTTP协议，因而照抄或者删除这两条均可。

- 编辑完成后，保存退出。(vim的命令：先按Esc，然后英文状态下的 :  然后输入wq  (代表write和quit))。
- 开放防火墙端口
      sudo apt install firewalld
      sudo firewall-cmd --permanent --add-port=7000/tcp
      sudo firewall-cmd --permanent --add-port=7500/tcp
      sudo firewall-cmd --permanent --add-port=7001/tcp
      sudo firewall-cmd --reload

- 运行frps服务
      ./frps -c frps.ini

- 如果看到类似下面的内容，说明成功了：
      2022/03/06 15:22:39 [I] [service.go:130] frps tcp listen on 0.0.0.0:7000
      2022/03/06 15:22:39 [I] [service.go:172] http service listen on 0.0.0.0:10080
      2022/03/06 15:22:39 [I] [service.go:193] https service listen on 0.0.0.0:10443
      2022/03/06 15:22:39 [I] [service.go:216] Dashboard listen on 0.0.0.0:7500
      2022/03/06 15:22:39 [I] [root.go:210] Start frps success

这时访问x.x.x.x:7500 (x.x.x.x是你的VPS提供的IP) 并使用自己设置的用户名密码登录，即可看到仪表板界面。
![控制面板](https://s2.loli.net/2022/03/06/WvsryxcB6GAi9wN.png)

# 服务器端后台运行

如果此时我们关闭terminal，刚才运行的frps会自动结束，这时我们就需要把它挂在后台：

      nohup ./frps -c frps.ini &
关于这条指令的详细讲解，请参考[这里](https://ehlxr.me/2017/01/18/Linux-%E7%9A%84-nohup-%E5%91%BD%E4%BB%A4%E7%9A%84%E7%94%A8%E6%B3%95/)。

这时我们关闭terminal，仍然可以通过x.x.x.x:7500访问后台面板。

# 客户端部署

- 这一步用来设置需要被远程连接的设备，我们以Linux系统的电脑为例，还是同服务器端一样下载文件，解压，复制到新文件夹，然后删除frps和frps.ini。

- 打开 frpc.ini，编辑以下内容：

      [common]
      server_addr = x.x.x.x
      server_port = 7000
      token = mypwd
      [ssh]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 22
      remote_port = 6000 
      [ssh2]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 50000
      remote_port = 50000
      [ssh3]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 50001
      remote_port = 50002
      [rdp]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 3389
      remote_port = 7001  
      [smb]
      type = tcp
      local_ip = 127.0.0.1
      local_port = 445
      remote_port = 7002

  其中common字段下的三项是我们早先在服务器端设置的内容。
  如果我们只需要ssh服务，下面的rdp和smb内容可以不填写。
  如果需要一个服务器给多台设备提供frp服务，可以使用以上设置多个ssh。

- 运行服务
      ./frpc -c frpc.ini
- 后台挂起
      nohup ./frpc -c frpc.ini &

- Windows客户端使用

  在文章开头下载frp的网址下载对应的Windos版本，这里我们需要编辑client客户端的配置，即frpc.ini

      [common]
      server_addr = x.x.x.x
      server_port = 7000
      token = mypwd
      [ssh]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 22
      remote_port = 6000 
      [ssh2]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 50000
      remote_port = 50000
      [rdp]
      type = tcp
      local_ip = 127.0.0.1           
      local_port = 3389
      remote_port = 7001  
      [smb]
      type = tcp
      local_ip = 127.0.0.1
      local_port = 445
      remote_port = 7002

- 然后再写一个脚本启动服务start.bat：

      @echo off

      if "%1" == "h" goto begin
      mshta vbscript:createobject("wscript.shell").run("%~nx0 h",0)(window.close)&&exit
      :begin

        ## 这个替换成你自己的文件路径
      cd /d "D:\software\frp_0.39.1.0_windows_amd64"

      frpc -c frpc.ini

  之后每次重启电脑，需要开启frp服务，只需要双击执行这个脚本即可。

- 开机自启动
  上面的脚本可以在开机之后双击启动frpc服务，但是如果想每次开机时自启动该服务，则需要另外一个脚本来辅助。
  ps:笔者尝试将上文中的start.bat放入开机启动文件夹，但是会有报错。
  首先写一个start.bat脚本：

      @echo off
      frpc -c frpc.ini

  再写一个start.vbs脚本：

      CreateObject("WScript.Shell").Run "cmd /c D:\frp_0.45.0_windows_amd64\start.bat",0

  注意把文件中start.bat所在文件夹的路径替换成你自己的。

  建议将start.bat和start.vbs都放在你的frp文件夹内。

  然后在windows的组策略--计算机配置--windows设置--脚本（启动/关机）--启动--添加--选择start.vbs，然后应用--确定。
  
  ![](https://s2.loli.net/2022/11/16/JIh3sbaonEMH1vC.png)


## 一些解释
1. “[xxx]”表示一个规则名称，自己定义，便于查询即可。
2. “type”表示转发的协议类型，有TCP和UDP等选项可以选择，如有需要请自行查询frp手册。
3. “local_port”是本地应用的端口号，按照实际应用工作在本机的端口号填写即可。
4. “remote_port”是该条规则在服务端开放的端口号，自己填写并记录即可。

>RDP，即Remote Desktop 远程桌面，Windows的RDP默认端口是3389，协议为TCP，建议使用frp远程连接前，在局域网中测试好，能够成功连接后再使用frp穿透连接。

>SMB，即Windows文件共享所使用的协议，默认端口号445，协议TCP，本条规则可实现远程文件访问。


# 远程连接
- 远程连接的电脑是linux系统
Linux可以直接打开terminal，Windows可以使用ssh工具，比如putty或者MobaXterm，在命令行界面输入x.x.x.x:6000，这里的6000是你自己设置的端口，可以是任何你设置的数字，然后输入本地用户名和密码就可以成功连接。

- 远程连接的电脑是windows
可以直接使用windows电脑自带的远程连接工具，输入vps ip:远程端口，即可输入用户名和密码登录。例如，远程主机ip是1.2.3.4，frpc.ini中设置的remote_port = 7001，可以输入1.2.3.4:7001远程连接电脑。

如果待连接的电脑是笔记本电脑或者是使用wifi连接的设备，那么在你远程登录过程中，待连接电脑会自动锁屏，然后断掉wifi。。。。目前我还找到解决这个问题的办法，只能使用网线连接。

连接过程中可能出现的问题参考文章 [微软远程桌面登录](https://www.gongsunqi.xyz/2022/11/11/%E6%97%A0%E6%B3%95%E4%BD%BF%E7%94%A8%E5%BE%AE%E8%BD%AF%E8%B4%A6%E5%8F%B7%E7%99%BB%E5%BD%95%E8%BF%9C%E7%A8%8B%E6%A1%8C%E9%9D%A2/)


# Reference
- [1] https://sspai.com/post/52523/
