title: 手机H5 web调试利器——WEINRE (WEb INspector REmote)
date: 2015-08-22 07:32:46
categories: javascript
---

调试移动端页面，优先选择使用chrome浏览器调试，如果是`hybrid`形式的页面，可以使用chrome提供的`chrome://inspect/#devices` 安卓真机调试，不过这个要求比较高：
首先，你的 Chrome 版本必须高于 32
其次你的测试机 Android 系统高于 4.0，
再其次，测试机安装 Chrome for Android 才可以使用 Chrome 远程调试这项功能，
最后， 手机需要开启`USB调试模式`


比如需要调试嵌入在APP中webView中的页面， 恰好安卓的版本比较低，没办法真机调试，
这时候`weinre`就是最好的选择。

## 如何使用 weinre

WEINRE 是 WEb INspector REmote 的缩写， 可以远程调试web页面。

### 安装

`$ sudo npm install -g weinre`
`$ weinre -v`

### 配置

获取本机IP：172.19.17.62
`$ ipconfig getifaddr en0`

开启本地监听服务器：
`weinre --boundHost 172.19.17.62`

![](http://images2015.cnblogs.com/blog/282019/201508/282019-20150828204957359-384833274.png)

打开`http://172.19.17.62:8080` ,

![](http://images2015.cnblogs.com/blog/282019/201508/282019-20150828205242469-1596822996.png)

将这段脚本放在需要调试的手机页面中就可以远程调试了，

`<script src="http://172.19.17.62:8080/target/target-script-min.js#anonymous"></script>`


加载好之后就可以在remote tab下找到需要调试的页面了， 和chrome devTools类似， 也可以查看DOM元素和控制台等。

![](http://images2015.cnblogs.com/blog/282019/201508/282019-20150828205740562-1922668759.png)