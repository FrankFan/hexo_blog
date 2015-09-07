title: 在git中集成beyond compare进行文件diff和merge(windows环境)
date: 2015-01-11 23:14:05
categories: github
---

### 一、首先安装 `beyond compare`
`beyond compare`官方地址 [http://www.scootersoftware.com/support.php?c=kb_vcs.php](http://www.scootersoftware.com/support.php?c=kb_vcs.php)，里面有详细的介绍（可能有墙，请自备梯子）
这个链接是墙内的下载地址：[http://rj.baidu.com/soft/detail/16703.html](http://rj.baidu.com/soft/detail/16703.html)

### 二、修改.gitconfig配置文件
```bash
$ subl ~/.gitconfig #打开用户home目录下的配置文件
```
添加配置节点：
```bash
[diff]
    tool = bc3
[difftool "bc3"]
    cmd = \"/d/Program Files (x86)/Beyond Compare 4/BComp.exe\" \"$LOCAL\" \"$REMOTE\"
[difftool]
    prompt = false
[merge]
    tool = bc3
[mergetool "bc3"]
    cmd = \"/d/Program Files (x86)/Beyond Compare 4/BComp.exe\" \"$LOCAL\" \"$REMOTE\" \"$BASE\" \"$MERGED\"
    trustExitCode = true
```

### 三、使用
当项目中有文件变动时，就可以使用`git difftool`命令来查看，解决冲突时使用`git mergetool`解决冲突。
```bash
$ git difftool
$ git mergetool
```

