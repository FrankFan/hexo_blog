title: git删除push到远程服务器的commit
date: 2015-09-01 18:01:20
categories: github
---

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