title: 解决github连接出现 "port 22 Bad file number" 问题
date: 2014-12-20 15:52:54
categories: github
---

趁周末休息来图书馆静下心来看看书，写写自己的代码，可是在执行 `git pull` 时却出现了 `ssh: connect to host github.com port 22: Bad file number` 的问题，仔细一想，很有可能是图书馆把ssh的22端口禁用掉了，一查发现还真是这样。

![](https://ws4.sinaimg.cn/large/006tNc79gy1fsbyr7ml90j30i504z74d.jpg)

![](https://ws4.sinaimg.cn/large/006tNc79gy1fsbys9l2g9j30pb07ita4.jpg)

### 解决办法

1）在用户根目录(`cd ~/.ssh`)下的`.ssh`目录下新建一个config文件，指定端口为443,

```text
host github.com
hostname ssh.github.com
port 443
```

![](http://images.cnitblog.com/blog/282019/201412/201545300797249)

2)执行`ssh -T git@github.com`
3)出现“Are you sure you want to continue connecting(yes/no)?”输入yes按一下“Enter”，出现成功提示即可

![](https://ws1.sinaimg.cn/large/006tNc79gy1fsbysifw6wj30p4061jrr.jpg)