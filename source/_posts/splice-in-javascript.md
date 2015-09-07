title: javascript中的splice方法介绍&示例
date: 2014-10-13 22:55:52
categories: javascript
---

javascript 中的 `splice` 方法很强大，它可以用于插入、删除或替换数组的元素。
下面来一一介绍！

1. 删除：用于删除元素，两个参数，第一个参数（要删除第一项的位置），第二个参数（要删除的项数）
2. 插入：向数组指定位置插入任意项元素。三个参数，第一个参数（其实位置），第二个参数（0），第三个参数（插入的项）
3. 替换：向数组指定位置插入任意项元素，同时删除任意数量的项，三个参数。第一个参数（起始位置），第二个参数（删除的项数），第三个参数（插入任意数量的项）

```javascript
var lang = ["php","java","javascript"];
//删除
var removed = lang.splice(1,1);
alert(lang); //php,javascript
alert(removed); //java ,返回删除的项
//插入
var insert = lang.splice(0,0,"asp"); //从第0个位置开始插入
alert(insert); //返回空数组
alert(lang); //asp,php,javascript
//替换
var replace = lang.splice(1,1,"c#","ruby"); //删除一项，插入两项
alert(lang); //asp,c#,ruby
alert(replace); //php,返回删除的项
```
