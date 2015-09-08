title: Mac OS X 安装ruby环境
date: 2015-05-27 20:22:01
categories: mac
---

1.查看版本
```shell
$ ruby -v
ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin14]
```

2.查看源
```shell
$ gem source -l
*** CURRENT SOURCES ***

https://rubygems.org/
```

3.更换源
```shell
$ gem source -r https://rubygems.org/

https://rubygems.org/ removed from sources
```

4.添加源

```shell
$ gem source -a https://ruby.taobao.org
```

5.安装compass

```shell
$ sudo install comopass

$ compass -v
Compass 1.0.3 (Polaris)
Copyright (c) 2008-2015 Chris Eppstein
Released under the MIT License.
Compass is charityware.
Please make a tax deductable donation for a worthy cause: http://umdf.org/compass
```