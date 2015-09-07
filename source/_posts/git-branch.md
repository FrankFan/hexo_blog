title: 关于 git branch 命令
date: 2015-05-01 23:11:08
categories: github
---

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
