title: javascript中数组揭秘
date: 2014-10-13 22:58:14
categories: javascript
---

js中的数组很强大，不仅仅是一个数组，更是一个无所不能的集合。

## 创建
可以使用 `数组字面量` 方式创建：
`var arr = []`
或者
`var arr = new Array()`

## 添加元素
```javascript
arr.push(item); // 将一个或多个新元素添加到数组结尾，并返回数组新长度

arr.unshift(item); // 将一个或多个新元素添加到数组开始，数组中的元素自动后移，返回数组新长度

arr.splice(insertPos,0,item1); // 将一个或多个新元素插入到数组的指定位置，插入位置的元素自动后移，返回""
```

## 删除元素
```javascript
arr.pop() // 移除最后一个元素并返回该元素值

arrayObj.shift(); //移除最前一个元素并返回该元素值，数组中元素自动前移

arrayObj.splice(deletePos,deleteCount); //删除从指定位置deletePos开始的指定数量deleteCount的元素，数组形式返回所移除的元素
```

## 访问元素
```javascript
var getArrValue = arr[0]; // 通过索引获取数组的值

arr[1] = "new value"; // 给数组元素赋值
```

## 数组排序
```javascript
arrayObj.reverse(); //反转元素（最前的排到最后、最后的排到最前），返回数组地址

arrayObj.sort(); //对数组元素排序，返回数组地址
```

## 数组元素的字符串化
```javascript
arr.join(separator); //返回字符串，这个字符串将数组的每一个元素值连接在一起，中间用 separator 隔开。

toLocaleString 、toString 、valueOf：可以看作是join的特殊用法，不常用
```

## 数组的拷贝
```javascript
arr.slice(0); //返回数组的拷贝数组，注意是一个新的数组，不是指向

arr.concat(); //返回数组的拷贝数组，注意是一个新的数组，不是指向
```

## 数组的截取和合并
```javascript
arr.slice(start, [end]); //以数组的形式返回数组的一部分，注意不包括 end 对应的元素，如果省略 end 将复制 start 之后的所有元素

arr.concat([item1[, item2[, . . . [,itemN]]]]); //将多个数组（也可以是字符串，或者是数组和字符串的混合）连接为一个数组，返回连接好的新的数组
```
