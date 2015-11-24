title: 前端的题
date: 2015-01-09 22:54:36
categories: 前端
---


## HTML/CSS 相关

1. 一道页面布局题
    有个web页面，分为左右结构，左边是一张宽度固定的图片；右边是一个宽度自适应的div，div中有很多其他元素从上到下依次排列。要写出html和css
    > 我用的float进行布局，但是这样是有问题的，右侧盒子宽度100%就没办法自适应了。
    正确的做法用`Flexbox弹性盒子`布局
    
    这个弹性盒子是CSS3的新特性，之前看到过没有深入研究，感觉还不太成熟，好多浏览器支持的也不是很好，可是如果是移动端使用还是比较适合的，之后再研究下吧

2. 如何看出是html4还是html5 ?
> 通过html第一行的`doctype`来区分
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<!DOCTYPE HTML>
```


## Javascript 相关
1. 输出终端运行结果
    ```javascript
    var i, j, obj=[];
    
    for(i = 0; i < 10; i++){
    	var tempFunc = function(){
    		console.log(i);
    	}
    	obj.push(tempFunc);
    }
    
    for(j = 0; j < 10; j++){
    	obj[j]();
    }
    ```
正确结果是输出10个10，算是考察闭包吧。
    ![](http://images.cnitblog.com/blog/282019/201501/100050486871889)

2. js数据类型
说出`null`、`undefined`和`NaN`的区别

>`null` 是对象类型，因为typeof(null)返回`object`
`undefined`是值类型， typeof(undefined)返回 `undefined`
`NaN`是window对象的一个全局属性，typeof(NaN)返回`number`，所以它是简单类型。

3. 输出终端运行结果
    ```javascript
    console.log('1');
    setTimeout(function(){
    	console.log('2');
    }, 0)
    console.log('3');
    ```

> 输出 1,3,2 而不是1,2,3 因为setTimeout会不论第二个参数是不是0都会放到程序最后执行

![](http://images.cnitblog.com/blog/282019/201501/100051337659883)

4. 说说对`promise`的理解
    这个理解的就是很深刻，项目中没有用到过，但是部门分享@lp有提到过。稍后深入研究一下。
参考资料：[http://www.infoq.com/cn/news/2011/09/js-promise/](http://www.infoq.com/cn/news/2011/09/js-promise/)

5. requirejs 如何加载非模块化js类库 ?
首先需要会手动配置require js，(`paths`)然后遇到非模块化的问题使用`shim方式`配置。


## 前端工作流
grunt + bower + yeoman + CI(持续集成) 打包等自动化流程

