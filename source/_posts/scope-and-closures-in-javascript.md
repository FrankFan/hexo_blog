title: js作用域和闭包
date: 2015-01-15 23:13:34
categories: javascript
---

## Javascript作用域概要
在Javascript中，作用域是执行代码的上下文。作用域有三种类型，`全局作用域`、`局部作用域`（有时也称作“函数作用域”）和`eval作用域`。

在函数内部使用`var`关键字定义变量，其作用域是局部的，且只对该函数的其他表达式是“可见的”，包括嵌套/子函数中的代码。在全局作用域内定义的变量从任何地方都可以访问，因为它是作用域链中的最高层/最后一个。

如下代码演示由于受作用域的影响，`foo`的每个生命都是独一无二的。

```javascript
var foo = 0; // global scope
console.log(foo); // output 0

var myFunction = function(){
	var foo = 1; // local scope
	console.log(foo); // output 1

	var myNestedFunction = function(){
		var foo = 2; // local scope
		console.log(foo); // output 2
	}();
}();

eval('var foo = 3; console.log(foo);'); // eval 作用域 output 3

```

注意：
> * 可以创建无数的函数作用域和eval作用域，而Javascript环境只使用一个全局作用域。
> * 全局作用域是作用域链中的最后一层。
> * 包含函数的函数，会创建堆栈执行作用域，这些链接在一起的栈通常被称为`作用域链`。


## Javascript没有块级作用域
由于逻辑语句（如if(){}）和循环语句（如for）无法创建作用域，因此变量可以互相覆盖。查看如下代码，并了解foo值被重新定义为执行代码的程序。

```javascript
var foo = 1;

if(true){
	foo = 2;
	for(var i = 3; i <= 5; i++){
		foo = i;  // foo 等于3、4，然后等于5
		console.log(foo); // output 3, 4, 5
	}
}
```

因此，代码执行时foo是变化的，因为Javascript根本没有块级作用域，只有函数、全局和eval作用域。

## 在函数中用var声明变量，避免作用域陷阱
Javascript会将缺少var的变量声明（即便是在函数或者封装的函数中）声明在全局作用域中，而非局部作用域。查看如下代码，请注意，如果不使用var来声明bar，那么该变量实际上是在全局作用域中定义，而不是在局部作用域中定义（其实本应该在局部作用域中定义）。

```javascript
var foo = function(){
	var boo = function(){
		bar = 2; // 没有使用var，所以var是在全局作用域中，即 window.bar
	}();
}();

console.log(bar); // output 2 因为bar在全局作用域中
```

相反：

```javascript
var foo = function(){
	var boo = function(){
		var doo = 2; // 使用var，所以var是在局部作用域
	}();
}();

console.log(doo); // 报错，Uncaught ReferenceError: doo is not defined
```

这里的重点是，在函数内部定义变量时，应该使用var，这样我们不用于处理那些潜在的易混淆的作用域问题。当然，要在函数内部创建或更改全局作用域内的属性，属于本规则的例外情况。

## 作用域链——chain scope（词法作用域）
当Javascript查找与变量相关的值时，会遵循一个查找链。这个链是基于作用域的层次结构的。在如下代码中，从func2函数作用域中记录了`sayHiText`值。

```javascript
var sayHiText = 'hi';

var func1 = function(){
	var func2 = function(){
		console.log(sayHiText); // hi
	}();
}();
```

当sayHiText值不包含在func2函数的作用域内部时，如何找到它? Javascript首先在func2函数中查找一个名为sayHiText的变量。如果在func2函数中没有找打，就会查找func2的父函数——func1。 在func1作用域中也找不到sayHiText变量，因此，Javascript会继续查找全局作用域（此处可找到sayHiText值）。如果sayHiText没有在全局作用域内定义，那么Javascript就会返回`undefined`。

这是一个需要掌握的非常重要的概念。让我们来看另一个代码示例。如下代码，从三个不同的作用域获取三个值。

```javascript
var x = 10;
var foo = function(){
	var y = 20;
	var bar = function(){
		var z = 30;
		console.log(z + y + x); // output 60 不解释了
	}();
}();
```

注意：
> * 仔细想一下，其实作用域链与原型链的区别并不大。两者都是通过位置体系和层次体系来查找值的方法。

## 作用域链查找返回第一轮值
看代码：

```javascript
var x = false;
var foo = function(){
	var x = false;
	bar = function(){
		var x = true;
		console.log(x); // 局部x在作用域内是第一个被查找到的，因此不再查找其余的
	}();
}

foo(); // output false
```

请记住，当在作用域链内最近位置找到变量时，查找即结束，不管作用域链顶部是否还有相同的变量名称。其实就是`就近原则`。

## 函数定义时确定作用域，而非调用时确定
由于函数决定作用域，并且函数可以像任何Javascript值那样被传递，因此有人可能会认为解密作用域链是很复杂的。它实际上却是非常简单的。作用域链是根据函数定义时的位置确定，而不是在调用时确定的。这也叫`词法作用域`。仔细思考这个问题，因为大多数人在编写Javascript代码时会被它绊住。

作用域链是在调用函数之前创建。正因为如此，我们可以创建闭包。例如，我们而已让函数向全局作用域返回一个嵌套函数，但该函数仍然能够通过作用域链访问其父函数的作用域。

如下代码，定义了parentFunction，它返回一个匿名函数，从全局作用域调用返回的函数。因为匿名函数被定义为包含在parentFunction内部，因此，它被调用后仍然能够访问parentFunction的作用域。
`这就是闭包`。

```javascript
var parentFunction = function(){
	var foo = 'foo';
	return function(){
		console.log(foo);
	}
}

// nestedFunction引用parentFunction函数返回的匿名函数
var nestedFunction = parentFunction();

nestedFunction(); // 输出 foo, 因为返回的函数可以通过作用域链访问foo
```

这里应该理解的重点是，作用域连是在定义时确定的——实际是编码的方式。在函数内部传递代码不会改变作用域链。

## 闭包`closures`是由作用域链引起的
有了作用域和作用域链的知识，就不难理解闭包了。如下代码，

```javascript
var countUpFromZero = function(){
	var count = 0;
	return function(){ // 调用countUpFromZero的时候返回的嵌套子函数
		return ++count; // count 在作用域链内定义，父函数里
	}
}(); // 立即调用，返回嵌套函数

console.log(countUpFromZero()); // output 1
console.log(countUpFromZero()); // output 2
console.log(countUpFromZero()); // output 3
```

每次调用`countUpFromZero`函数时，包含在countUpFromZero函数内（并由其返回的）的匿名函数仍可以访问父函数的作用域。这种技术，通过使用作用域链，就是一个闭包的示例。

总结一下，闭包就是`闭包就是能够从外部读取内部函数的内部变量的函数。`（反过来是很正常的）。
在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

## 使用闭包的注意点
> 1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
> 2. 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

