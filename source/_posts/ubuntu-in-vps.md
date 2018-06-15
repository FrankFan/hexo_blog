title: Ubuntu 的基本配置
date: 2016-03-18 13:29:20
categories: Server
---

买了一个VPS，选择了Ubuntu12.04 LTS 作为操作系统，下面介绍下做过的一些配置，记录一下。

<!-- more -->

```bash
# 登录到VPS
$ ssh root@[your_ip_address]
```

登录上来以后第一件事就是查看一下系统的版本和名称等信息：

```
$ lsb_release -a
# 系统信息
root@GalaxyServer:~# lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:  Ubuntu 12.04.5 LTS
Release:  12.04
Codename: precise
```


登上来以后第二件事就是安装各种软件，发现通过`apt-get install xxx`命令安装会报各种网络错误, 或者资源 `404 Not Found`等错误，导致安装软件失败。

解决办法是修改 `source.list` 源文件， 位置在 `/etc/apt/sources.list`，VPS默认的源都是指向.hk的域名，有些在url在大陆无法正常访问，所以需要修改下 `source.list`文件.

`Tips`：修改服务器文件之前习惯性备份一下是个好习惯：
`cp sources.list sources.list.backup`

```
$ cd /etc/apt/
$ vim sources.list
# 复制粘贴下面的↓↓↓
deb http://cn.archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse
# 测试版源
deb http://cn.archive.ubuntu.com/ubuntu/ precise-proposed main restricted universe multiverse
# 源码
deb-src http://cn.archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse
deb-src http://cn.archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse
deb-src http://cn.archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse
deb-src http://cn.archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse
# 测试版源
deb-src http://cn.archive.ubuntu.com/ubuntu/ precise-proposed main restricted universe multiverse
# Canonical 合作伙伴和附加
deb http://archive.canonical.com/ubuntu/ precise partner
deb http://extras.ubuntu.com/ubuntu/ precise main

```


环境准备好之后，就可以安装软件了。

```
# 安装Apache
$ apt-get install apache2 apache2-doc apache2-utils
# 通过下面命令验证是否安装成功
root@GalaxyServer:~# apachectl -v
Server version: Apache/2.2.22 (Ubuntu)
Server built:   Jul 15 2016 15:32:46

# 安装 vim
$ apt-get install vim

# 安装 curl
$ apt-get install curl

# 安装 node
$ apt-get install nodejs

# 安装 npm
$ apt-get install npm

# 可以使用一下命令检测是否安装成功
$ node -v
$ npm -v

```


# scp 部署
```
$ scp ~/tmp/hello.html root@[your_ip_address]:/var/www/
```

# 修改root密码
```
$ root@GalaxyServer:~# passwd root
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```


# 参考
[digitalocean.com非常详细的一篇文章](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts)