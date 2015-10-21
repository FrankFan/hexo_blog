title: 从快的线上callback hell代码说起
date: 2015-10-20 20:52:38
categories: javascript
---

## 概述

就像谈到闭包必须要说js变量作用域一样，谈到 promise 之前肯定要先说谈异步编程。一直以来， javascript 处理异步方式都是使用 callback 方式，对与写 javascript 的人来时候 callback 深入人心。比如只有前端经验没有后端经验的同学看到 java 代码可能会问『为什么readFile方法可以直接返回结果？为何不使用 callback 』

由于 javascript 的单线程性质，必须等待上一个事件执行完成才能处理下一步。传统解决 javascript 异步编程的方法就是使用 callback，比如这样：

```js
$(document).ready(function(){
    ajaxGet('/api/userinfo', function() {
        ajaxGet('/api/productList', function() {
            ajaxGet('/api/ads', function(result) {
                console.log('all done!');
            });
        });
    });
});
```

再比如这样：

![](http://images2015.cnblogs.com/blog/282019/201510/282019-20151020203443645-1667364741.jpg)

截止到2015年10月20日晚，[http://www.kuaidadi.com/assets/js/animate.js](http://www.kuaidadi.com/assets/js/animate.js)还可以访问。

『快的』用线上代码为我们生动的演示了什么叫`callback hell`——『回调地狱』。


## promise

Promise 字面上可以理解为『承诺』，即A调用B，B返回一个『承诺』给A，然后A就可以认为B给我返回结果的时候我就执行方案一了，反之没有得到结果就执行方案二。

上面这句话翻译为代码：

```js
var resB = B();
var runA = function() {
    resB.then(execPlan1, execPlan2);
}
runA();
```

Promise 是一种异步操作模式，表示一个异步操作的最终结果，返回的是一个 Promise 对象，由于是立即返回，所以可以采用同步操作的流程。 这个 Promise 对象有一个 then 方法，允许指定回调函数，在异步任务完成后调用。

比如上面『快的』的例子可以改写为这样：

```js
(new Promise(step1))
    .then(step2)
    .then(step3)
    .then(step4)
    .then(step5)
    .then(step6)
    .then(step7)
    .then(step8)
    .then(step9)
    .then(step10)
    .then(step11)
    .then(step12)
    .then(step13)
    .then(step14)
    .then(step15)
    .then(step16)
    .then(step17);
```

看，『横向的胖子』变的苗条了，看起来是不是更加可爱呢？

Promise有个一个规范叫做 [Promises/A+](https://github.com/promises-aplus/promises-spec),  有各种各样的第三方库遵循这个规范实现了 Promise/A+ 。 比如 [Q](https://github.com/kriskowal/q)、 [when](https://github.com/cujojs/when), jQuery 有个类似的方法叫 [Deferred。](http://api.jquery.com/category/deferred-object/) 


一个 Promise 对象的实例一般有三种状态：未完成（pending）、已完成（fulfilled）和失败（rejected）。

>这三种的状态的变化途径只有两个，且只能发生一次：从“未完成”到“已完成”，或者从“未完成”到“失败”。
>一旦当前状态变为“已完成”或“失败”，就意味着不会再发生状态变化了。

Promise对象的运行结果，最终只有两种。
>得到一个值，状态变为fulfilled
>抛出一个错误，状态变为rejected



## 参考阅读

> [JavaScript Promise启示录](http://www.alloyteam.com/2014/05/javascript-promise-mode/)
> [JavaScript Promise迷你书（中文版）](http://liubin.github.io/promises-book/)
> [JavaScript Promises](http://www.html5rocks.com/zh/tutorials/es6/promises/)
> [javascript.ruanyifeng.com](http://javascript.ruanyifeng.com/advanced/promise.html)
> [Promise/A+规范](http://segmentfault.com/a/1190000002452115)