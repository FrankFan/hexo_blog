title: javascript中的事件揭秘
date: 2014-10-05 17:37:06
categories: javascript
---

## 介绍

Javascript中的事件可以和html交互。

事件流
**IE&Opera**：事件冒泡 
**其他** 浏览器： 事件捕获

**事件冒泡**：事件由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播至最不具体的那个节点（文档）。

**事件捕获**：不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。


## 事件处理程序

### HTML事件

缺点：
- HTML和js代码紧密的耦合在一起，
- 不利于扩展，
- 只能添加一个事件

### DOM0 级事件处理程序
把一个函数赋值给一个事件处理程序的属性。
可以添加多个事件处理程序。

### DOM2 级事件处理程序
DOM2级事件定义了2个方法：
用于处理指定和删除事件处理程序的操作：addEventListener() 和 removeEventListener()
都接收三个参数：要处理的事件名、作为事件处理程序的函数和布尔值（true：表示在事件捕获阶段调用事件处理程序 false：表示事件在事件冒泡阶段调用事件处理程序）。


```javascript
var btn3 = document.getElementById('btn3');
btn3.addEventListener('click', showMessage, false); // 添加事件

btn3.removeEventListener('click', showMessage, false); // 删除事件
```

### IE事件处理程序
attachEvent() 添加事件处理程序
detachEvent() 删除事件处理程序
都接收两个参数：事件处理程序名称和事件处理程序函数
不加第三个参数是因为IE8之前的浏览器只支持事件冒泡。
```javascript
btn3.attachEvent('onclick', showMessage); // 添加事件处理程序
btn3.detachEvent('onclick', showMessage); // 删除事件处理程序
```

### 跨浏览器事件处理程序
使用浏览器能力检测（Browser Compatibility）方法

封装方法：跨浏览器事件处理程序方法封装

```javascript 
var eventUtil = {
	// 添加句柄
	addHandler: function (element, type, handler) {
		if(element.addEventListener){ //DOM2级
			element.addEventListener(type, handler, false);
		}else if(element.attachEvent){ // DOM0级 IE
			element.attachEvent('on' + type, handler);
		}else{ // HTML事件
			element['on' + type] = handler;
		}
	},

	// 删除句柄
	removeHandler: function (element, type, handler) {
		if(element.removeEventListener){ //DOM2级
			element.removeEventListener(type, handler, false);
		}else if(element.detachEvent){ // DOM0级 IE
			element.detachEvent('on' + type, handler);
		}else{ // HTML事件
			element['on' + type] = null;
		}
	}
}
```

## DOM中的事件对象
在触发DOM上的事件时都会产生一个对象，叫做事件对象。

DOM事件对象event的属性：
### type属性
用于获取事件类型
如：`click`等

### target属性
用于获取事件目标
如：`target.nodeName`

### stopPropagation() 方法
用于阻止事件冒泡

### preventDefault() 方法
用于阻止事件的默认行为


## IE中的事件对象

### type 属性
用于获取事件类型

### srcElement 属性
用于获取事件目标
IE中没有e.target属性，而是 e.srcElement 属性。

所以，js中获取元素最兼容的写法是：
```javascript
e = event || window.event; // IE8之前使用window.event 传递事件
var element = e.target || e.srcElement;
```

### 3. cancelBubble 属性
用于阻止事件冒泡
```javascript
true：表示阻止事件冒泡
fales：表示不组织事件冒泡
```

### 4. returnValue 属性
用于阻止事件的默认行为
```javascript
false：表示阻止事件的默认行为
```

继续封装eventUtil

```javascript
var eventUtil = {
	// 添加句柄
	addHandler: function (element, type, handler) {
		if(element.addEventListener){ //DOM2级
			element.addEventListener(type, handler, false);
		}else if(element.attachEvent){ // DOM0级 IE
			element.attachEvent('on' + type, handler);
		}else{ // HTML事件
			element['on' + type] = handler;
		}
	},

	// 删除句柄
	removeHandler: function (element, type, handler) {
		if(element.removeEventListener){ //DOM2级
			element.removeEventListener(type, handler, false);
		}else if(element.detachEvent){ // DOM0级 IE
			element.detachEvent('on' + type, handler);
		}else{ // HTML事件
			element['on' + type] = null;
		}
	}，

	// 获取事件对象
	getEvent: function (event) {
		return event ? event : window.event;
	},

	// 获取事件类型
	getType: function (event) {
		return event.type;
	},

	// 获取事件目标对象
	getElement: function (event) {
		return event.target || event.srcElement;
	}

	// 阻止事件的默认行为
	preventDefault: function (event) {
		if (event.preventDefault) {
			event.preventDefaul();
		}else{
			event.returnValue = false;
		}
	},

	// 阻止冒泡
	stopPropagation: function (event) {
		if (event.stopPropagation) {
			event.stopPropagation();
		}else{
			event.cancelBubble = true;
		}
	}

}

```

