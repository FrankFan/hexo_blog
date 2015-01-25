title: javascript中this关键字详解
date: 2015-01-22 16:29:25
categories: javascript
---

##  this概要及this如何引用对象
创建函数时，系统会（在后台）创建一个名为`this`的关键字，它链接到运行函数的对象。换个说法就是，`this`对齐函数的作用域是可见的，而且它是函数属性/方法所在对象的一个引用。

```javascript
var cody = {
	living: true,
	age: 23,
	gender: 'male',
	getGender: function(){ return cody.gender; }
};

console.log(cody.getGender()); // output 'male'
```
 
 请注意我们是如何在getGender函数内部使用点表示法在cody对象上访问gender属性的（如cody.gender）。可以使用`this`重写来访问cody对象，因为它指向cody对象。

```javascript
var cody = {
	living: true,
	age: 23,
	gender: 'male',
	getGender: function(){ return this.gender; }
};

console.log(cody.getGender()); // output 'male'
```

`this.gender`中的this只引用该函数所要操作的cody对象。

`this`可能会令人迷惑，单页不一定要如此。只要记住，总的来说，`this`是在函数内部使用，用来引用内包含函数的对象，而不是函数本身（使用`new`关键字或`call()`和`apply()`的情况例外）。

**注意**
> * 除了不能修改这一点，`this`关键字看起来以及表现得都像其他变量。
> * 与传递函数的`arguments`和任何参数不同，`this`是call/activation对象中的关键字（不是属性）。

## 如何确定this值
`this`值会被传递给所有函数，其值基于在运行时调用函数的上下文。特别要注意，因为`this`是需要记住的其中一个另类。

```javascript
var foo = 'foo';
var myObject = { foo: 'I am myObject.foo' };

var sayFoo = function(){
	console.log(this['foo']);
};

// 给myObject设置一个sayFoo属性，并指向到sayFoo函数
myObject.sayFoo = sayFoo;

myObject.sayFoo(); // output 'I am myObject.foo'
sayFoo(); // output 'foo'
```

很显然，`this`值是基于调用函数的上下文。考虑一下`myObject.SayFoo`和`sayFoo`都指向相同的函数。然而，调用`sayFoo()`的位置（即上下文）不同`this`值也不同。

如下代码显示使用window对象，效果和上面代码等效。
```javascript
window.foo = 'foo';
window.myObject = { foo: 'I am myObject.foo' };

window.sayFoo = function(){
	console.log(this.foo);
};

window.myObject.sayFoo = window.sayFoo;

window.myObject.sayFoo();
window.sayFoo();
```

在传递函数或者有多个函数的引用时，要意识到`this`值会根据调用函数所在的上下文而改变。

**注意**
> 除了`this`和`arguments`意外的所有变量都遵循词法作用域规则


## 嵌套函数中用this关键字引用head对象
当在嵌套函数内部使用`this`时，你可能想知道`this`会发生什么事情。在ES3中`this`比较糟糕，因为`this`失去了方向，引用的是`head对象`（浏览器中的window对象），而不是定义函数所在的位置。

```javascript
var myObject = {
	func1: function() {
		console.log(this); // output myObject 对象
		var func2 = function() {
			console.log(this); // output window对象，从此处开始，this都是window对象
			var func3 = function() {
				console.log(this); // 输出window，即head对象
			}();
		}();
	}
}

myObject.func1();
```

欣慰的是，`this`在ES5中是固定的。现在，我们应该清楚的了解这种困境，尤其是在开始将函数作为值传递给其他函数的时候。

```javascript
var foo = {
	func1: function(bar){
		bar(); // 输出window，而不是foo，这是嵌套函数
		console.log(this);  // 这里的this是foo对象的一个引用
	}
}

foo.func1(function(){console.log(this) });
```

现在你将再也不会忘记：当`this`值的宿主函数被封装在另外一个函数的内部或在另一个函数的上下文中被调用时，`this`值将永远是对head对象的引用（再次说明，在ES5中是固定的）。

## 充分利用作用域链研究嵌套函数问题
可以简单地在父函数中使用作用域链来保存`this`的引用，以便`this`值不丢失。

```javascript
var myObject = {
	myProperty: 'I can see the light',
	myMethod: function(){
		var that = this; // myMetho作用域内，保存this引用（也就是，myObject）
		var helperFunction = function(){ // 子函数
			// 输出通过作用域链得到的 'I can see the light'， 因为 that = this
			console.log(that.myProperty); // 输出 'I can see the light'
			console.log(this); // 如果不使用that，则输出window object
		}();
	}
}

myObject.myMethod();
```

## 使用call()或apply()控制this值
`this`值通常取决于调用函数的上下文，但我们可以使用`apply()`或`call()`来重写/控制`this`值，以便在调用函数时定义`this`指向哪个对象。使用这些方法就好像在说：“嘿，调用X函数，但要告诉该函数把Z对象作为`this`值用。”这样做可以改变Javascript中决定`this`值的方式（取代默认方式）。

```javascript
var myObject = {};

var myFunction = function(param1, param2){
	this.foo = param1;
	this.bar = param2;
	console.log(this); // 输出Object {foo: "foo", bar: "bar"}
};

// 调用函数，设置this值引用到myObject
myFunction.call(myObject, 'foo', 'bar'); // 输出Object {foo: "foo", bar: "bar"}

console.log(myObject); // 输出Object {foo: "foo", bar: "bar"}
```

上述示例中使用的`call()`，但也可以使用`apply()`。两者的区别在于如何为函数传递参数：前者参数只是使用逗号分隔的值；后者使参数值在数组内传递。

```javascript
var myObject = {};

var myFunction = function(param1, param2){
	this.foo = param1;
	this.bar = param2;
	console.log(this); // 输出Object {foo: "foo", bar: "bar"}
};

// 调用函数，设置this值引用到myObject
myFunction.apply(myObject, ['foo', 'bar']); // 输出Object {foo: "foo", bar: "bar"}

console.log(myObject); // 输出Object {foo: "foo", bar: "bar"}
```

这里需要注意的是，可以在函数作用域中设置Javascript决定this值的方式，取代默认方式。

## 在用户定义构造函数内部使用this关键字

```javascript
var Person = function(name){
	this.name = name || 'john doe'; // this引用所创建的实例
}

var cody = new Person('Cody Lindley'); // 基于Person构造函数创建的实例
console.log(cody.name); // output Cody Lindley
```

同样，未使用`new关键字`调用构造函数时，this引用“即将创建的对象”。如果不使用new关键字，this值将是调用Person的上下文——本例中是head对象。

```javascript
var Person = function(name){
	this.name = name || 'john doe'; // this引用所创建的实例
}

var cody = Person('Cody Lindley'); // 基于Person构造函数创建的实例
console.log(cody.name); // undefined, 实际上name的值设置到window.name 上
console.log(window.name); // output Cody Lindley
```

## 原型方法内的this关键字引用构造函数实例
当在添加至构造函数的`prototype`属性的函数中使用this时，this引用调用方法的实例。

```javascript
var Person = function(x) {
	if (x) { this.fullName = x };
};

Person.prototype.whatIsMyFullName = function() {
	return this.fullName; // this 引用Person()所创建的实例
}

// 调用继承的 whatIsMyFullName 方法，该方法用this引用实例
var cody = new Person('cody lindley');
var lisa = new Person('lisa lindley');

console.log(cody.whatIsMyFullName(), lisa.whatIsMyFullName());

/* 原型链依然有效，所以如果实例没有fullName属性，程序将查找原型链。
 * 如下代码为Person原型和Object原型添加fullName属性 
 */
Object.prototype.fullName = 'John doe';
var john = new Person(); // 没有传任何参数，所以fullName没有添加到实例上

console.log(john.whatIsMyFullName()); // output 'John doe'
```

这里的重点是，当在`prototype`对象中方法内部使用this关键字时，this可用于引用实例。如果该实例不包含所要查找的属性，则继续在原型链上查找。


