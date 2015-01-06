title: 用CSS画三角形
date: 2014-11-20 23:44:41
categories: css
---

作为一个不太会写CSS的`伪前端`来说，用纯CSS画各种形状是一件很牛X的事情，今天就先画一个三角形吧。

最终效果图：
![](http://images.cnitblog.com/blog/282019/201412/041937581088177)

html:

```html
<div class="triangle">
</div>
```

css:

```css
.triangle{
    width: 0;
    height: 0;
    border-width: 30px;
    border-style: solid;
    border-color: transparent rgba(0,0,0,0.6) rgba(0,0,0,0.6) transparent;
}
```

### 说明
html部分很简单，就一个div；
css部分定义宽度和高度都为0，border宽度是30px并且border-style是实心的div，
其中最重要的是最后一句，也是最关键的一句，`border-color`属性的四个参数分别定义了边框的`上-右-下-左`（顺时针）的样式，
上、左是透明的，下、右使用rgba定义了黑色且透明度为0.6的颜色。

同理， 可以修改`border-clor`属性画出各种形状：
![](http://images.cnitblog.com/blog/282019/201412/042013314983349)