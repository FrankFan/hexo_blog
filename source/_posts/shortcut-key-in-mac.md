title: Mac 常用快捷键整理
date: 2015-07-28 08:21:38
categories: mac
---

## 文本编辑
以下适用于文本编辑器，浏览器等：

跳到页首  `cmd` + `↑`  类似windows下的 `ctrl + home`
跳到页尾  `cmd` + `↓`  类似windows下的 `ctrl + end`
光标移到行首  `cmd` + `←`  类似windows下的 `home`
光标移到行尾  `cmd` + `→`  类似windows下的 `end`
选择一行  `cmd` + `shift` + `→` 或 `cmd` + `shift` + `→` 
选择一个单词  `option` + `shift` + `←` 或 `option` + `shift` + `→` 
向上滚一屏 `fn` + `↑`
向下滚一屏 `fn` + `↓`
删除一整行文字  `cmd + delete`
删除一个单词    `option + delete`
光标移动一个单词 `option + ←` 或者 `option + →`

## 截屏
全屏截图自动保存为文件 `cmd + shift + 3`
区域截图自动保存为文件 `cmd + shift + 4`，这里有个小技巧，按下`cmd + shift + 4`后单击空格键，会出现一个相机的icon，表示自动捕捉这个区域。

## 窗口
关闭当前窗口  `cmd + w`
退出当前程序  `cmd + q`
最小化窗口  `cmd + m`
切换窗口程序  `cmd + tab`
快速显示桌面  `cmd + F3`
显示当前程序缩略图  `ctl + F3`
显示桌面和缩略图  `F3` 
显示Dashboard  `F4` 

## Terminal 终端

Mac不像`Ubuntu`可以使用 Ctrl+T 快捷键呼出终端，但是可以通过`control+space`呼出`Spotlight`，然后输入terminal回车快速打开终端。

光标移到行首 `ctrl` + `A`
光标移到行尾  `ctrl` + `E`
清除一行  `ctrl` + `U`
撤销清除  `ctrl` + `Y`
清屏  `ctrl` + `L`
新建一个Tab  `cmd` + `T`
关闭一个Tab  `cmd` + `W`


## 文件相关

```bash
# 创建目录
$ mkdir newDir
# 删除目录及子目录中的内容, 慎用!!
$ rm -rf newDir
# 复制
$ cp file toDir
# 设置目录读写权限
$ sudo chmod 777 /etc/hosts
```


## 进程相关

mac os x 下杀死进程
```bash
# 找到要杀死进程的id
$ ps -ef | grep idea  
# 强制kill掉进程
$ kill 91107
# 根据项目找对应的进程id
$ ps -ef | grep m-web
$ lsof -i:55010

$ lsof -i:55010 
COMMAND  PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    6227 fanyong    9u  IPv4 0xf526b9f45ed7c075      0t0  TCP *:55010 (LISTEN)
$ lsof -i:9001
COMMAND  PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    6227 fanyong  254u  IPv6 0xf526b9f456b4bcf5      0t0  TCP *:etlservicemgr (LISTEN)
```

`cmd + opt + esc` ，打开类似windows下任务管理器的快捷键。

![](http://images2015.cnblogs.com/blog/282019/201509/282019-20150908132558965-1931754023.jpg)


## 网络相关

```bash
# 查看本机IP、Mac地址等信息
$ ifconfig en0
# 查看nameserver 修改 nameserver 172.19.8.1 -> nameserver 172.19.8.2
$ sudo vim /etc/resolv.conf
# 诊断
$ dig lujs.cn
$ nslookup lujs.cn
```


## chrome 快捷键

新建一个Tab  `cmd` + `T`
关闭一个Tab  `cmd` + `W`
打开开发者工具，`cmd` + `option` + `I` Mac下F12不管用,因为系统默认把`F12`分配给了音量
查看源代码  `cmd` + `option` + `U`
调试js - step over `cmd` + `\`
调试js - step in `cmd` + `;`
调试js - step out `cmd` + `'`
快速定位Tab  `cmd` + `1/2/3/等`
向左切换Tab顺序  `cmd` + `shift` + `{`
向右切换Tab顺序  `cmd` + `shift` + `}`

