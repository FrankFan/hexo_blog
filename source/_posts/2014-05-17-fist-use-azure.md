title: 初次使用Microsoft Azure
date: 2014-05-17 23:37:35
categories: 其他
---
## 一、介绍

在[微博][2]上偶然发现微软的Azure有免费申请试用的机会，于是赶快给微软发邮件申请，第二天就通过了。

![][1]

早就听说过微软在云计算方面发力，但一直没机会试用，之前用过国产的BAE、SAE，用GoAgent翻墙时也了解过GAE，提供一个类似虚拟空间的东西，但是微软Azure还可以建立虚拟主机，Windows、Linux都有。

![][3]

## 二、创建Ubuntu虚拟主机并用SSH连接
创建虚拟机很简单，根据提示一步一步来就可以了。
关键是使用SSH客户端连接Azure上的Ubuntu费了一些时间，特此记录。

进入虚拟机面板，切换到端口(PORT) tab 页，确保SSH协议的22端口是开放的；

![][4]

然后进入仪表盘面板，看下SSH详细信息

![][5]

##三、SSH客户端
最简单是SSH客户端就是PUTTY了，这里是[官方下载地址][6]。

![][7]

要注意：如果在创建虚拟机的时候没有指定过登录名，Azure默认的名字是**azureuser**，奇怪的是没有任何文档说明，这个地方浪费了不少时间，最后还是在[这篇文章的评论][8]中发现的。

ssh远程登录命令：
```bash
ssh -l azureuser yourIP
```

到这里就可以顺利的连上远程虚拟机Ubuntu了，接下来好玩的东西再慢慢发掘吧。


  [1]: http://images.cnitblog.com/other/282019/201405/172255547185397
  [2]: http://weibo.com/2552080342/B4JpDyaX9
  [3]: http://images.cnitblog.com/other/282019/201405/172303546567553
  [4]: http://images.cnitblog.com/other/282019/201405/172308179063378
  [5]: http://images.cnitblog.com/other/282019/201405/172310558122553
  [6]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
  [7]: http://images.cnitblog.com/other/282019/201405/172316100004671
  [8]: http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-how-to-log-on/