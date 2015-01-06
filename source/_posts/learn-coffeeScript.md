title: CoffeeScript简介 <一>
date: 2014-10-06 23:45:10
categories: javascript
---
## 介绍
coffeeScript是一种轻量级的编程语言，可以用编译器生成原生javascript代码。它简化了许多javascript繁琐的方式，可以让你用简单的方式直接使用一行程序代表javascript多行代码，而且编译后还会根据`最佳实践`优化javascript代码。它的语法像是`python`和`ruby`的混合，不用括号控制排版，直接用缩进表示。建议初学者一边写`coffeescript`，一边对照生成的`javascript`代码，可以很快的了解`coffeescript`的意义。 浏览器最后执行的还是编译后的`javascript`代码。

## 语法

### 去掉多余的符号＆＆使用缩进
首先来看一个 `coffeescript` demo：
```javascript
if elvis
  alert "oh no"
  elvis = 3
```
编译成 `javascript` 代码之后：
```javascript
if (elvis){
  alert("oh no");
  elvis = 3;
}
```
看上面的coffee代码和js代码，js中的圆括号被去掉了，画括号也去掉了，分号`;`也去掉了。

再比如：
```javascript
if elvis
  alert "oh no"
elvis = 3
```
编译成 `javascript` 代码之后：
```javascript
if (elvis){
  alert("oh no");
}
elvis = 3;
```
最后一句代码缩进方式不同，导致最终编译的js也不一样，coffee就是根据`tab缩进`来进行排版的。

### 函数
声明函数时coffee默认会把最后一行作为函数的返回值，可以不加`return`，如果返回值为空，可以加上`return`。

例如：
```javascript
fill = (x) ->
  x * x
```
编译后的js为：
```javascript
var fill;
fill = function(x)｛
  return x * x;
｝
```

### 字符串占位符
这是coffe中最爱的一点，因为javascript中没有类似`c#`中的`string.Format()`方法，拼接很长的字符串时代码看起来可读性很差。
```javascript
# 这是cofee的注释
eat = (x) -> alert "I eat #{x}!"
eat food for food in ['toast', 'cheese', 'wine']
```
编译后的js代码：
```javascript
var eat, food, _i, _len, _ref;

eat = function(x) {
  return alert("I eat " + x + "!");
};

_ref = ['toast', 'cheese', 'wine'];
for (_i = 0, _len = _ref.length; _i < _len; _i++) {
  food = _ref[_i];
  eat(food);
}
```
这里可以看出来使用coffee有多省事了吧。

### 区间使用
coffee有一个像java一样的`...`的语法：
```javascript
# ... 表示区间
numbers = [0,1,2,3,4,5,6,7,8,9]
copy = numbers[0...numbers.length]
middle = numbers[3...6]
```

### 关于 `==` 和 `!=` 之间的比较
在coffee中没有`==`，一律使用`===`，所以也就没有`!=`，只有`!==`。javascript中`==`和`===`的区别是：
> 三等操作符`===`用来判断两个变量是否相等，相等的前提是同样的类型和同样的值。

具体请参考我的[另一篇文章](http://fy98.com/2014/10/04/learn-javascript/)。

### 对象判空
coffee可以使用`?`来判断参数是否已定义或是`null`值，例如：
```javascript
if elvis?
  alert "oh no"
  elvis = 3
```
编译后的js代码：
```javascript
var elvis;

if (typeof elvis !== "undefined" && elvis !== null) {
  alert("oh no");
  elvis = 3;
}
```
