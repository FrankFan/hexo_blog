title: 再谈js闭包
date: 2015-01-28 22:46:30
categories: javascript
---

![](http://images.cnitblog.com/blog/282019/201502/082243438445578)

## 定义
一谈到js闭包就不能不说js作用域、作用域链。我们知道，一个函数中嵌套另一个函数时，内部函数由于作用域链的存在，很容易访问外部函数的变量。可是，外部函数就没办法访问内部函数的变量。
一句话定义闭包：当函数a内部的函数b被函数a外的一个变量引用的时候，就创建了一个闭包。即：外部函数引用内部函数的变量。

## 作用
> * （1）可以读取函数内部的变量
> * （2）让这些变量的值是中保持在内存中

## 注意
如果过多的使用闭包而不释放掉这些引用，就会导致内存中的变量越来越多，进而影响性能。
在Javascript中，如果一个对象不再被引用，那么这个对象就会被GC回收。如果两个对象互相引用，而不再被第三者所引用，那么这两个互相引用的对象也会被回收。因为函数a被函数b引用，b又被a外的函数引用，这就是为什么函数a执行后不会被回收的原因。

## 示例

第一题：

```javascript
var person = functioin() {
     // 变量作用域为函数内部，所以外部函数通过普通方式无法访问
     var name = 'default';

     return {
          getName: function() { return name;},
          setName: function(newName) { name = newName;}
     }
}();

// 测试代码
console.log(person.name); // undefined
console.log(person.getName()); // default
console.log(person.setName('fy98.com')); // 设值
console.log(person.getName()); // fy98.com
```

第二题：

```javascript
// 假设 HTML 中有 5 个 name='btn' 的 button
// 需求是当点击按钮的时候弹出当前btn的顺序

var buttons =document.getElementsByName('btn');
var len = buttons.length;

for(var i = 0; i < len; i++) {
     var button = buttons[i];
     button.addEventListener('click', function() {
          console.log(i); 
     }, false);
}

// 上述代码的结果是： 不论点击哪个按钮，控制台打印出来的都是5， 表明`i`的值都是一样的
// 这显然不是我们想要的结果，怎么解决呢？ 可以使用闭包改造一下，让外面的函数访问内部函数的变量

// 使用闭包改造
var buttons = document.getElementsByName('btn');
var len = buttons.length;

for(var i = 0; i < len; i++) {
     var button = buttons[i];
     button.addEventListener('click', (function(i) {
          return function() {
               console.log(i); 
          }
     })(i), false);
}

```


再来一道：`不恰当使用闭包容易引起内存泄露`

```javascirpt
function foo() {
     var oDiv = document.getElementById('div');
     var id = oDiv.id; // here
     oDiv.onclick = function() {
          // alert(oDiv.id); 
          // 这里存在循环引用, IE低版本在页面关闭后oDiv仍在内存中，
          // 所以尽可能缓存基本类型，而不是对象
          alert(id);
     };
     // 手动讲对象指向null
     oDiv = null; // here
}
```


