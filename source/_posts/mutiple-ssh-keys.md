title: 管理多个 ssh key
date: 2014-09-09 23:48:28
categories: github
---

以前只使用一个 ssh key 在github上提交代码，由于工作原因，需要再添加一个ssh key在公司的 gitlab上提交代码，下面记录下配置过程，防止遗忘。
说明下我的环境是 Win7 + msysgit + GitBash， 相信 *nux + bash 也是同样的道理。


## 生成并添加第一个ssh key
第一次使用ssh生成key，默认会在用户~（根目录）下生成 id_rsa, id_rsa.pub 2个文件；所以需要添加多个ssh key时也会生成对应的私钥和公钥。

```bash
$ ssh-keygen -t rsa -C "youremail@yourcompany.com"
```
在Git Bash中执行这条命令一路回车，会在 ~/.ssh/ 目录下生成 id_rsa 和 id_rsa.pub 两个文件，用文本编辑器将 id_rsa_pub 中的内容复制一下粘贴到github(gitlab)上。

## 生成并添加第二个ssh key
```bash
$ ssh-keygen -t rsa -C "youremail@gmail.com"
```
注意不要一路回车，要给这个文件起一个名字， 比如叫 id_rsa_github, 所以相应的也会生成一个 id_rsa_github.pub 文件。

![](http://images.cnitblog.com/blog/282019/201409/091222268402433)


目录结构如下：
![](http://images.cnitblog.com/blog/282019/201409/091222046992263)

## 添加私钥
```bash
$ ssh-add ~/.ssh/id_rsa
$ ssh-add ~/.ssh/id_rsa_github
```
如果执行ssh-add时提示"Could not open a connection to your authentication agent"，可以现执行命令：
```bash
$ ssh-agent bash
```
然后再运行ssh-add命令。

```bash
# 可以通过 ssh-add -l 来确私钥列表
$ ssh-add -l

# 可以通过 ssh-add -D 来清空私钥列表
$ ssh-add -D
```


## 修改配置文件
在 ~/.ssh 目录下新建一个config文件
```bash
touch config
```

添加内容：
```bash
# gitlab
Host gitlab.com
    HostName gitlab.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

# github
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_github
```

## 测试
```bash
$ ssh -T git@github.com
```
输出 
Hi user! You've successfully authenticated, but GitHub does not provide shell access. 就表示成功的连上github了