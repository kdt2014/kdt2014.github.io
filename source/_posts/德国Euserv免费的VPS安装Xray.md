---
title: 德国Euserv免费的VPS安装Xray
date: 2021-08-08 19:48:57
update: 
tags:
- 网络
- vps
- 记录
- Xray
categories: 网络
copyright: true
description: 德国Euserv免费的VPS安装Xray
---

# 前言 #

放假在家的时候，没有IPV6环境，想通过北邮人下载一些需要的资源，但是又不想花钱买vultr的VPS（因为我没有扶墙的需求）。所以就琢磨着白嫖，哈哈哈，白嫖使我快乐，后来就发现了Euserv这个德国的VPS。

# 目录 #

1. 注册使用Euserv
2. ssh登录到远程主机
3. 安装Xray
4. 使用Qv2ray


## 注册使用Euserv ##

1. 注册[Euserv](https://www.euserv.com/en/register.php),注册时，信息可以如实填写，在国内的同学账户验证可能需要2-3天。有一说一，到德国的延时是真的高，网页半天才刷出来~~
2. 账户注册验证完成后，在这个界面[vs2-free](https://www.euserv.com/en/virtual-private-server/root-vserver/v2/vs2-free.php)订购一个免费的服务。这一步也是需要审核的，耐心等待，难道这就是德国人严谨的作风，interesting~
3. 再等个一天吧，审核通过。登录账户，login customer control panel。在Vserv中点击select，我们先点击reinstallation安装一个系统Debian10系统。系统装好后点击serverdata，就可以看到VPS的详细信息。包括远程登录使用的IP，root密码。
![](https://i.loli.net/2021/08/08/hVRvz1ISgYLWJZ9.png)
![](https://i.loli.net/2021/08/08/B8P6rSzxuMcnbjs.png)
![](https://i.loli.net/2021/08/08/SsWkYDa9j2gHcBz.png)

## ssh登录到远程主机 ##

因为我没有本地IPV6，所以只能给本地电脑添加IPV6隧道，然后再ssh连接到Euserv。如果你有本地IPV6，比如家里的宽度有，或者手机支持IPV6（国内电信联通移动这些运营商好像会提供），你可以直接远程连接。这里推荐[MobaXterm](https://mobaxterm.mobatek.net/)这款软件，免费且界面好看。比putty和Xshell都好用。

本地电脑添加IPV6隧道：

1. 以管理员权限打开windows终端：在windows图标上右键，选择“windows终端（管理员）”
2. 依次输入以下命令：

		netsh interface teredo set state enterpriseclient server=default
		netsh interface ipv6 reset
		netsh interface teredo set state server=teredo.remlab.net

3. 打开MobaXterm，建立ssh连接。端口默认22，用户root，密码和ip可以在Euserv的serverdata中找到。
4. 以后你可以通过以下命令关闭IPV6隧道（本教程中不需要执行这一条）：

		netsh interface Teredo set state disable

## 安装Xray ##

前提你得有一个自己的域名，没有的自己去买一个，或者找找免费的域名。然后参考这篇文章，设置一下[cloudflare](https://zhuanlan.zhihu.com/p/82909515)。

在开始之前在cloudflare上增加一个新的记录，如下图所示，名称你可以自己取，内容就是Euserv上的IPV6地址，代理状态先不打开：

![](https://i.loli.net/2021/08/08/q2M3X9LFlfij1em.png)


**当然，当然，**如果你和我一样懒，一样的财力不雄厚，也可以不搞cloudflare,直接去[godaddy](https://sso.godaddy.com/account/create?realm=idp&path=%2Fproducts&app=account)上面注册一个域名，选最便宜的一年才8块钱，等到期了再8块钱注册一个呗，可以使用PayPal付款，paypal可以绑定银联的借记卡。注册好自己的域名之后：我的产品---网域---点击右上角的三角符号---管理DNS--点击底部的加入---增加一个AAAA记录，参考下图:

![](https://i.loli.net/2021/08/09/AzuBxDEiQqP5yec.png)
![](https://i.loli.net/2021/08/09/VtJNO1Lgbahv8s4.png)


然后我们接着往下走，这一部分我参考的[这篇文章](https://trojanv2ray.blogspot.com/2020/12/VPSEuservXray.html)。

1. VPS设置IPV4访问。因为我们订购的那个免费主机是纯IPV6地址的，为了能访问Github下载文件，所以要设置VPS能访问IPV4地址。输入以下命令：

		echo -e "nameserver 2001:67c:2b0::4•\nnameserver 2001:67c:2b0::6" > /etc/resolv.conf

2. 安装curl:
		
		apt-get update -y && apt-get install curl -y

3. Xray一键安装代码:

		bash <(curl -sL https://s.hijk.art/xray.sh)

Cloudflare的CDN，目前只能使用websocket协议，XTLS不支持websocket协议,所以我们选择7,VLESS+WS+TLS这一个选项。
![](https://i.loli.net/2021/08/08/W31hYbA72FgzqfM.png)
安装的过程中**BBR加速选项选择no**，**BBR加速选项选择no**，**BBR加速选项选择no**，其余的可以都是默认。

安装到最后会报错，证书没获取。没关系，我们输入以下命令获取证书：

		bash /root/.acme.sh/acme.sh --issue -d 域名 --debug --standalone --keylength ec-256 --listen-v6  

**记得把“域名”这两个字换成自己的域名**。

如果到最后能看到 your cert is in 某某路径，说明安装成功了，然后再次运行刚才的一键安装脚本，重新安装一遍。

如果证书没有安装成功，试试下面的代码：

		apt-get install openssl cron socat curl   
		apt-get -y install netcat   

安装成功后执行 source ~/.bashrc 以确保脚本所设置的命令别名生效。然后再运行获取证书的命令，如果成功，就运行Xray一键安装代码。

我在安装证书的时候遇到了“tcp port 80 is alread used in nginx..."的错误，提示我先先关闭nginx。我使用下面的命令关闭：

		nginx -s quit  #此方式停止步骤是待nginx进程处理任务完毕进行停止

还有一些其他的命令放在这里(你不用输入的亲，我留着给自己以后参考）:

		1.start nginx  //启动nginx的命令。
		2.nginx -s quit  //此方式停止步骤是待nginx进程处理任务完毕进行停止。
		3.nginx -s stop  //此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
		4.nginx -s reload  //重新加载配置文件：当 nginx的配置文件 nginx.conf 修改后，要想让配置生效需要重启 nginx，使用-s reload不用先停止 nginx再启动 nginx 即可将配置信息在 nginx 中生效

4.Xray安装成功后，可以看到配置信息。

## 使用Qv2ray ##

把我截图中的红框里的内容换成自己的，就OK了。

主机和TLS下“服务器地址（SNI)”填写自己的域名。

需要特别说明的一个就是请求头那里是 Host|你的域名。其他的就是正常使用Qv2ray的方法。

![](https://i.loli.net/2021/08/08/ryMPJ1Y7xDTUwO9.png)
![](https://i.loli.net/2021/08/08/ldGCFqkUQyKi3En.png)

打开代理，看看自己是不是能上网了。如果不能，回到cloudflare里，把我们刚刚增加的那个记录的代理打开。也就是点击小云朵，让他变黄色~~~

# 致谢 #

本文属于自己参考多篇教程梳理总结的内容，建议配合[这个Youtube视频](https://www.youtube.com/watch?v=cfoh2j4fZcM)一起食用。		
