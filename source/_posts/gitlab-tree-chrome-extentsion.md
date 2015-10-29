title: gitlab-tree 更方便的浏览Gitlab上的代码
date: 2015-10-15 10:09:50
categories: myworks
---

## 说明
经常玩`Github`的人肯定都知道大名鼎鼎的[`octotree`](https://github.com/buunguyen/octotree)吧，这款chrome插件可以说是浏览代码的神器，利用左侧的树形菜单可以很方便的打开目录、浏览文件等，加上`Github`全站本身使用了`pjax`技术，基本全程无刷新，用户体验非常好。

本着`不要重新发明轮子`的原则，搜遍了整个互联网发现确实还没有一个可以在`gitlab`
上浏览代码的插件。
现阶段几乎每家用`git`管理源代码的公司都用上了配套的`gitlab`服务，一般都会部署在企业内网。而且，在`octotree`的`issue`里有好多老外也在`跪求`作者做一个`gitlab`版本的，但是作者貌似也没有这个打算。

![](http://images2015.cnblogs.com/blog/282019/201510/282019-20151029104304450-1035382532.jpg)

人们常说`不要重新发明轮子`, 可是别忘了这句`舶来语`后面还有一句：`Unless You Plan on Learning More About Wheels`


## 开发过程
根据自己定的需求，最终目的是制作一款chrome插件，可以在`gitlab`上浏览代码。为了做到对用户影响最小，这个插件不会占用chrome右上角、地址栏右侧的地方，只是会在页面中加载一段`js`探测是否属于gitlab服务，如果是的话，经过一系列初始化、调用`Gitlab API`以及`DOM 操作`之后，就会生成一棵代码树，可以清晰的查看目录结构。

![](https://raw.githubusercontent.com/FrankFan/gitlab-tree/master/docs/gitlab-tree.png)

技术方面没什么可说的，感兴趣的同学自己翻代码吧，`repo`在这里：[https://github.com/FrankFan/gitlab-tree](https://github.com/FrankFan/gitlab-tree)

欢迎下载使用，如果有问题可以[在这里](https://github.com/FrankFan/gitlab-tree/issues/new)告诉我，欢迎`fork`，一起改进完善， make it better.

## 发布
目前`gitlab-tree`已经更新到`v1.3`版本了，基本趋于稳定，后续还会继续完善。已经放在`chrom web store`上面了。对了，安装chrome插件需要拥有[翻~墙]技能。

[https://chrome.google.com/webstore/detail/gitlab-tree/dllpphhnoanpcnlnipopibigdoeignbb?hl=zh-CN](https://chrome.google.com/webstore/detail/gitlab-tree/dllpphhnoanpcnlnipopibigdoeignbb?hl=zh-CN)

