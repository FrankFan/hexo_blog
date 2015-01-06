title: Javascript中string方法
date: 2014-10-25 18:51:50
categories: javascript
---

## string.charAt(num)

- 返回某个指定索引处的字符
- 索引从0开始

```javascript
var str = "jQuery is good";
var   n = str.charAt(2);

//output will be "u"
```

## string.indexOf(searchValue, [start])

- 返回字符串中某个搜索字符首次出现的索引位置
- 索引从0开始
- 如果没有找到则返回 -1
- 该方法大小写敏感(case-sensitive)

```javascript
var str = "Hello world, welcome to my blog.";
var n   = str.indexOf("welcome");

//output will be 13
```

## string.lastIndexOf(searchValue, [start])

- 返回字符串中某个搜索字符串最后一次出现的索引位置
- 搜索从后往前执行，但是返回的索引是从索引0处开始往后计数的
- 如果没有找到则返回 -1

```javascript
var str = "welcome to this beautiful world.";
var n   = str.lastIndexOf("this");

//Output will be 11
```

## string.concat(string1, string2, .., stringX)

- concat 用来拼接2个或多个字符串
- 该方法不会改变已有的字符串，而是返回一个新的拼接后的字符串

```javascript
var str1 = "welcome to this beautiful world.";
var n   = str.lastIndexOf("this");

//Output will be 11
```

## string.substr(start, [length])

substr()方法用来提取字符串部分， 从指定位置开始返回指定个数的字符。

```javascript
var str = "Hello world!";
var n   = str.substr(2,3);

//output will be "llo"
```

## string.substring(from, [to])

substring()方法用来截取字符串，返回一个新的字符串。该方法从from开始截取，到to为止，不包括to

```javascript
var str = "Hello world!";
var n   = str.substring(2,3);

//output will be "l"
```

## string.toLowerCase()

将字符串转化成小写字母

```javascript
var str = "Hello world!";
str = str.toLowerCase();

//output will be "hello world!"
```

## string.toUpperCase()

将字符串转化成大写字母

```javascript
var str = "Hello world!";
str = str.toLowerCase();

//output will be "HELLO WORLD!"
```

## string.search(searchvalue)

search()方法参数可以是一个字符串或者正则表达式， 返回匹配的索引。
如果没有找到则返回-1

```javascript
var str = "Hello world!";
str = str.search("wo");

//output will be 6
```

## string.replace(searchvalue, newvalue)

replace()方法搜索一个指定的字符串或者正则表达式，返回一个新的被替换后的字符串。

```javascript
var str = "Hello world!";
str = str.replace("Hello", "Welcome to this");

//output will be "Welcome to this world!"
```

##string.match(regexp)

```javascript
var str = "The rain in SPAIN stays mainly in the plain";
var n   = str.match(/ain/g);

//output will be "ain,ain,ain"
```

## string.slice(start, [end])

- 返回被截取的字符串

```javascript
var str = "hello world.";
var n   = str.slice(6, 11);

//output will be "world"
```
