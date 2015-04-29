title: max os x 中使用subl命令
date: 2015-04-22 20:12:09
categories: mac
---

[官方文档](https://www.sublimetext.com/docs/3/osx_command_line.html)

按照官方文档执行命令：

`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`

极可能遇到这种问题，
`ln: /usr/local/bin/subl: No such file or directory`

原因其实很明显， 就是没有这个文件或目录，
解决办法是手动新建一个bin目录即可。

### 第一步 新建目录

`mkdir /usr/local/bin`

### 第二步 创建链接

然后执行链接命令， 接着编辑 ~/.bash_profile 文件，

```shell
export PATH=/usr/local/bin:$PATH
export EDITOR='subl -w'
```

### 第三步 使环境变量生效

最后使环境变量生效：
`$ source ~/.bash_profile`

最后在terminal中任意目录执行 `subl .` 就会打开sublime text. 

参考
http://my.oschina.net/VincentJiang/blog/184108
http://www.phodal.com/blog/mac-os-command-line-sublime/
