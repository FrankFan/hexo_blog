title: 几行代码瞬间提升Sublime Text的效率
date: 2015-12-12 22:16:21
categories: mac
---


### 增加关闭所有标签功能

打开 `Sublime Text` -> `Preferences` -> 'Key Bindings - User', 加入一行自定义快捷键：

```js
[
    { "keys": ["ctrl+q"], "command": "close_all" }
]
```

![](http://images2015.cnblogs.com/blog/282019/201601/282019-20160112223804553-1174840545.gif)


### 修改用户设置

打开 `Sublime Text` -> `Preferences` -> 'Settings - User', 加入：

```js
{
    // 滚动到底
    "scroll_past_end": true,
    // 双击选中又横杠(中划线)连接的单词
    "word_separators": "./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?"
}

```

![](http://images2015.cnblogs.com/blog/282019/201601/282019-20160112223221460-1412191457.gif)