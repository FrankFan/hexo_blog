title: 利用useragent判断移动设备
date: 2014-06-30 22:34:02
categories: javascript
---

## 利用 User Agent 判断移动设备

## 说明
WebApp除了做成响应式设计以外，还可以给移动设备做一套UI，PC端再做一套UI，然后在前台进行判断进行相应的跳转。判断是否是移动设备一般根据浏览器的useragent进行判断，虽然可以伪造，但是用起来方便，和Chrome的设备模拟功能配合起来
调试方便。

## 代码
```javascript
//根据useragnet判断是否是移动设备
function isMobileDevice(ua) {
    if (/(iphone|ios|android|mini|mobile|mobi|Nokia|Symbian|iPod|iPad|Windows\s+Phone|MQQBrowser|wp7|wp8|UCBrowser7|UCWEB|360\s+Aphone\s+Browser)/i.test(ua)) {
        return true;
    }
    return false;
}
```

## chrome模拟手机
F12调出开发者工具，可以模拟各种手机的useragent，注意有些细节和真是手机上还是有区别的，只能做参考。
![](https://ws4.sinaimg.cn/large/006tNc79gy1fsbynqn7xtj30ty0legsk.jpg)