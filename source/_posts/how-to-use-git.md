title: 我是如何使用git的
date: 2014-10-19 23:33:54
categories: github
---

## 安装
首先需要安装 `msysgit`,  下载地址：[http://msysgit.github.io/](http://msysgit.github.io/)
`msysgit`提供了`Git Bash`命令行工具和`Git GUI`，前者提供了类似linux系统下bash shell 工具。

![](http://msysgit.github.io/img/git_logo.png)

再安装可视化工具 `tortoisegit`,下载地址： [https://code.google.com/p/tortoisegit/](https://code.google.com/p/tortoisegit/)


安装完之后可能需要手动添加环境变量PATH，通过以下命令确认 `git` 是否安装正确
```bash
$ git --version
```
![](http://images.cnitblog.com/blog/282019/201410/171947165916210)

## 常用命令

`git`常用命令如下：

```bash
# 查看git版本
$ git --version

# 初始化一个git仓库
$ git init

# 添加一个文件到缓存区
$ git add <file>

# 添加所有文件到缓存区
$ git add .

# 提交代码
$ git commit -m 'some comments'
# 如果不加`-m`参数，会自动打开vim编辑器，填写注释。

# 提交之前先从服务器拉一下
$ git pull

# 提交代码
$ git push

# 查看当前所在分支
$ git branch
* develop
   master

# 查看所有分支：
$ git branch --all

# 删除分支
$ git brach -d xxx

# 切换分支（第一次克隆后可以从master分支切换到develop分支）
$ git brach checkout xxx

# 撤销文修改
$ git checkout -- <file>

# 查看git日志
$ gitk

# 合并当前分支到myBranch
$ git merger myBranch

# git修改上一次提交（不小心写错了）
$ git commit --amend
```

## 进阶命令
```bash
# 恢复到某个版本
$ git reset --hard d79bea4e8c5157998eadd3afb803420e24ebc631
$ git reset --hard <Chaged-Id>

# Change-Id可以通过查看log 或者 gitk 得到
$ git log
# 按q退出
```
