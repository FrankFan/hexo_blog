title: jquery bind、delegate、live、on的区别及联系
date: 2015-03-27 20:24:12
categories: javascript
---

## 概述
jquery提供了好几个API都可以实现事件绑定, 如 `delegate`, `live` , `bind` 等, 可是有没有疑惑这几个API之间有什么区别和联系呢？


其实 `.delegate, .live, .on`这三个都API可以事先事件绑定，只不过有一点稍微的不同点。他们属于jQuery不同时期的同一个功能的不同名称实现。如果jQ版本大于1.7，建议使用.on 可以保证向上兼容。查看jquery源码知道， jquery很多地方都是使用`on`处理事件绑定的。


## 分析

`delegate`
jquery1.4.2及其以上版本；

delegate() 为指定的元素（被选元素的子元素）添加一个或多个事件处理程序，
并规定当这些事件发生时运行的函数。
使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）

`bind`
适用所有版本，但是根据官网解释，自从jquery1.7版本以后bind()函数推荐用on()来代替。

bind()向匹配元素添加一个或多个事件处理器。

`live`
jquery1.9版本以下支持，jquery1.9及其以上版本删除了此方法，jquery1.9以上版本用on()方法来代替。

live() 向当前或未来的匹配元素添加一个或多个事件处理器

`on`
jquery1.7及其以上版本；jquery1.7版本出现之后用于替代bind()，live()绑定事件方式；

on() 为指定的元素,添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数。使用 on() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。


## 区别及联系

### 相同点：

1.都支持单元素多事件的绑定；空格相隔方式或者大括号替代方式;
2.均是通过事件冒泡方式，将事件传递到document进行事件的响应；

###不同点：

1.bind()函数只能针对已经存在的元素进行事件的设置；但是live(),on(),delegate()均支持未来新添加元素的事件设置

2.bind()函数在jquery1.7版本以前比较受推崇，1.7版本出来之后，官方已经不推荐用bind()，替代函数为on(),这也是1.7版本新添加的函数，同样，可以用来代替live()函数，live()函数在1.9版本已经删除；

3.live()函数和delegate()函数两者类似，但是live()函数在执行速度，灵活性和CSS选择器支持方面较delegate()差些，想了解具体情况

4.bind()支持Jquery所有版本；live()支持jquery1.8-；delegate()支持jquery1.4.2+；on()支持jquery1.7+；


## 事件绑定方式

.bind()是直接绑定在元素上
.live()则是通过冒泡的方式来绑定到元素上的。更适合列表类型的，绑定到document DOM节点上。和.bind()的优势是支持动态数据。
.delegate()则是更精确的小范围使用事件代理，性能优于.live()
.on()则是最新的1.9版本整合了之前的三种方式的新事件绑定机制


## 取消事件绑定

`delegate` 对应 `undelegate`
`live` 对应 `die`
`bind` 对应 `unbind`
`on`  对应 `off`

具体用法参考[jQuery手册](http://hemin.cn/jq/)


参考
[http://www.cnblogs.com/xilipu31/p/4105794.html](http://www.cnblogs.com/xilipu31/p/4105794.html)
[http://blog.csdn.net/panfang/article/details/21705681](http://blog.csdn.net/panfang/article/details/21705681)