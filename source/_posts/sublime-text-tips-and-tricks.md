title: sublime text 常用快捷键设置&插件推荐
date: 2014-12-15 00:15:17
categories: 前端
---

## 安装
推荐安装`sublime text 2`， 3还是beta版，使用过几次感觉略卡顿。
官网 [http://www.sublimetext.com/](http://www.sublimetext.com/)

## 安装 `Package Control`
`package control`是sublime安装插件包的管理工具，安装方法如下：
1.`ctrl + ~` : 呼出控制台
2.在控制台输入一下代码
```python
import urllib2,os; pf='Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read()); print('Please restart Sublime Text to finish installation')
```
3.确认安装成功
快捷键`ctrl+shift+P`打开Package Contrl，说明成功了
![](http://images.cnitblog.com/blog/282019/201309/20231253-b4d749b6657048a190d516f70ba7417e.png)

如果是`sublime text 3`, 安装`package control`代码如下：
```python
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = 
sublime.installed_packages_path(); urllib.request.install_opener( 
urllib.request.build_opener( urllib.request.ProxyHandler()) ); 
open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 
'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

## 插件推荐
1.输入法跟随
在win7 64bit操作系统遇到 “搜过输入法不跟随光标，选词框总在屏幕最下方” 的问题,原因可能是Sublime Text的bug，并非输入法的bug；解决办法：安装IMESurpport插件即可。
1)`ctrl+Shift+P` 呼出 `Package Control`，
2)输入`Install Package`，等待片刻，
3)然后`IMESurport`，就可以安装好了。
![](http://images.cnitblog.com/blog/282019/201309/24111720-ed58ca912c66425ca39770105e18aff7.jpg)

2.中文支持
如果遇到使用sublime text打开中文文件出现乱码的情况，可以尝试安装`ConvertToUTF8` 和  `GBK Encoding Support` 这2个插件。

3.格式化js

4.格式化html

5.`Emmet`
前端开发必备神插件，安装后使用得当可极大的提高书写html的效率。
粗略介绍如下:
1) 在空白文件中输入`html:5`后，按快捷键`ctrl+E`, `Emmet`会自动生成一段标准的html5代码片段：
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
</body>
</html>
```

2)输入html标签时可以省略大小括号，例如：
输入 `div` 然后按`tab`键，就可以得到
```html
<div></div>
```
3) 原理同上，可以给标签后面加上id名或者class名，如
```html
输入： div#container + tab
得到：<div id="container"></div>

输入： div.wrap + tab
得到： <div class="wrap"></div>
```

4)下级标签， 如：
```html
输入： ul>li + tab
得到：
<ul>
	<li></li>
</ul>

输入： ul>li*5
得到：
<ul>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
</ul>
```

更详细使用方法参考官方指南：[http://docs.emmet.io/](http://docs.emmet.io/)

## 常用快捷键推荐

`$ subl .`在控制台终端中快速打开文档或者目录
`start .` 在控制台终端中迅速打开`File Explorer`
`pushd path`  更改目录
`ctrl + shift + D`: 复制当前行
`ctrl + enter` : 在当前行下一行插入光标
`ctrl + D`: 选择一个单词，配合使用 `ctrl + K + D`，可以实现多游标选择器。
`alt + F3`列选择
`shift + alt + 2`:把编辑区域分成左右2块（3、4其他同理）
`ctrl + K + B` : toggle side bar


## 自定义快捷键
细心的你一定发现sublime没有`全部保存`的快捷键，也没有一个GUI按钮可以点击，这就需要我们自定义添加一个全部保存的快捷键了，步骤：

打开 `Preferences` ->  `Key Binding` - `User` 文件，添加快捷键为：
[
     { "keys": ["ctrl+q"], "command": "close_all" },
     { "keys": ["ctrl+shift+s"], "command": "save_all" }
]

这时候我们就可以通过 `ctrl+shift+s` 保存所有文件了，很高效有木有……
同理可以实现一键关闭所有文件 `ctrl + q`
关闭单个标签 `ctrl + w`


![](http://images.cnitblog.com/blog/282019/201412/142029584622910)
