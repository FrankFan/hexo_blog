title: Javascript需要掌握的基础知识
date: 2014-11-15 20:21:48
categories: javascript
---

## 一、八大数据类型 
* 基本数据类型：数值型 （number）、字符串型（string）、逻辑型（boolean）； 
* 特殊数据类型：无定义数据类型 （undefined）、空值(null)； 
* 复合数据类型：函数（function）、对象（object）、数组 （array）。 

## 二、JS 中如何判断－undefined 
```javascript
if (typeof exp == "undefined") {   
    alert("undefined");   
}   
```

## 三、typeOf的用法 
`typeof()`返回的是字符串，有六种可能：number、string、boolean、object、function、undefined。 
当定义了array类型时，返回的是object字符串
另外`alert(typeof null); //output "object" `
 
## 四、Null与Undefined的区别
`undefined`类型只有一个值，即`undefined`。当声明的变量还未被初始化时，变量的默认值为`undefined`。
Null类型也只有一个值，即`null`。`null`用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。

```javascript
var oValue;   
alert(oValue == undefined); 
//结果为true,代表oVlaue的值即为undefined，因为我们没有初始化它。   
  
alert(null == document.getElementById('notExistElement')); 
//结果为true,因为我们尝试获取一个不存在的对象(页面上不存在id为"notExistElement"的DOM节点)。  
  
alert(typeof undefined); //output "undefined"   
alert(typeof null); //output "object" null即是一个不存在的对象的占位符  
  
alert(null == undefined); //output "true"   
//ECMAScript认为undefined是从null派生出来的，
//所以把它们定义为相等的。但是，如果在一些情况下，
//我们一定要区分这两个值，那应该怎么办呢？可以使用下面的两种方法。  
  
//以下可以区分这两种类型  
alert(null === undefined); //output "false"   
alert(typeof null == typeof undefined); //output "false"   
```
## 五、判等 `==`
JS对于变量使用`==`比较时, 对于相同类型的两个标量的比较，除了NaN比较特殊之外（NaN==NaN返回false），都没什么疑问，而对于类型不同的两个标量的比较，JS就有一套严格的规则，这规则JS解析引擎具体怎样执行的，只好对其表现作个总结 
1.将Boolean,Number,String这三种类型进行不同类型的==比较时，其规则是，总将两边的值转换成数字，再看看转换结果数字是否相等 
   
## 六、用 `===` 代替` ==`
JavaScript里有两种不同的判断相等运算符：`===|!== `和`==|!=`。相比之下，前者更值得推荐。因为不仅比较变量值，还要比较变量类型是否一样。在`coffeescript`中就推荐这种写法，`coffeescript`会把`is`编译成`===`, `isnt`编译成`!==`。
如果两个比较对象有着同样的类型和值，`===`返回true，`!==`返回false。
不过，如果使用`==`和`!=`，在操作不同数据类型时, 你可能会遇到一些意想不到的问题。在进行相等判断前，JavaScript会试图将它们转换为字符串、数字或 Boolean量。

## 七、javascript控制页面控件隐藏显示
两种方法, 方法的不同之处在于控件隐藏后是否还在页面上占位
```javascript
// 方法一：
document.all["PanelSMS"].style.visibility="hidden"; 
document.all["PanelSMS"].style.visibility="visible";
//方法二：
document.all["PanelSMS"].style.display="none"; 
document.all["PanelSMS"].style.display="inline";
```
方法一隐藏后 页面的位置还被控件占用 只是不显示 
方法二隐藏后 页面的位置不被占用

## 八、页面刷新
页面刷新方法总结：有时候可能会用到
`window.location.reload()`刷新当前页面.
`parent.location.reload()`刷新父亲对象（用于框架）
`opener.location.reload()`刷新父窗口对象（用于单开窗口）
`top.location.reload()`刷新最顶端对象（用于多开窗口）
