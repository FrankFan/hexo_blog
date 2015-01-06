title: 给 gerrit 设置 code reviewer快捷键
date: 2014-12-05 14:10:36
categories: github
---

`gerrit` 提供了一种`code review`解决方案，但每次代码提交之后都要设置每个commit的`code review`， 命令行中输入那么长的命令实在是痛苦，
`gerrit` 提供了一种快捷键的方式进行code review

命令行中痛苦的做法：
```bash
-- 可加多个code reviewer
git push origin HEAD:refs/for/develop%r=yp_liu,%r=y.fan
```

机智的做法, 修改项目根目录`.git/config`文件：
```bash
[remote "test"]
    pushurl = ssh://account@code.ctripcorp.com:29418/project_name
    push = HEAD:refs/for/develop
    receivepack = git receive-pack --reviewer testA

[remote "testM"]
    pushurl = ssh://account@code.ctripcorp.com:29418/project_name
    push = HEAD:refs/for/master
    receivepack = git receive-pack --reviewer testB

[remote "testR"]
    pushurl = ssh://account@code.ctripcorp.com:29418/project_name
    push = HEAD:refs/for/release/v4.1
    receivepack = git receive-pack --reviewer testC
```
然后使用 `git push test` 就可以了。

![](http://images.cnitblog.com/blog/282019/201412/081652507121202)
