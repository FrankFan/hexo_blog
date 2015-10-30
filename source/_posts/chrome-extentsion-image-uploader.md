title: 开源一个图床工具 - image-uploader
date: 2015-10-03 12:33:35
categories: myworks
---


## 说明

去年做了一款 windows 下的图片上传程序，【[自制小工具含源码——博客园图床ImageBed](http://fy98.com/2014/03/15/2014-03-15-cnblogs-image-bed/)】, 但是这个小工具只适用于 windows 平台，自从换了 Mac 以后就不能用了。于是萌生了再写一款的念头。

我理想中的软件应该是这样的：

* 绿色免安装
* 简单易用，最好是傻瓜式操作
* 跨平台，最好windows、*nix都能用


用chrome extention 来做，刚好符合上述几点要求。

于是就有了下面的这个插件：

![](http://images2015.cnblogs.com/blog/282019/201510/282019-20151030124148888-2018701784.jpg)

简单说就是可以将你本地的一张图片上传到博客园的图片服务器上，变成一个可访问的url。适用于写markdown文件时插入图片的情况。
为什么要用博客园当图床呢？

- 因为我用博客园写了好几年的博客，有感情了
- 博客园的访问速度非常快，上传速度也快
- 图片外链没有限制，可以随意使用


使用方法很简单，点击`img-uploader`的`icon图标`，会打开一个新的页面，此时程序会判断你在博客园cnblogs.com的登录状态，如果没有登录，会提示用户先去博客园进行登录操作;

![](http://images2015.cnblogs.com/blog/282019/201510/282019-20151030113440794-1642761159.jpg)

如果检测到你在博客园是登录状态，就可以上传图片：：

![](http://images2015.cnblogs.com/blog/282019/201510/282019-20151030113445997-414524488.jpg)

支持拖拽操作上传操作，还可以直接复制上传后图片的url。

## 源代码

这个应用的源代码托管在`GitHub`上，欢迎大家 `star and fork`, 多提建议。

[https://github.com/FrankFan/img-uploader](https://github.com/FrankFan/img-uploader)

## 安装

我已经把这个插件在 chrome web store 上发布了，安装地址（需~翻~墙）：

[https://chrome.google.com/webstore/detail/image-uploader/ncdoclefjnhbjnbcdpekmmgmgbdodklo?hl=zh-CN](https://chrome.google.com/webstore/detail/image-uploader/ncdoclefjnhbjnbcdpekmmgmgbdodklo?hl=zh-CN)
