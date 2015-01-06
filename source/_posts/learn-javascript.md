title: 【译】《Learn Javascript》
date: 2014-10-04 15:21:54
categories: javascript
---

## 介绍
### 学习Javascript
这本书将教给你编程和Javascript的基础。不论你是否是一名经验丰富的程序员，这本书适用于每一个想学习Javascript编程语言的人。


JavaScript（简称JS）是一门允许网页响应用户的交互而不仅仅是展现基本的层次编程语言。创建于1995年，js 是现在使用的最流行的编程语言之一。

**说明**：这本书由[Gitbook](http://www.gitbook.io/)生成并且是开源的，欢迎随时在[Github](http://www.github.com/)上贡献或者发布issue，您可以在[https://www.gitbook.io/book/GitBookIO/javascript](https://www.gitbook.io/book/GitBookIO/javascript)下载**PDF**或者**ePUB**版本。

**译者注**：该电子书是偶然在Gitbook上看到的一本介绍关于js基础的书，看了几章感觉甚好，适逢十一小长假，遂萌生翻译一遍的的想法。翻译技术书，不会过分追求`信达雅`，只求能用最通俗的语言把知识介绍清楚就好。全书共分8个章节，除第一章介绍外，共介绍7个主题，分别是js基础、数字类型、字符串类型、条件逻辑、数组、循环、函数、以及对象。

## 关于编程基础
在第一章，我们将要学习编程和js的基础知识。

编程意味着敲代码。一本书由章节、段落、句子和词组构成，同样的，一个程序可以被分为一小块一小块的部分。从现在开始，最终的就是语句。（程序中的）语句类似于一本书里的句子。对它自己来说有它自己的结构和目的，但是如果没有其他语句作为上下文，语句并不是那么有意义。

编程语句一般是*一行代码*。那是因为编程语句往往写在单独的几行。就像这样，程序被从上到下、从左到右地解析。也许你会疑惑什么是代码（也叫源代码），那碰巧是一个宽泛的术语，代码用来代指整个程序或者是指程序的最小部分。所以，一行代码仅仅是你程序的一部分。

下面是一个简单的实例：
```javascript
var hello = "Hello";
var world = "World";

// Message equals "Hello World"
var message = hello + " " + world;
```

这段代码可以被另一个叫做*解释器*的程序所执行，解释器先读代码，然后用合适的顺序执行所有的语句。

### 注释
注释是不会被解释器执行的语句，是用来给其他程序员或者对你写的代码做小段描述用的标记说明，这样可以使你写的代码更容易被其他人理解。

在Javascript中，注释通常有2中写法：

- 用双斜杠 `//` 开头：
```javascript
// 这是一行注释，将会被解释器忽略
var a = "this is a variable defined in a statement";
```
- 一个代码块用 `/*` 开头、由 `*/` 结束，这种方法用来进行多行注释
```javascript
/*
这是多行注释,
也会被解释器忽略
*/
var a = "this is a variable defined in a statement";
```

### 变量
要真正理解编程的第一步是回顾一下`代数`。如果你还记得在学校里，代数课就像下面从写等式开始。
```javascript
3 + 5 = 8
```
当引入一个未知数时你就会开始计算，例如：
```javascript
3 + x = 8
```
移动数字就可得出x：
```javascript
x = 8 -3
-> x = 5
```
当引入不知一个未知数时会使你的等式更加多变，这时可以使用`变量`：
```javascript
x + y = 8
```
你可以改变x和y的值，等式依然成立：
```javascript
x = 4
y = 4
```
或者
```javascript
x = 3
y = 5
```

这种规律和编程语言一样。在程序中，变量是会变化的值的载体。变量可以承载所有类型的值，也包含计算的结果。变量有一个`名称`和一个`值`由等号`=`隔开。变量名称可以是任意字母或数字，但是要紧记你可以使用变量名根据不同的编程语言而有所限制，因为一些单词为了其他功能会作为`保留字`。

让我们看看变量是如何在Javascript中工作的，以下代码定义了2个变量，计算2个变量相加的结果并且定义第三个变量作为结果。
```javascript
var x = 5;
var x = 6;
var result = x + y;
```

### 变量类型
计算机很复杂，并且可以使用更复杂的变量而不仅仅是数字。这就是引入变量类型的原因所在。变量有多种类型并且不同的语言支持不同类型的变量。
最常用的变量类型有：

- **数值类型**
	+ **浮点数**：就像1.21323、4、-33.5、10004或者0.123这样的数字
	+ **整数**：就像1、12、-33、140这样的整数，不能包含1.233这样的小数
- **字符串**：就像"boat","elephant"或者"damn, you are tall!"这样的一行文本
- **布尔值**：不是真就是假，没有别的选择
- **数组**：就像：1,2,3,4,'I am bored now'这样的值的集合
- **对象**：表示一个更加复杂的事物

JavaScript是一种`类型宽松`的语言，意味着不必显式声明数据变量的类型。
你只需使用`var`关键字表示你声明一个变量，解释器会根据上下文来决定使用什么样的数据类型。

### 相等
程序员经常需要判断变量同其他变量的相等关系，这使用`相等操作符`来完成。

最基本的相等操作符是 `==` ，该操作符可以判断任何两个即使类型不同的变量是否相等。

例如：
```javascript
var foo = 42;
var bar = 42;
var baz = "42";
var qux = "life";
```

`foo == bar` 的值为 `true`， `baz == qux`的值为 `false`，正如我们期望的一样。然而，尽管 **foo** 和 **baz** 是不同的类型，但是 `foo == baz` 的值也是 `true`。在双等操作符 `==` 背后，会尝试强制使操作符转成相同类型在进行相等性判断。这一点和三等操作符 `===` 相反。

三等操作符`===`用来判断两个变量是否相等，相等的前提是同样的类型和同样的值。按照上面的例子，这意味着`foo == bar` 的值依然为 `true`， 但是 `foo == baz` 的值现在是 `false`。`baz == qux`的值依然为 `false`。

## 数值
Javascript只有一种数据类型——64位浮点数。和Java中的**double**一样。和其他大多数语言不一样，Javascript没有单独的整数类型，因此`1`和`1.0`是相同的值。

### 创建
创建一个数值很简单，就像其他任何变量类型使用**var**关键字就可以。

数值可以根据常量值来创建：
```javascript
// This is a float:
var a = 1.2;

// This is a integer:
var b=  10;
```
或者通过另一个变量来创建：
```javascript
var a = 2;
var b=  a;
```


### 基本操作符
您可以使用下列操作符对数值使用数学运算：

- **加**：`c = a + b`
- **减**：`c = a - b`
- **乘**：`c = a * b`
- **除**：`c = a / b`

可以使用括号，就像数学中分离和组合运算。

### 高级操作符
可以使用一些高级运算符，例如：

- **模(除数取余)**: `x = y % 2`
- **自增**: 给定 `a = 5`
	+ `c = a++`，结果是 `c = 5` 且 `a = 6`
	+ `c = ++a`，结果是 `c = 6` 且 `a = 6`
- **自减**: 给定 `a = 5`
	+ `c = a--`，结果是 `c = 5` 且 `a = 4`
	+ `c = --a`，结果是 `c = 4` 且 `a = 4`

## 字符串
Javascript的字符串与其他高级语言的字符串的实现有许多相似之处，表示基于文本的消息和数据。

这一节我们将介绍基本知识：如何创建新字符串，并对其执行常用操作。

下面是string的一个例子：
```javascript
"Hello World"
```

### 创建
在Javascript中通过单引号或者双引号括起来文本来定义字符串：

```javascript
// Single quotes can be used
var str = 'Our lovely string';

// Double quotes as well
var otherStr = "Another nice string";
```
在Javascript中，字符串可以包含UTF-8字符：
```javascript
"中文 español English हिन्दी العربية português বাংলা русский 日本語 ਪੰਜਾਬੀ 한국어";
```

> **注**：字符串不能减，乘或除。

### 拼接字符串
拼接字符串通过添加2个或多个字符串在一起，从而创建这些包含原始字符串组合数据的较大字符串。
在Javascript中通过加号操作符 `+` 来完成。

```javascript
var bigStr = 'Hi ' + 'JS strings are nice ' + 'and ' + 'easy to add';
```

### 长度
在Javascript中通过 `.length` 属性很容易得知一个字符串中有多少个字符。
```javascript
// Just use the property .length
var size = 'Our lovely string'.length;
```
> **注**：字符串不能减，乘或除。


## 条件逻辑
条件就是某种东西的一个测试。对于编程来说条件非常重要，主要表现一下几方面：

首先，不管程序在处理时你输入了什么数据，条件能来确保你的程序可以工作。如果你盲目的相信数据，你将会陷入困境并且你的程序也会失败。如果测试你想做的事情是可能的并且以正确的格式拥有所有必需的信息，那么失败就不会发生，而且你的程序也会更加稳定。采取这样的预防措施，也被称为编程防守。

另外，条件可以让程序中加入分支。在填写表格时你也许已经遇到过分支图了。基本上，这是在执行不同的分支代码（部分），取决于条件是否被满足。

在这一章我们将要学习Javascript中条件逻辑的基础。

### if 条件语句
最简单的条件语句是`if`语句，它的语法是 `if(condition){ do this ...}`。条件为`true`的话就会执行花括号中的代码。
例如你可以根据字符串的值给它设置另一个字符串的值来测试一个字符串。

```javascript
var country = 'France';
var weather;
var food;
var currency;
if(country === 'England') {
    weather = 'horrible';
    food = 'filling';
    currency = 'pound sterling';
}
if(country === 'France') {
    weather = 'nice';
    food = 'stunning, but hardly ever vegetarian';
    currency = 'funny, small and colourful';
}
if(country === 'Germany') {
    weather = 'average';
    food = 'wurst thing ever';
    currency = 'funny, small and colourful';
}
var message = 'this is ' + country + ', the weather is ' +
            weather + ', the food is ' + food + ' and the ' +
            'currency is ' + currency;
```

> **注**：条件可以嵌套。

### else
当第一个条件不为`true`时`else`从句将会生效。如果你相对任何值做出反应这一点很强大，但是要挑出一个特别的做特殊处理。

```javascript
var umbrellaMandatory;
if(country === 'England'){
    umbrellaMandatory = true;
} else {
    umbrellaMandatory = false;
}
```

`else`子句可以和另一个`if`子句拼接。让我们根据上文改造一下这个例子：

```javascript
if(country === 'England') {
    ...
} else if(country === 'France') {
    ...
} else if(country === 'Germany') {
    ...
}
```

### 比较
现在让我们来关注一下条件部分：

```javascript
if(country === 'France') {
    ...
}
```

条件部分是一个变量`country`紧跟着一个三等操作符`===`。三等操作符用来测试变量`country`是否有正确的值（**France**）和正确的类型（**String**）。你也可以用双等操作符来判断条件。然而，例如一个`if(x == 5)`的条件对`var x = 5`和`x = '5'`都返回`true`；根据你程序的功能这一点会导致很大的不同。最为最佳实践(`Best Practice`)强烈推荐你使用三等操作符 (`===` 和 `!==`) 而不是双等操作符 (`==` 和 `!=`)。

其他条件判断：

- `x > a`：x是否比a大?
- `x < a`：x是否比a小?
- `x <= a`：x是否小于等于a?
- `x != a`：x不是a?
- `x`：x是否存在?


### 条件连接
此外你可以使用`or`或者`and`语句拼接不同的条件来判断每个条件是否是`true`，或者两个是否分别是`true`。

在Javascript中`or`写作`||`，`and`写作`&&`。

假定想判断`x`的值是在10和20之间，你可以用条件语句来做：
```javascript
if(x > 10 && x < 20) {
    ...
}
```

如果你想确定`country`是`England`或者`Germany`，你可以使用：
```javascript
if(country === 'England' || country === 'Germany') {
    ...
}
```

> **注**：就像数值操作符一样，条件语句也可以使用括号来进行分组，例如：
`if ( (name === "John" || name === "Jennifer") && country === "France")`

## 数组
数组是程序设计的基本组成部分。数据就是数据的集合。我们可以在一个变量中存放许多数据，这使得代码更容易阅读而且易于理解。并且在操作函数操作相关数据变的更容易。

数组中的数据被称作**元素**。

下面是一个简单的数组：
```javascript
// 1, 1, 2, 3, 5, and 8 are the elements in this array
var numbers = [1, 1, 2, 3, 5, 8];
```

### 索引indicies
你有一个由数据元素构成的数组，但是假如要访问某个特定的元素该怎么办呢？这就是介绍索引的原因。索引是数组中的一个点。在逻辑上索引一个一个的增长，但是应当注意的是在数组中索引是从**0**开始的，就像大多数编程语言一样。中括号`[]`用来表示数组的索引。

```javascript
// This is an array of strings
var fruits = ["apple", "banana", "pineapple", "strawberry"];

// We set the variable banana to the value of the second element of
// the fruits array. Remember that indicies start at 0, so 1 is the
// second element. Result: banana = "banana"
var banana = fruits[1];
```

### 长度
数组有一个属性叫做长度`.length`,和听起来几乎一样，表示数组的长度。

```javascript
var array = [1 , 2, 3];

// Result: l = 3
var len = array.length;
```

## 循环
循环是在循环变化中有一个变量重复的情况。如果你想一次一次的运行相同的代码并且每次有一个不同的值，那么循环是方便的。

不是这样写：
```javascript
doThing(cars[0]);
doThing(cars[1]);
doThing(cars[2]);
doThing(cars[3]);
doThing(cars[4]);
```

而是：
```javascript
for (var i=0; i < cars.length; i++) { 
    doThing(cars[i]);
}
```

### `for` 循环
循环最简单的方式是`for`循环。语法上`for`循环和`if`语句相似，但是有更多的选项：
```javascript
for (condition; end condition; change) {
    // do it, do it now
};
```

例如我们看一下如何利用**`for`**循环执行10次相同的代码：
```javascript
for(var i = 0; i < 10; i = i + 1){
    // do this code ten-times
}
```

> **注**：`i = i + 1` 可以写成 `i++`。

### `while` 循环
只要条件是`true`的话`while`循环会重复的执行一个代码块。
```javascript
while(condition){
    // do it as long as condition is true
}
```

在下面的例子中我们重复的执行一个代码块只要变量`i`小于5：
```javascript
var i = 0, x = "";
while (i < 5) {
    x = x + "The number is " + i + "\n";
    i++;
}
```

`Do/While`循环是`while`循环的变种。这种循环会在检查条件为`true`之前执行一遍代码块，然后只要条件为`true`循环代码块。

```javascript
do {
    // code block to be executed
} while (condition);
```

> **注**：要小心避免条件永远为真导致无限循环的情况。

## 函数
函数是编程语言中最强大最重要的概念之一。

函数就像数学中的函数进行变换，它接受叫做`参数`的输入值最后返回一个输出值。

### 函数声明
就像其他变量一样，函数必须先声明。让我们声明一个函数**double**，它接收参数`x`，输出`x`的2倍：

```javascript
function double (x) {
    return 2 * x;
}
```
> **注**：上面的函数在它被定义之前**可以**被引用到。

在Javascript中函数也是值，他们可以被存放在某个变量中，比如：`numbers`、`string`等等，并且可以作为参数传递给另一个函数：

```javascript
var double = function(x) {
    return 2 * x;
};
```

> **注**：上面的函数在它被定义之前**不会**被引用到，就像其他任意变量一样。

### 高阶函数
高阶函数是处理其他函数的函数。比如，一个函数可以把其他函数作为参数，并且/或者作为返回值返回一个函数。在 javascript 和其他高级语言，如Python、list等，都提供了这样*花哨*的功能性技术和强大的结构。

现在我们创建两个简单的函数：**add_2** 、 **double** 和 一个叫做 **map** 的高阶函数。 **map** 接收2个参数， **func** 和 **list**（所以该函数的声明是 **map(func,list)** ），最后返回一个数组。第一个参数 **func** 是一个作用于数组 **list** （第二个参数） 中每一个元素的函数。

```javascript
// Define two simple functions
var add_2 = function(x) {
    return x + 2;
};
var double = function(x) {
    return 2 * x;
};

// map is cool function that accepts 2 arguments:
//  func    the function to call
//  list    a array of values to call func on
var map = function(func, list) {
    var output=[];              // output list
    for(idx in list) {
        output.push( func(list[idx]) );
    }
    return output;
}
// We use map to apply a function to an entire list
// of inputs to "map" them to a list of corresponding outputs
map(add_2, [5,6,7]) // => [7, 8, 9]
map(double, [5,6,7]) // => [10, 12, 14]
```

上面例子中的函数很简单。然而，当我们当做参数传递给其他函数时，它会以不可预见的方式构建成构架复杂的函数。

例如：如果我们在代码中很频繁的调用 **map(add_2, ...)** 和 **map(double, ...)** ，我们可以创建2个特殊目的的列表处理函数，把需要的操作封装到里面。使用函数组合，我们可以做如下改造：

```javascript
process_add_2 = function(list) {
    return map(add_2, list);
}
process_double = function(list) {
    return map(double, list);
}
process_add_2([5,6,7]) // => [7, 8, 9]
process_double([5,6,7]) // => [10, 12, 14]
```

现在让我们创建一个叫做 **buildProcessor** 的函数，接收一个函数 **func** 作为输入参数并且返回一个 **func-processor** ，也就是一个把函数 **func** 作用于列表中每一个输入元素的函数。

```javascript
// a function that generates a list processor that performs
var buildProcessor = function(func) {
    var process_func = function(list) {
        return map(func, list);
    }
    return process_func;
}
// calling buildProcessor returns a function which is called with a list input

// using buildProcessor we could generate the add_2 and double list processors as follows:
process_add_2 = buildProcessor(add_2);
process_double = buildProcessor(double);

process_add_2([5,6,7]) // => [7, 8, 9]
process_double([5,6,7]) // => [10, 12, 14]
```

让我们来看另外一个例子。我们创建一个叫做 **buildMultiplier** 的函数，接收 `x` 作为输入参数，并且返回一个用它的参数乘以 `x` 的函数。

```javascript
var buildMultiplier = function(x) {
    return function(y) {
        return x * y;
    }
}
var double = buildMultiplier(2);
var triple = buildMultiplier(3);
double(3); // => 6
triple(3); // => 9
```

## 对象
javascript中最基本的数据类型是`true`、`false`、数值类型、字符串、`null`和`undefined`。除此之外全都是`对象object`
在Javascript中对象包含 `属性名：属性值` 键值对。

### 创建
在Javascript中有两种方式创建对象：

1.字面量（literal）

```javascript
var object = {};
  // Yes, simply a pair of curly braces!
```
> **注**：**推荐**使用这种方式。

2.面向对象（OO）的方式

```javascript
var object = new Object();
```
> **注**：和Java很像。

### 属性
对象的属性是一个`属性名：属性值`的键值对，他的**属性名只能是string类型**。如果不是字符串类型，将会被装换成字符串类型。在创建对象时或者之后，你可以指定属性名。对象中可以有0个或多个被逗号`,`隔开的属性。

```javascript
var language = {
    name: 'JavaScript',
    isSupportedByBrowsers: true,
    createdIn: 1995,
    author:{
        firstName: 'Brendan',
        lastName: 'Eich'
    },
 // Yes, objects can be nested!
    getAuthorFullName: function(){
        return this.author.firstName + this.author.lastName;    
    }
 // Yes, functions can be values too!
};
```

下面代码示范如何**获取**属性值：
```javascript
var variable = language.name;
// variable now contains "JavaScript" string.
variable = language['name'];
/* The lines above do the same thing. The difference is that the second one lets you use litteraly any string as a property name, but it's less readable. */
variable = language.newProperty; 
// variable is now undefined, because we have not assigned this property yet.
```

下面代码展示如何*添加**一个新的属性或者**改变**一个已存在的属性。

```javascript
language.newProperty = 'new value';
// Now the object has a new property. If the property already exists, its value will be replaced.
language['newProperty'] = 'changed value';
// Once again, you can access properties both ways. The first one (dot notation) is recomend
```

### 可变的(Mutable)
对象和基本类型的不同点在于我们可以**改变对象**，而基本类型是不可变的。

```javascript
var myPrimitive = "first value";
    myPrimitive = "another value";
 // myPrimitive now points to another string.
var myObject = { key: "first value"};
    myObject.key = "another value";
 // myObject points to the same object.
```

### 引用
对象**永远不会被复制**。他们通过引用被传递。

```javascript
// Imagine I had a pizza
var myPizza = {slices: 5};
 // And I shared it with You
var yourPizza = myPizza;
 // I eat another slice
myPizza.slices = myPizza.slices - 1;
var numberOfSlicesLeft = yourPizza.slices;
 // Now We have 4 slices because myPizza and yourPizza
 // reference to the same pizza object.
var a = {}, b = {}, c = {};
 // a, b, and c each refer to a
 // different empty object
a = b = c = {};
 // a, b, and c all refer to
 // the same empty object
```

### 原型prototype
每个对象链接到一个从它继承属性的原型对象上。

所有由字面量({})创建的对象自动地被链接到 `Object.prototype` 上，它是Javascript的一个标准对象。

当Javascript解释器（浏览器中的一个模块）尝试查找属性时，就像下面代码一样：

```javascript
var adult = {age: 26},
    retrievedProperty = adult.age;
// The line above
```

首先，解释器浏览对象拥有的每一个属性。例如 `adult` 只有一个属性——`age`，但是除此之外它实际上还有几个属性，就是继承自 `Object.prototype` 的。

```javascript
var stringRepresentation = adult.toString();
// the variable has value of '[object Object]'
```

`toString` 是继承自 `Object.prototype` 的一个属性。它有一个值是函数，返回一个表示这个对象的字符串。如果你想返回一个更加有意义的字符串，那么你可以**重写** 它。 很简单，给`adult`对象添加一个新的属性。

```javascript
adult.toString = function(){
    return "I'm "+this.age;
}
```

如果你现在调用`toString`方法，解释器将会在对象本身中查找这个新的属性，然后停止。

这样，解释器从对象本身检索第一个属性，更多的属性从它的原型（`prototype`）中检索。

给你自己的对象设置属性而不是使用默认的`Object.prototype`，你可以调用`Object.create`，如下所示：
```javascript
var child = Object.create(adult);
 /* This way of creating objects lets us easly replace the default Object.prototype with the one we want. In this case, the child's prototype is the adult object. */
child.age = 8;
 /* Previously, child didn't have its own age property, and the interpreter had to look further to the child's prototype to find it.
 Now, when we set the child's own age, the interpereter will not go further.
 Note: adult's age is still 26. */
var stringRepresentation = child.toString();
 // The value is "I'm 8".
/* Note: we have not overrided the child's toString property, thus the adult's method will be invoked. If adult did not have toString property, then Object.prototype's toString method would be invoked, and we would get "[object Object]" instead of "I'm 8" */
```

`child`的原型是`adult`，`adult`的原型是`Object.prototype`。这个原型链顺序成为`原型链`。

### 删除
`delete`用于从对象中**移除一个属性**。它将从对象中移除一个属性，如果这个对象有的话。它不会沿着原型链向上找。从对象中删除一个属性允许从原型链中找：

```javascript
var adult = {age:26},
    child = Object.create(adult);
    child.age = 8;
delete child.age;
 /* Remove age property from child, revealing the age of the prototype, because then it is not overriden. */
var prototypeAge = child.age;
 // 26, because child does not have its own age property.
```

### 枚举
`for in`语句可以遍历对象中的每个属性，枚举包含函数和原型属性。

```javascript
var fruit = {
    apple: 2,
    orange:5,
    pear:1
},
sentence = 'I have ',
quantity;
for (kind in fruit){
    quantity = fruit[kind];
    sentence += quantity+' '+kind+
                (quantity===1?'':'s')+
                ', ';
}
 // The following line removes the trailing coma.
sentence = sentence.substr(0,sentence.length-2)+'.';
 // I have 2 apples, 5 oranges, 1 pear.
```

### 全局变量Global Footprint
如果你正在开发一个可能运行在网页上的一个模块，同时运行着其他模块，那么你必须小心变量名重复的情况。

假定我们正在开发一个计数器模块：

```javascript
var myCounter = {
    number = 0,
    plusPlus = function(){
        this.number = this.number + 1;
    },
    isGreaterThanTen = function(){
        return this.number > 10;
    }
}
```

> **注**：这项技术经常和`闭包`一起使用，使得内部状态相对于外部状态是不可变的。

这个模块现在只有一个变量——`myCounter`。如果这个页面上的其他模块使用诸如`number`或者`isGreaterThanTen`这样的变量也是绝对安全的，因为我们不会覆盖彼此的值。

![](http://images.cnitblog.com/blog/282019/201409/282318313899917)

> 全文完。