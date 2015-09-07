title: jQuery用法小结
date: 2014-11-10 23:43:05
categories: 前端
---

## jQuery DOM 操作
1.使用`html()`方法读取或者设置元素的innerHTML

```javascript
//读取
$("a:first").html();
//设值
$("a:first").html("<h2>hello</h2>");
```

2.使用`text()`方法读取或者设置元素的innerText

```javascript
//读取
$("a:first").text();
//设值
$("a:first").text("hello");
```

3.使用`attr()`方法读取或者设置元素的属性
对于jQuery没有封装的属性用attr操作
```javascript
//读取
$("a:first").attr("href");
//设值
$("a:first").text("href", "http://www.fy98.com/");
```

4.使用 `removeAttr()` 方法删除元素属性
`$("a:first").removeAttr("href");`

5.用`addClass()` 给元素添加样式名， 用`removeClass()`移除样式名
```javascript
//动态添加样式名 class
$("a").addClass("current");
// 移除样式名
$("a").removeClass("current");
//显示元素,相当于添加style='display:block;'
$(this).show();
//隐藏元素,相当于添加style='display:none;'
$(this).hide("slow");
```

##jQuery表单选择器

* $(":input")选取所有 `<input>`, `<textare>`, `<select>`和`<button>`元素
* 和$("input")不一样，$("input")只选取`<input>`
* 多条件选择器
`$("p, div, span.menuitem")` 同时选择p标签、div标签和拥有menuitem样式的span标签，注意选择器表达式中的空格不能多不能少。
* 层次选择器
1. `$("div li")` 获取div下的所有li元素，包括后代、后台的后台等
2. `$("div > li")` 获取div下的直接li子元素
3. `$(".menu + div")` 获取样式名为menu之后的第一个div元素（不常用）
4. `$(".menu ~ div")` 获取样式名为menu之后的所有的div元素（不常用）

## jQuery过滤器
1. `:first` 选取第一个元素。$("p:first")选取第一个p标签
2. `:last` 选取最后一个元素。$("div:last")选取最后一个div标签
3. `not(选择器)` 选取不满足`选择器`条件的元素。$("input: not(.myClass)")选取样式名不是myClass的input标签
4. `:even`、`:odd` 选取索引是奇数、偶数的元素。$("input:even")选取索引是奇数的input标签。
5. `:eq(索引序号)`、`:gt(索引序号)`、`:lt(索引序号)` 选取索引等于、大于或小于索引序号的元素。比如$("li:lt(1)")选取索引小于1的li标签
6. `$(":header")` 选取所有h1至h6的元素
7. `$("div:animated")` 选取所有正在执行动画的div元素
8. 属性过滤选择器
  * `$("div[id]")` 选取所有有id属性的div
  * `$("div[title=test]")` 选取title属性为test的div标签，注意，jQuery中没有对`getElementsByName` 进行封装，用`$("input[name=abc]")` 这样替代
  * `$("div[title!=test]")` 选取title属性不为test的div标签 
9. 表单对象选择器
* `$("#form1 :enabled")` 选取id为form1的表单内所有启用的元素
* `$("#form1 :disabled")` 选取id为form1的表单内所有被禁用的元素
* `$("input:checked")` 选取所有选中的元素，如radio、checkbox等
*  `$("select:seleced")` 选取下拉列表中所有被选中的元素

##jQuery中的回调
1. 没有参数的回调
* `$.get("page.html", myCallBack);` 当get请求完成后调用myCallBack方法
2. 有参数的回调
* `$.get("page.html", function(){myCallBack(param1, param2)});` 带参数的方法要用匿名函数包起来。


