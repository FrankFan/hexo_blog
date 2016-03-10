title: git进阶
date: 2016-01-29 23:33:54
categories: github
---

## 多出来的commit
Git从将远程分支与本地分支合并可以有两种方式，一种是 `git pull`, 另一种是 `git fetch + git rebase`.
区分在于 `git pull` 是把远程分支代码拉下来，与本地分支进行merge操作，相当于`git fetch + git merge`；
所以使用`git pull`命令之后，会自动多出来一次merge的commit，从`git log`上面看到的情况就是多了一次commit, 而且git树也不那么整洁了。
推荐的做法是使用rebase而不是pull, 可以`git fetch ; git rebase` ，也可以`git pull —rebase`.

## tag 管理

```bash
# 查看tag
$ git tag | grep dev_20150525
# 创建tag
$ git tag dev_20150525_16 -m 'comment'
# 把tag push到远程
$ git push origin dev_20150525_16
$ git push origin --tags

Counting objects: 1, done.
Writing objects: 100% (1/1), 156 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:FrankFan/fxxxk.git
 * [new tag]         test_tag1 -> test_tag1

# 删除tag 本地删除
$ git tag -d test_tag1

# 删除远程的tag:推一个空的上去
#有的gitlab没有删除远程tag的权限
$ git push origin :refs/tags/reg_201050709_01
```


## git stash 暂存

```bash
# 缓存到暂存区
$ git stash
# 取出来
$ git stash pop
# 查看暂存列表
$ git stash list
# 清空
$ git stash clear
```

注意： `stash` 尽量少用，最好只缓存一次，不然顺序会搞不好弄乱的。

## 添加一个忽略文件到 gitignore 

```bash
$ git rm --cached your_ignored_file
```

## 一个好看的git log
默认 `git log` 样式不太好看，用 alias 换成一个比较好看的：

```bash
$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blu
e)<%an>%Creset' --abbrev-commit"
```

