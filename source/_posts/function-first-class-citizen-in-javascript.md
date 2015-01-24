title: js中的一等公民——Function()对象
date: 2015-01-20 23:49:59
categories: javascript
---

## Function()对象概要
函数是代码语句的容器，可以使用圆括号操作符`()`来调用。调用函数时，参数可以在圆括号内传递，以便函数中的语句可以访问这些特定值。

如下代码创建了两个版本的`addNumbers`函数对象，一个使用`new`操作符，另一个使用更常见的`字面量模式`。两者都需要两个参数。两种函数在调用时，都可以在圆括号操作符`()`中传递参数。

```javascript
var addNumbersA = new Function('num1', 'num2', 'return num1 + num2');
console.log(addNumbersA(2, 3)); //output 5

// 也可以使用字面量模式，这种方式更常用
var addNumbersB = function(num1, num2){
	return num1 + num2;
}
console.log(addNumbersA(2, 2)); //output 4
```

函数可用于返回值、构建对象，或者作为一种机制简单的运行代码。Javascript的函数有很多种用途，但从最基本的形式来说，函数只是可执行语句的唯一作用域。

## Function()的参数
Function()构造函数采用不定数量的参数，但Function()构造函数的最后一个参数是一个包含具有函数体语句的字符串。在最后一个参数之前传递给构造函数的任何参数都可用于创建函数。也可以将多个参数放在一起以逗号分隔形成字符串进行传递。

```javascript
var addFunction = new Function('num1', 'num2', 'return num1 + num2');

// 同样，所有参数放在一起用逗号隔开形成字符串作为第一个参数，第二个参数为函数体
var timesFunction = new Function('num1,num2', 'return num1 * num2');

console.log(addFunction(2, 2), timesFunction(2, 3));

// 与此同时，还可以使用表示形式初始化函数的方式，这种形式更常用
var addFunction2 = function(num1, num2){
	return num1 + num2;
}

// 语句形式
function addFunction3(num1,num2){
	return num1 + num2;
}
```

**注意：**
> * 不推荐或通常不直接利用Function()构造函数，因为Javascript将使用`eval()`来解析包含函数逻辑的字符串。很多人认为不必要使用`eval()`，因为如果使用它，很有可能出现代码设计缺陷。
> * 使用带`new`关键字的Function()构造函数创建函数对象，与仅使用构造函数创建函数对象具有先攻的效果，如`new Function('x', 'return x')`与`function('x', 'return x')`。
> * 直接使用Function()构造函数时没有创建闭包。

## 函数总有返回值
由于可以创建一个函数以简单的执行代码语句，因此函数返回一个值也是很常见的。

```javascript
var sayHi = function(){
	return 'Hi';
}
console.log(sayHi()); // output Hi
```

如果函数没有指定返回值，则会返回`undefined`。下面代码调用yelp函数，它将字符串`'yelp'`打印至控制台，切不会显示返回值。

```javascript
var sayHi = function(){
	return 'Hi';
}
console.log(sayHi()); // output Hi


var yelp = function(){
	// 如果不声明返回值，则返回undefined
	console.log('I am yelping!');
}
// output true
console.log(yelp() === undefined);
```

这里的重点是，即使没有显示地提供要返回的值，所有函数也都返回了一个值。如果不指定要返回的值，则返回的值是`undefined`。

## 函数是一等公民——不仅语法，还有值
在Javascript中，函数是对象。这意味着函数可以存储在一个变量、数组或对象中。同时，函数还可以传递给函数，并由函数返回。函数拥有属性，因为他是一个对象。所有这些因素是函数在Javascript中成为了`一等公民 —— first-class citizen`。

```javascript
// 函数可以保存在变量（funcA）、数组（funcB）和对象（funcC）中
var funcA = function(){}; // 调用方式： funcA()
var funcB = [function(){}]; // 调用方式： funcB[0]()
var funcC = { method: function(){ } }; // 调用方式： funcC.method() 或者 funcC['method']()

// 函数可以作为参数传递，也可以作为返回值返回
var funcD = function(func){
	return func;
}

var runFuncPassedToFuncD = funcD(function(){
	console.log('Hi');
});

runFuncPassedToFuncD();

// 函数是对象，也就意味着函数也拥有属性
var funcE = function(){ };
funcE.answer = 'yup'; // 实例化属性
console.log(funcE.answer); // output yup
```

至关重要的是要意识到函数是一个对象，因此函数也是一个值。它可以像Javascript中的其他表达式那样被传递或增加。

## 函数的参数传递
在调用函数时，参数是将值传递给函数作用域的工具。

```javascript
var addFunction = function(number1, number2){
	var sum = number1 + number2;
	return sum;
}

console.log(addFunction(2, 6)); // output 8
```

**注意**
> * 与其他编程语言相比，在Javascript中省略参数是完全合法的，即使已定义了接收这些参数的函数。只是为省略的参数赋予了`undefined`值。当然，省略参数后函数有可能无法正常工作。
> * 如果向函数传递意想不到的参数（那些在创建函数时没有被定义的参数），则不会发生任何错误。而且可以从`arguments`对象访问这些参数，`arguments`对象对所有的函数都是可用的。

## this和arguments适用于所有函数
在所有函数的作用域/函数体内，`this`和`arguments`值都是可用的。

`arguments`对象是一种类数组的对象，它包含所有传递给函数的参数。在下列代码中，即使在定义函数时不指定参数，在调用时如果还是发送参数，我们也可以依靠传递给函数的`arguments`数组来访问参数。

```javascript
var add = function(){
	return arguments[0] + arguments[1];
};

console.log(add(3, 5)); // output 8
```

传递给所有函数的`this`关键字都是对`包含函数的对象的引用`。如您所料，作为属性包含在对象内的函数（即方法），也是可以使用`this`来获得对“父”对象的引用。当函数在全局作用域中定义时，`this`值是全局对象。

```javascript
var myObject1 = {
	name: 'myObject1',
	myMethod: function(){ console.log(this); }
};

myObject1.myMethod(); // output 'myObject1'

var myObject2 = function(){ console.log(this); }

myObject2(); // output 'window对象'
```


## arguments.callee属性
`arguments`对象拥有名为`callee`的属性，它是对当前执行函数的引用。该属性可以用于从函数的作用域内引用函数（如`arguments.callee`）——自我引用。

```javascript
var foo = function foo() {
	console.log(arguments.callee); // output 
	// callee 可以用于对foo函数进行递归调用（例如，arguments.callee()）
}();
```

当函数需要递归调用时，它非常有用。


## 函数实例的length属性和arguments.length
`arguments`对象有一个独特的`length`属性。大家可能会认为这个`length`属性将提供已定义参数的数量，实际上，它给出的是在`调用时`发送给函数的参数数量。

```javascript
var myFunction = function(z, s, d){
	return arguments.length;
};

console.log(myFunction()); // output 0 因为没有传入任何参数
```

通过使用Function()实例的`length`属性，实际上可以获得函数所需要的参数总数量。

```javascript
var myFunction = function(z, s, d, e, r, m, q){
	return myFunction.length;
};

console.log(myFunction()); // output 7
```

**注意**
> 自Javascript 1.4 开始，`arguments.length`属性就被废弃掉了，可以从函数对象的`length`属性获取发送给函数的参数数量。
> 因此，接下来可以通过利用`callee`属性获得长度值，首先获得对被调用函数的引用（即`arguments.callee.length`）。



## 重定义函数参数
函数的参数可以直接在函数内部或通过使用`arguments`数组进行重新定义。

```javascript
var foo = false;
var bar = false;

var myFunction = function(foo, bar){
	arguments[0] = true;
	bar = true;
	console.log(arguments[0], bar); // output true true
};

myFunction();
```

请注意，可以使用`arguments`索引或直接为参数再指定一个新值来重新定义`bar`参数的值。


## 代码执行完成前取消函数执行
可以通过返回有值或无值的`return`关键字在调用时随时取消函数执行。下面代码中如果参数是`undefined`或非数字，则取消执行`add`函数。

```javascript
var add = function(x, y){
	// 如果参数不是数字，返回错误
	if(typeof x !== 'number' || typeof y !== 'number'){
		return 'pass in numbers';
	}
	return x + y;
}

console.log(add(3, 4)); // output 7
console.log(add('2', '2')); // output 'pass in numbers'
```

这里的重点是，可以在函数执行的任意点上通过使用`return`关键字来取消函数的执行。

## 定义函数
函数的定义有三种不同的方式：`函数构造函数`、`函数语句`和`函数表达式`。

```javascript
// 函数构造函数：最后一个参数是函数逻辑，之前的都是参数
var addConstructor = new Function('x', 'y', 'return x + y');

// 函数语句
function addStatement(x, y){
	return x + y;
}

// 函数表达式
var addExpression = function(x, y){
	return x + y;
}

console.log(addConstructor(2, 2), addStatement(2, 3), addExpression(2, 4));
```

**注意：**
> * 有些人说，第四种定义函数的方式被称为“命名函数表达式”。命名函数表达式只是一个包含名称的函数表达式（如 `var add = function add(x, y){return x + y;}`）。

##调用函数
使用4中不同的场景或模式调用函数。
> * 作为函数
> * 作为方法
> * 作为构造函数
> * 使用`apply()`或`call()`

```javascript
// 函数模式
var myFunction = function(){ return 'foo';}
console.log(myFunction()); // output 'foo'

// 方法模式
var myObject = { myFunction: function(){ return 'bar'; }}
console.log(myObject.myFunction()); // output 'bar'

// 构造函数模式
var Cody = function(){
	this.living = true,
	this.age = 33,
	this.gender = 'male',
	this.getGender = function(){ return this.gender };
}
var cody = new Cody(); // 通过Cody构造函数调用
console.log(cody); // output cody对象和属性

// apply() 和 call() 模式
var greet = {
	runGreet: function(){
		console.log(this.name, arguments[0], arguments[1]);
	}
}

var cody = { name: 'cody' };
var lisa = { name: 'lisa' };

// 在 cody 对象上调用 runGreet 函数
greet.runGreet.call(cody, 'foo', 'bar'); // output 'cody foo bar'

// 在 lisa 对象上调用 runGreet 函数
greet.runGreet.apply(lisa, ['foo', 'bar']); // output 'lisa foo bar'

/* 注意 call() 和 apply() 之间的区别是函数调用时，参数传递的不同，
* 前者传递多个分开的参数，后者传递多个参数组成的数组
*/
```

要理解这4中调用模式，因为以后遇到的代码可能会用到其中一种模式。

## 匿名函数
匿名函数是一种没有给出标示符的函数。匿名函数主要用于将函数作为参数传递给另一个函数。

```javascript
// function(){console.log('hi');}; // 匿名函数，但无法调用

// 创建一个函数来执行匿名函数
var sayHi = function(f){
	f();
}

// 将匿名函数作为参数传递
sayHi(function(){
	console.log('hi'); // output 'hi'
});
```

## 自调用的函数表达式
通过圆括号操作符可以在定义函数表达式后立即调用该函数表达式（除了由`Function()`构造函数创建的函数）。下面创建了一个`sayWord()`函数表达式，然后立即调用该函数。这就是自调用函数。

```javascript
// output 'hello world.'
var sayWord = function () { console.log('hello world.'); }();
```

## 自调用的匿名函数语句
可以创建一个自调用的匿名函数语句，这叫做自调用匿名函数。

```javascript
// 最经常使用的匿名函数
(function (msg) { 
	console.log(msg);
} )('Hi');

// 看起来有点不一样，但效果一样
(function(msg){
	console.log(msg);
}('Hi 1'));

// 更简短的方式
!function(msg){ console.log(msg); }('Hi 2');

// 注意，下面的代码报错：Uncaught SyntaxError: Unexpected token )
function sayHi(){ console.log('Hi');}()
```

**注意：**
> * 根据ECMAScript标准，如果要立即调用函数，需要使用函数外面的圆括号（或任何将函数转化为表达式的符号）。

## 函数可以嵌套
函数可以无限地嵌套在其他函数内部。在如下代码中，在`bar`函数内部封装了`goo`函数，同时`bar`函数位于`foo`函数内部。

```javascript
var foo = function(){
	var bar = function(){
		var goo = function(){
			console.log(this); // ouput window 对象
		}();
	}();
}();
```

这里的要点是，函数是可以嵌套的，并且嵌套的深度是没有限制的。

**注意：**
> * 请记住，嵌套函数的`this`值在ECMAScript3、Javascript 1.5中是head对象（如在web浏览器中是window对象）。


## 给函数传递函数，从函数返回函数
如上所述，函数在Javascript世界中是“一等公民”。由于函数是一个值，并且可以将任何类型的值传递给函数，因此函数可以被传递给函数。函数可以接收/返回其他函数。它们有时被称为“高阶函数”。

如下代码，将一个匿名函数传递给`foo函数`，它是稍后立即从`foo函数`返回的函数。这个匿名函数是`bar`变量指向的函数，`foo`函数先接收，然后返回该匿名函数。

```javascript
// 函数可以传入，也可以传出
var foo = function(f){
	return f;
}

var bar = foo(function(){ console.log('Hi'); });

bar(); // outpu 'Hi'
```

因此，当`bar`被调用时它调用传递给`foo()`匿名函数，然后从`foo()函数`传回，并从`bar`变量引用。所有这些都是在展示，函数可以像任何其他的值一样被传递。

## 函数定义之前调用（函数提升）
在真正定义函数语句之前，可以在执行时调用该函数语句。这有点奇怪，但你应该了解它，这样你就可以利用它，或者至少知道遇到它时会发生什么事情。

```javascript
// 示例 1
var speak = function(){
	sayYo(); // sayYo() 还没有被定义，但依然可以执行，并输出 'yo'
	function sayYo(){ console.log('yo'); }
}(); // invoke


// 示例 2
console.log(sum(2, 3)); // sum() 没定义之前，被调用，依然可以执行
function sum(x, y){ return x + y; }
```

上述情况发生的原因是，在运行代码之前，函数语句其实已经被编译器解释，并添加至执行堆栈/上下文。在使用函数语句时要确保自己理解这一点。

**注意**
> 被定义为`“函数表达式”`的函数没有被提升，只有`“函数语句”`被提升。

## 函数可以调用自身（递归）
函数调用自身完全是合法的。事实上，这是非常有名的编码模式。在如下代码中，

```javascript
var coundDownFrom = function coundDownFrom(num){
	console.log(num);
	num--; //改变参数值
	if(num < 0){ return false; } // 如果 num < 0 ,停止递归
	// 如果是匿名函数的话，也可以使用 arguments.callee(num) 进行递归
	coundDownFrom(num);
};

coundDownFrom(5); // 调用函数，输出 5,4,3,2,1,0
```