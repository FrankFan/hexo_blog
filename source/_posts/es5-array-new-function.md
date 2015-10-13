title: ECMAScript5 Array新增方法
date: 2015-09-23 19:30:05
categories: javascript
---

ECMAScript5标准发布于2009年12月3日，它带来了一些新的，改善现有的Array数组操作的方法。
如果不考虑兼容性的话可以大面积使用了。

在ES5中，Array一共有9个方法：

```javascript
Array.prototype.indexOf
Array.prototype.lastIndexOf
Array.prototype.every
Array.prototype.some
Array.prototype.forEach
Array.prototype.map
Array.prototype.filter
Array.prototype.reduce
Array.prototype.reduceRight
```


## 1. .indexOf(element) / .lastIndexOf(element)
`indexOf`方法返回元素在数组中的第一个位置的索引，如果不存在返回"-1"

不使用`indexOf`时:

```javascript
var arr = ['apple','orange','pear'],
    found = false;

for(var i = 0, length = arr.length; i < length; i++) {
    if (arr[i] === 'orange') {
        found = true;
    }
}

console.log('found orange :' + found);
```


使用`indexOf`方法后：

```javascript
var arr = ['apple','orange','pear'];
console.log('found orange : ',  arr.indexOf('orange') != -1);
```


## 2. .filter(function(element))

filter方法创建一个一个新的匹配过滤条件的数组，返回数组的一个子集，回调函数用于逻辑判断是否返回，返回true则把当前元素加入到返回数组中，false则不加，新数组只包含返回true的值，索引缺失的不包括，原数组保持不变.

```javascript
var arr = new Array(1, 2, 3, 4, 5, 6);

var newArr = arr.filter(function(e){
    return e % 2 == 0;
});

console.log(newArr); // [ 2, 4, 6 ]
console.log(arr); //[1, 2, 3, 4, 5, 6]
```


再举个例子，不使用filter时：

```javascript
var arr = [
    {"name":"apple", "count": 2},
    {"name":"orange", "count": 5},
    {"name":"pear", "count": 3},
    {"name":"orange", "count": 16},
];
    
var newArr = [];

for (var i = 0, l = arr.length; i < l; i++) {
    if (arr[i].name === "orange") {
        newArr.push(arr[i]);
    }
}

console.log("Filter results:", newArr);
```

使用filter后：

```javascript
var arr = [
    {"name":"apple", "count": 2},
    {"name":"orange", "count": 5},
    {"name":"pear", "count": 3},
    {"name":"orange", "count": 16},
];

var newArr = arr.filter(function(item){
    return item.name === "orange";
});
console.log("Filter results:",newArr);
```

## 3. .forEach(element,index,array)

遍历数组，参数为一个回调函数，回调函数有三个参数：当前元素，元素索引，整个数组。
为每一个元素执行对应的回调方法。 `forEach` 是用来替换 `for` 、和 `for in` 循环的。

```javascript
var arr = [1,2,3,4,5,6,7,8];

// 普通for循环
for(var i= 0, l = arr.length; i< l; i++){
    console.log(arr[i]);
}

// forEach 迭代
arr.forEach(function(item,index){
    console.log(item);
});

// 给数组中的每个元素加1
var a = new Array(1, 2, 3, 4, 5, 6);
a.forEach(function(e, i, array) {
    array[i] = e + 1;
});
console.log(a); //[2, 3, 4, 5, 6, 7]
```


## 4. .map(function(element))

`map()`对数组的每个元素进行一定操作（映射）后，会返回一个新的数组。
与`forEach`类似，遍历数组，回调函数的返回值组成一个新的数组，新数组的索引结构和原数组一致，原数组保持不变。


不使用`map()`

```javascript
var oldArr = [
    {
        first_name: "Colin",
        last_name: "Toh"
    }, 
    {
        first_name: "Addy",
        last_name: "Osmani"
    }, 
    {
        first_name: "Yehuda",
        last_name: "Katz"
    }];

function getNewArr() {

    var newArr = [];

    for (var i = 0, l = oldArr.length; i < l; i++) {
        var item = oldArr[i];
        item.full_name = [item.first_name, item.last_name].join(" ");
        newArr[i] = item;
    }

    return newArr;
}

console.log(getNewArr());

```

使用`map()`后：

```javascript
var oldArr = [
    {
        first_name: "Colin",
        last_name: "Toh"
    }, 
    {
        first_name: "Addy",
        last_name: "Osmani"
    }, 
    {
        first_name: "Yehuda",
        last_name: "Katz"
    }];

function getNewArr() {

    return oldArr.map(function(item, index) {
        item.full_name = [item.first_name, item.last_name].join(" ");
        return item;
    });
}

console.log(getNewArr());


// 再举个例子：
var a = new Array(1, 2, 3, 4, 5, 6);
var newArr = a.map(function(e) {
    return e * e;
});
console.log(newArr); // [1, 4, 9, 16, 25, 36]
console.log(a); //[1, 2, 3, 4, 5, 6]
```


## 5. .reduce(function(v1,v2),value) / .reduceRight(function(v1,v2),value)

todo...




