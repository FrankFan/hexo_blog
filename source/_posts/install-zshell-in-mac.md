title: Mac 下安装zshell
date: 2015-07-08 13:17:01
categories: mac
---

## 什么是shell
操作系统是内核(core), 与操作系统通信的一层是壳，就是shell.
大多数命令行用户接触最多的是 `shell` 是 `Bash`，因为Bash是各个版本操作系统(Linux&Mac)的默认shell,  除此之外，还有很多其他的shell可以选择。

查看当前使用的shell
```bash
$ echo $SHELL
```

查看系统所支持的shell
```bash
$ cat /etc/shells

/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

## 切换默认shell
```bash
$ chsh -s /bin/zsh
```

## 安装 on-my-shell
- wget

确保安装了wget，使用

`wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh`

- 手动安装

确认安装了git，使用git clone

`git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc`

这时候我查看~/.zshrc，里面用了默认的主题`robbyrussell`,还可以设置alias, 配置插件等等。

## 参考
http://macshuo.com/?p=676
https://github.com/robbyrussell/oh-my-zsh
http://ohmyz.sh/
http://www.open-open.com/lib/view/open1394763235862.html
http://www.cnblogs.com/growingkata/p/3734994.html