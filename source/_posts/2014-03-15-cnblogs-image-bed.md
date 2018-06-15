title: 自制小工具含源码——博客园图床ImageBed
date: 2014-03-15 23:01:34
categories: myworks
---

本文介绍一款小工具：博客园图床的开发过程

<!-- more -->

## 说明
俗话说：好记性不如烂笔头。工作中会遇到各种各样的需求，各种各样的任务，可能当时完成了，但过一段时间回头看发现连自己都不知道当初写的代码是啥意思。大脑是用来思考的，不是用来存储记忆的。所以要经常记录一下自己的想法，以免过一段时间淡忘。

我最喜欢的习作方式是简单的文本编辑器，加上简单的可以格式化文本的代码，再配上几张精美的图片效果就perfect了。Markdown好像天生就是为这个需求而生的，美中不足的是在Sublime Text或者Notepad++中写的时候插入配图需要提供url，也就是需要一个可以存储图片的、稳定的、可以提供图片外链的服务。寻寻觅觅，寻寻觅觅发现一些云存储厂商（如七牛云存储）提供限量的免费空间、每个月限量的请求次数，要求不少，pass掉。

每天使用频率最高的网站就是cnblogs博客园，使用博客园发布文章时发现上传图片功能很好用：

- 支持常见的多种图片格式
- 上传速度快
- 支持10M一下图片
- 服务稳定（阿里云，分析Url用的貌似是又拍云存储图片服务）

唯一的缺点就是必须要求登录，于是就萌生一个想法：做一个图片上传小工具。

## 需求
目前基本功能是图片上传，然后获得图片的url地址。对，听起来就这么简单。

从技术角度来讲，需要克服的难点：

- Http抓包分析
- 模拟登录博客园
- 代码实现图片上传

要做一个小工具，能在windows平台运行，首选用C#开发Winform Application，在宇宙最强IDE——Visual Studio的帮助下开发效率最高了。

## 开发
开发详细过程就不写了，只写重点。

重点1：界面设计

![][1]

界面设计如图，左右2个panel，左边是登录信息，登录成功后跳转到右侧图片上传界面，登录隐藏。

![][2]

登录之前如上图，登录成功如下图：

![][3]

只要选择想要上传的图片，点击上传按钮，接着在下方文本框中就能得到想要的图片外链地址。

重点2：HTTP抓包分析

![][4]

这就是博客园图片上传主界面，上传一张图片用Http分析工具（用chrome develop tool就行，Fiddler有杀鸡用牛刀的感觉）跟踪一下Http请求，找到最关键的一条：

![][5]

请求的最终Url是：
> http://upload.cnblogs.com/imageuploader/processupload?host={0}&qqfile={1}

## 项目结构
![][6]

涉及到：

* 模拟Http请求，携带Cookie的Get和Post请求
* 对服务器返回的json对象反序列化
* 方法封装，一个函数只做一件事

源代码放在Github上，地址 [https://github.com/FrankFan/CnblogsImageBed](https://github.com/FrankFan/CnblogsImageBed)
欢迎拍砖。

当然你可以下载 [exe文件](https://github.com/FrankFan/CnblogsImageBed/releases/download/v2.0/CnblogsImageBed.exe) 使用博客园账号登录即可使用，你值得拥有 ：)

## 最后
当然，这篇文章中的图片都是来自这个小工具哦~ ：） <br />
P.S. 希望dudu看到了不会介意，毕竟这个小工具使用者不多，不会对博客园造成压力的，而且还会增加注册量哦~ ：）


[1]: http://images.cnitblog.com/other/282019/201403/151439438553796
[2]: http://images.cnitblog.com/other/282019/201403/151442576052938
[3]: http://images.cnitblog.com/other/282019/201403/151444083246499
[4]: http://images.cnitblog.com/other/282019/201403/151448179803028
[5]: http://images.cnitblog.com/other/282019/201403/200025517407526
[6]: http://images.cnitblog.com/other/282019/201403/151506322931344

