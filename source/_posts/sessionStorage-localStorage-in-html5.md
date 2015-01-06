title: Html5中的sessionStorage和localStorage简介
date: 2014-12-15 13:59:33
categories: javascript
---

## 介绍

html5中的web storage包括2中存储方式：sessionStorage和localStorage.
`sessionStorage`用于本地存储一个会话(session)中的数据，这些数据只有在同一个会话中的页面才能访问，并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储，不过有时这恰恰是它的优点。

而`localStorage`是用于持久化的本地存储，除非主动删除，否则数据是永远不会过期的。

## web storage 和 cookie的区别
web storage的概念和cookie类似，区别是前者是为了更大存储容量设计的。cookie的大小是受限的，并且每次发起请求时cookie都会被发送到服务端，这样无形中浪费了带宽，另外，cookie还需要指定作用域，不可跨域调用。
除此之外，web storage拥有setItem、getItem、removeItem和clear等方法可以使用，不像cookie需要前端开发自己封装setCookie、getCookie等操作。

## h5 web storage浏览器兼容情况
```javascript
if (window.localStorage) {
	alert('浏览器支持localStorage');
}else{
	alert('浏览器不支持localStorage');
}

//或者
if (typeof(window.localStorage) == 'undefined') {
	alert('浏览器不支持localStorage');
}else{
	alert('浏览器支持localStorage');
};
```

## localStorage和sessionStorage操作
localStorage和sessionStorage都具有相同的操作方法，例如setItem、getItem和removeItem等

### setItem 存储value
```javascript
sessionStorage.setItem("key", "value")
localStorage.setItem("site", "fy98.com")
```

### getItem 获取value
```javascript
var value = sessionStorage.getItem("key")
var site = localStorage.getItem("site")
```

### removeItem 删除key
```javascript
sessionStorage.removeItem('key')
localStorage.removeItem('site')
```

### clear 清除所有的key/value
```javascript
sessionStorage.clear()
localStorage.clear()
```

### 其他操作方法 `.`和 `[]` 访问

web Storage不但可以用自身的setItem,getItem等方便存取，也可以像普通对象一样用点(.)操作符，及[]的方式进行数据存储，比如：
```javascript
var storage = window.localStorage;
storage.key1 = 'hello';
storage['key2'] = 'world';
console.log(storage.key1);
console.log(storage["key2"]);
```
其实只要理解web storage本质上就是`object`就可以了。

### 遍历 web storage
sessionStorage和localStorage提供的key()和length可以方便的实现存储的数据遍历，比如：
```javascript
var storage = window.localStorage;
storage.key1 = 'hello';
storage['key2'] = 'world';
var len = storage.length;
for (var i = 0; i < len; i++) {
	var key = storage.key(i);
	var value = storage.getItem(key);
	console.log(key + "=" + value);
};
```

## storage 事件
storage还提供了st候orage事件，当键值改变或者clear的时，就可以触发storage事件，如下面的代码就添加了一个storage事件改变的监听：
```javascript
if (window.addEventListener) {
	window.addEventListener("storage", handle_storage, false);
}else if (window.attachEvent) {
	window.attachEvent("onstorage", handle_storage);
};

function handle_storage(e){
	if(!e){
		e = window.event;
	}

	console.log('fire on storage');
}
```
