title: Mac下修改环境变量
date: 2015-06-30 10:27:18
categories: mac
---

如果使用默认Bash，
首先修改 `~/.bash_profile` 文件，添加文件路径，比如：

```bash
export PATH=~/bin:/usr/local/bin/node:~/Downloads/software/gradle-1.0/bin/:$PATH
```

然后输入  `source ~/.bash_profile` 使之生效。

如果使用的是 zshell , 编辑 `~/.zshrc` 文件, 然后再 `source ~/.zshrc`  。
