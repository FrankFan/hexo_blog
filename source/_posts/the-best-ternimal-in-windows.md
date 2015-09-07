title: windows下使用体验更好的控制台——ConsoleZ
date: 2014-10-18 23:19:24
categories: 前端
---

转做前端开发以来，每天使用最频繁的工具就是控制台了，`git`提交代码要用，`npm`安装node包也要用，`grunt` 运行 task 也要用，可是系统自带的`cmd`太难用，有界面丑，字体丑，不能最大化等等问题，
那么问题就来了：

> "windows 下 Terminal哪家强？"

推荐一款代替 `cmd.exe` 和 `Git Bash` 的windows平台下的终端工具——`ConsoleZ`。
完全可以替代windows自带的`cmd.exe`和`Git Bash`，可以更换字体、缩放字体、更改背景色或背景图片、设置透明度、复制+粘贴更不在话下，大大提升工作效率，写代码心情也更好了。

据江湖传言，`ConsoleZ`的前身是[Console2](http://sourceforge.net/projects/console/)，由于长期不更新，一牛人在此基础上重新开发了[ConsoleZ](https://github.com/cbucher/console)

下载地址： [https://github.com/cbucher/console/wiki/Downloads](https://github.com/cbucher/console/wiki/Downloads)


P.S.  Mac党、Linux党请飘过~

先来一张全图看看：
![](http://images.cnitblog.com/blog/282019/201410/171840464663450)

## 配置ConsoleZ

### 颜色

选择一种赏心悦目的颜色，再加上适当的半透明，使`ConsoleZ`看起十分舒服。

背景色：rgb(46, 52, 54)
字体： Consolas
大小：13px


![](http://images.cnitblog.com/blog/282019/201410/171843347019752)

![](http://images.cnitblog.com/blog/282019/201410/171844042639186)

![](http://images.cnitblog.com/blog2015/282019/201504/071832381963112)

### 快捷键

- 选择文本：`Shift + Left Mouse`
- 选择一个单词：`Shift + Double Click`
- 放大字体：`Ctrl + Num +`
- 缩小字体：`Ctrl + Num -`
- 还原大小：`Ctrl + 0`
- 全屏：`F11`
- 粘贴：`Shift + Insert`
- 新建一个Tab：`Ctrl + F1` 这个姿势不适合一只手操作，我改成了`Ctrl + T`，其实大部分快捷键和`Chrome`一样
- 多标签从左到右一次切换：`Ctrl + Tab`
- 多标签精确切换：`Ctrl + 1`、`Ctrl + 2`等等

### 与 git bash 集成
Shell: "D:\Program Files (x86)\Git\bin\sh.exe" --login -i
Startup dir: 项目目录地址

![](http://images.cnitblog.com/blog/282019/201410/171844322326609)


## Q & A

- 如何显示中文?
可参考github repo 中的 issue,  [https://github.com/cbucher/console/issues/172](https://github.com/cbucher/console/issues/172)

- 如何输入中文?
设置-Styles-Integrated IME 
前提是`git bash`配置好了关于中文的支持项。