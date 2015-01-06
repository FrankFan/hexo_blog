title: CoffeeScript简介 <二>
date: 2014-10-09 22:47:46
categories: javascript
---

## 集合与迭代

### `..` 与 `...`

先看例子：
```javascript
arr = ["a1", "a2", "a3", "a4", "a5"]
arr[0..3] // ["a1", "a2", "a3", "a4"]
arr[-2..] // ["a4", "a5"]
arr[-3..3] // ["a3", "a4"]
arrRange = [1..5]//[1,2,3,4,5]
```

`..`包含右边区间。

```javascript
arr = ["a1", "a2", "a3", "a4", "a5"]
arr[0...3] // ["a1", "a2", "a3"]
arr[-2...] // ["a4", "a5"]
arr[-3...3] // ["a3"]
arrRange = [1...5]//[1,2,3,4]
```
`...`不包含右边区间。

### 遍历

**数组**

`arr = ["one", "two", "three", "four", "five"]`

基本遍历：
```javascript
console.log item for item in arr
```

加条件：
```javascript
console.log item for item in arr when item isnt "two"
```

带索引：
```javascript
console.log item for item,i in arr when i isnt 2
```

带循环项：
```javascript
[1,5].map (i) -> console.log i*2 // 也可以用带索引的for循环
```

**对象**
```javascript
obj = {a1: "a111", a2: "a222"}
console.log k,v for k,v of obj
```

### 循环
**单行**
```javascript
console.log i for i in [0..5]
```

**多行**
```javascript
for i in [0..5]
	console.log i
```

### 条件语句

**基本语法**
```javascript
eat food if cat is hungry
play game unless cat is hungry
play game if cat isnt hungry
```
生成`js`代码为：
```javascript
if (cat === hungry) {
  eat(food);
}

if (cat !== hungry) {
  play(game);
}

if (cat !== hungry) {
  play(game);
}
```
代码确实精简不少。


## OO篇
使用coffeeScript实现面向对象写起来很爽。

### 类定义

```javascript
class Animal
    constructor: (name) ->
		@name = name
    sayhello: () ->
		console.log @name
animal = new Animal('ray')
animal.sayhello()
```

生成的`js`代码为：
```javascript
var Animal, animal;
Animal = (function() {
  function Animal(name) {}
  return Animal;
})();

this.name = name({
  sayhello: function() {}
});

console.log(this.name);
animal = new Animal('ray');
animal.sayhello();
```

### 继承
```javascript
class Animal
  constructor: (name) ->
    @name = name
  sayhello: () ->
    console.log @name
class Cat extends Animal
  constructor:(name,@hungry) ->
    super
```

## `CoffeeScript` 与 `jQuery`
```javascript
$(function(){})
  |
  |
$ ->
```

比如：
```javascript
$(function() {
	$('h1').click(function() {
		$(this).html('I am clicked');
	});
});
  |
  |
$ -> 
	$('h1').click -> 
		$(@).html 'I am clicked'
```

## `Require` 与 `Backbone`
```javascript
define [
  'backbone'
  'underscore'
  'text!templates/yes.html'
], (Bacbone, _, tpl) ->

  class UserView extends Backbone.View

    events: {}

    initialize: (options)->

    render: ->
      @$el.html _.template( tpl, {  } )
```

## 其他
### 对象判空
`console?.log? 'log'`

```javascript
if (typeof console !== "undefined" && console !== null) {
	if (typeof console.log === "function") {
		console.log('log');
	}
}
```

### 关于 `->` 和 `=>` 号

```javascript
cat = ->
  console.log this
cat = =>
  console.log @
```

```javascript
# ->的结果
var cat;
cat = function() {
  return console.log(this);
};
# => 的结果
cat = (function(_this) {
  return function() {
    return console.log(_this);
  };
})(this);
```

也就是说：`=>`（胖头号）可以直接获取父级作用域中的`this`关键字。

### 最后
![](http://images.cnitblog.com/blog/282019/201410/092151423279522)
