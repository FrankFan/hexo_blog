title: 手机Safari浏览器在隐私模式下使用本地存储localStorage问题
date: 2015-06-09 20:15:38
categories: javascript
---

开发H5 webapp时经常需要使用本地存储，如localStorage和sessionStorage存储一些数据，相比最多能存4k的cookie相比，用起来很好用。但是localStorage在iOS Safari、chrome和UC浏览器中的隐私模式（也叫无痕模式）下无法使用，手机Safari浏览器中具体表现是：

- localStorage对象仍然存在
- 但是setItem会报异常：QuotaExceededError
- getItem和removeItem直接忽略


Safari中控制台截图
![](http://images0.cnblogs.com/blog2015/282019/201506/092058146293230.png)

判断浏览器是否支持localStorage的方法:

```javascript
function isLocalStorageSupported() {
    var testKey = 'test',
        storage = window.sessionStorage;
    try {
        storage.setItem(testKey, 'testValue');
        storage.removeItem(testKey);
        return true;
    } catch (error) {
        return false;
    }
}
```

在实际项目中，需求如果非要坚持隐私模式也要支持的话，可以把数据写2遍，先写到localStorage中，再写到内存中。