title: git flow 简介
date: 2014-11-02 22:47:31
categories: github
---

## 介绍

使用git开发进行分支管理功能确实比TFS、SVN方便许多，推荐大家使用分支来做开发。git branch 虽然功能强大但是在团队开发中使用不当反而会降低工作效率，在这种情况下有牛人开发整理出一套比较好的方案 A successful Git branching model 来规范代码版本管理流程。

git flow 是规范化使用git branch 的一套方案来管理分支，规范代码流程。

## 安装
下载地址： [http://files.cnblogs.com/fanyong/gitflow_to_git_bin.7z](http://files.cnblogs.com/fanyong/gitflow_to_git_bin.7z)
解压缩后放在git安装目录中的bin目录下。

![](https://ws2.sinaimg.cn/large/006tNc79gy1fsbyvgntomj307207tmx1.jpg)

## 使用
第一次使用先初始化，它会问你一系列问题，蛋定，一般采用默认参数一路回车即可。

```bash
$ git flow init

Which branch should be used for bringing forth production releases?
   - master
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
```

每个项目都有2个分支，master和develop分支，master分支是主分支，保证程序有一个稳定的版本，和线上代码是同步的 ； develop分支则是开发使用的分支，几乎所有的功能开发都要在该分支上进行。
简单来说， git branch 把 branch 分成了2个主要分支 和 3个临时辅助分支：

![](https://ws1.sinaimg.cn/large/006tNc79gy1fsbyvp73y7j30gz0mn77y.jpg)

### 主要分支
* master分支：永远处在即将发布（production-ready）状态
* develop分支：最新的开发状态

### 辅助分支
* feature分支：开发新功能的分支，基于develop，开发完成后merge回develop
* release分支：准备要发布版本的分支（测试环境用的），用来修复SIT bug；基于develop分支，完成后merge回develop和master分支
* hotfix分支：修复线上（master）紧急bug，等不及release分支就必须马上上线；基于master分支，完成后merge回master和develop分支。

### 新建feature分支
完成 `git flow init` 后当前所在分支就变成 develop. 任何开发都必须从 develop 开始。
开始开发一个新的功能点：
```bash
$ git flow feature start some_awesome_feature
# ... 开发 完成后 ...
$ git flow feature finish some_awesome_feature
```
最后一条命令会把 `feature/some_awesome_feature` 合并到develop分支，然后删除feature分支。

```bash
$ git flow feature start td
Switched to a new branch 'feature/td'

Summary of actions:
- A new branch 'feature/td' was created, based on 'develop'
- You are now on branch 'feature/td'

Now, start committing on your feature. When done, use:

     git flow feature finish td

$ git add .
$ git commit -m 'update a new feature'

# finish 
$ git flow feature finish td
Switched to branch 'develop'
Updating 85a4e89..b2740da
Fast-forward
 CampusAmbassador.Task.Web/Scripts/crop.js | 8 +++++++-
 1 file changed, 7 insertions(+), 1 deletion(-)
Deleted branch feature/td (was b2740da).

Summary of actions:
- The feature branch 'feature/td' was merged into 'develop'
- Feature branch 'feature/td' has been removed
- You are now on branch 'develop'
```

### 管理release分支
新建并且把一个release分支推送到远程服务器：
```bash
$ git flow release publish release1.0
```
组内其他成员在 release1.0上继续开发或者修改测试环境的bug
```bash
$ git flow releas track release1.0
```
当你的功能点都完成时（需要发布新版本了），就基于develop创建一个发布(release)分支
```bash
$ git flow release start v1.0
$ git flow releaes finish v1.0
```
当你在完成（finish)一个发布分支时，它会把你所作的修改合并到master分支，同时合并回develop分支，所以，你不需要担心你的master分支比develop分支更加超前。

### hotfix分支
最后一件让git-flow显得威武的事情是它处理热修复（即时的BugFix）的能力，你可以像其他分支一样地创建和完成一个热修复分支，区别是它基于master分支，因此你可以在产品出现问题时快速修复，然后通过”finish”命令把修改合并回master和develop分支。
如果线上出现bug需要紧急修复，就可以使用hotfix分支
```bash
$ git flow hotfix start fixbug
# ... bug fixed ...
$ git flow hotfix finish fixbug
```
最后一条命令会把 `hotfix` 合并到master和develop分支上，然后删除hotfix分支。
