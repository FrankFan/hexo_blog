title: CSS网页布局基础
date: 2014-11-30 11:23:31
categories: css
---

##CSS基础

网页布局分类
1. 流式布局
2. 浮动布局
3. 绝对定位布局

需要理解：
* 标准文档流
* 盒子模型
* float属性
* position属性

W3C标准是指由万维网联盟指定的一系列标准，包括：
* 结构化标准语言（HTML和XML）
* 表现标准语言（CSS）
* 行为标准语言（DOM和ECMAScript）

W3C倡导结构、样式和行为分离。

在CSS中，存在3中定位机制：
1. 标准文档流（Normal flow）
2. 浮动（Floats）
3. 绝对定位（Absolute positioning）


标准文档流
特点：
从上到下、从左到右输出文档内容，
由块级元素和行级元素组成，可以实现一列布局。

块级元素的特点是：
从左到右撑满页面，独占一行；
触碰到页面边缘时，会自动换行。

常见的块级元素有 div、ul、li、dl、dt、p 等

行级元素的特点：
能在同一行内显示，
不会改变HTML文档结构

常见的行级标签有 span、strong、img、input 等

块级元素和行级元素都是盒子模型。

盒子模型是网页布局的基石，盒子模型由4部分组成：
* 边框（border）
* 外边距（margin）
* 内边距（padding）
* 内存（content）

![](http://images.cnitblog.com/blog/282019/201412/061903416238106)

盒子模型属性设置4个值时表示 上-右-下-左 ，
设置3个值表示 上-左右-下
设置2个值表示 上下-左右
设置1个值表示 上下左右

CSS优先级采用`就近原则`：行内样式 > 内部样式 > 外部样式


## 浮动布局

### 理解浮动
float是CSS中规定的第二种定位机制，能够实现横向多列布局。
`float: left | right | none`, 浮动的特点是元素会左移或者右移，
知道触碰到容器边缘为止。

注意：设置了浮动的元素，仍旧处于标准文档流中，也就意味着它仍旧
占据着标准文档流中的空间，会影响到其他（特指紧挨着浮动元素的后一个元素）元素的布局。

### 清除浮动

方法1：
`clear: left | right | both`属性, 常用 `clear: both;`

方法2：
为元素同时设置 `width: 100%` 或者固定宽度 + `overflow:hidden;`

### 案例：横向两列布局
主要技能：
* float属性——使纵向排列的块级元素，横向排列
* margin属性——设置两列之间的间距

html
```html
<body>
	<div id="wrap">
		<div id="header">头部</div>
		<div id="mainbody">
			<div class="left"></div>
			<div class="right"></div>
		</div>
		<div id="footer">版权部分 copyright 2014</div>
	</div>
</body>
```

css
```css
*{ margin: 0; padding: 0;}
#wrap{background: #00C; margin: 0 auto; width: 960px;}
#header{background: #FF3300; width: 100%;}
#mainbody{background: #FC0; width: 100%; overflow: hidden;}
.left{width: 800px; height: 200px; background: #000; float: left;}
.right{width: 140px; height: 500px; background: #690; float: right;}
#footer{background-color: #639; width: 100%;}
```

效果图：
![](https://ws4.sinaimg.cn/large/006tNc79gy1fsbyq83lbnj30qo0exdfn.jpg)
