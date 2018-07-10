title: git常用命令总结
date: 2016-01-29 23:33:54
categories: github
---

本文总结了平时开发中常常用到的git命令。

<!-- more -->

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



`git`最强大的功能之一就是分支管理，下面总结下常用的`branch`命令。

## 查看分支

```bash
$ git branch -a # 列出所有分支,包括本地的和remote的
* develop
  master

$ git branch # 只列出本地分支
* develop
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/develop
  remotes/origin/master
```


## 创建分支 git checkout -b [branchname]

我们经常需要基于`master`拉一个分支进行开发，开发完成之后再将代码合并会`master`分支.

```bash
$ git branch testing # 创建一个叫 `testing` 的分支

$ git branch # 列出本地分支，发现我们还在develop分支上
* develop
  master
  testing

$ git checkout testing # 切换到testing分支上
Switched to branch 'testing'

# 上面2个命令，首先创建了一个分支，然后再切换到新的分支上。

$ git checkout -b 'testing2' # 这个命令结合了上面2条命令，创建分支后自动切换到新分支上
Switched to a new branch 'testing2'

# 将本地分支push到远程
$ git push origin testing
```

## 删除分支 git branch -d [branchname]

```bash
$ git branch -d testing2
Deleted branch testing2 (was 3ce3fc3). # 删除成功

# 如果恰巧你当前也在要被删除的分支上，git就会报错：
# error: Cannot delete the branch 'testing2' which you are currently on.

# 删除远程分支
$ git push origin :[branchname]
git push origin :testing
To git@github.com:test/testing.git
- [deleted] testing
# 冒号前面的空格不能少，原理是把一个空分支push到server上，相当于删除该分支
```

## 切换分支 git checkout [branchname]

```bash
$ git checkout testing # 切换到testing分支上
Switched to branch 'testing'
```


## 合并分支（解决冲突）
开发分支是用来开发新功能的，开发完毕后还是要将代码饭和到主分支 `master` 中。

```bash
$ git checkout master # 首先切换到 master 分支
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git merge testing
# git会自动合并，如果有冲突则解决冲突

# 冲突了， 解决冲突的办法是根据terminal的提示一个文件一个文件的修改。
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

## git删除push到远程服务器的commit

如果不小心把不该提交的代码或者敏感的数据（如密码）提交到远程git服务器上，可以使用`git reset`回滚到上一个commit，并且`commit history`不留下任何痕迹。

具体做法：

```bash
# 1.通过找到想要退回到的commit_id
$ git log
# 2.本地回到上一个commit_id
$ git reset --hard <commit_id>
# 3.推送到服务器，一定要加 --force 参数
$ git push origin HEAD:master --force
```


如果不加`--force`参数提交不上去，服务器rejected.
![](http://images2015.cnblogs.com/blog/282019/201509/282019-20150908175619012-1314340411.jpg)

最后你会发现，代码服务器上也不会留下痕迹，完美。