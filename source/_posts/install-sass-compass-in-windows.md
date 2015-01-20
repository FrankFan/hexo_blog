title: windows下安装ruby/sass/compass
date: 2015-01-05 21:57:22
categories: 前端
---

### 认识SASS/Compass
ruby不用说了吧，大家都知道，是一种程序语言，可以用来写server端代码。

SASS是对CSS的预处理器，提供了许多便利的写法，它具有某些编程的思想（比如变量、嵌套、函数、运算等等），通过它再生成相应的CSS，使得CSS的开发，变得简单和可维护。而Comapss是基于SASS的一个库，Compass相对于SASS的关系大致相当于 JQuery：JS的关系。

### 安装
SASS是依赖于Ruby的，因此在安装SASS之前，必须先在Windows内安装Ruby。

早就听说windows下安装ruby是非常非常费时，我还不信这个邪尝试了一把，果然用从官网下载的安装包安装以后测试是失败的。

[https://www.ruby-lang.org/zh_cn/](https://www.ruby-lang.org/zh_cn/)
[https://www.ruby-lang.org/zh_cn/downloads/](https://www.ruby-lang.org/zh_cn/downloads/)
[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)

最后使用rubyinstaller一键安装成功了。

在控制台确认是否安装成功

```bash
$ ruby -v
ruby 2.1.5p273 (2014-11-13 revision 48405) [x64-mingw32]
```

如果不出错的话应该能够得到Ruby的版本号。到这里，我们已经可以接着安装SASS/Compass环境了。

Ruby环境内有个包管理器——GEM，它类似于Nodejs下的NPM，它随着Ruby一起被安装，因此不需要额外安装。啰嗦到这里，是因为sass和compass都是基于Ruby的包，一会儿我们安装Compass/SASS时会用到它。

可以先使用命令看一下自带了哪些gem包
`$ gem list`

安装sass
`$ gem install sass`

如果你在中国，第一次安装往往是不成功的，你应该被墙了……
默认ruby会去http://rubygems.org/ 下载 gem， 这个网站被GFW墙了，我们可以使用淘宝的国内镜像站点http://ruby.taobao.org/来解决。

`$ gem sources -a http://ruby.taobao.org/`

这次应该安装成功了，你可以使用`gem list`来确认。

安装compass
`$ gem install compass`


安装成功，这时候在项目中执行`grunt server`就可以使用sass命令了。


更多请参考：[这里](http://www.html-js.com/article/CSS-solves-the-installation-and-debugging-of-SASSCompass-scheme)