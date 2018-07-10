title: Mac OS 常用命令行
date: 2016-01-08 16:29:25
categories: mac
---

##  mac os 用命令下杀死进程
Mac没找到类似windows下进程管理器的GUI软件，通过命令也很简单：

```bash
# 找到要杀死进程的id
$ ps -ef | grep idea
$ kill 91107
$ ps -ef | grep m-web

# 查看端口被哪个进程占用
$ lsof -i:55010
COMMAND  PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    6227 fanyong    9u  IPv4 0xf526b9f45ed7c075      0t0  TCP *:55010 (LISTEN)
$ lsof -i:9001
COMMAND  PID    USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    6227 fanyong  254u  IPv6 0xf526b9f456b4bcf5      0t0  TCP *:etlservicemgr (LISTEN)
```


## 查看本机IP
mac是`ifconfig`,windows下是`ipconfig`

```bash
$ ifconfig # 查看全部信息
$ ifconfig en0 # 查看en0的IP
$ ipconfig getifaddr en0 # 更精确的命令
```


## 查看目录、文件占用空间

```bash
# 查看目录大小：
$ du -h -d 1 ~/gitlab
# 查看磁盘容量
$ df -h
```

## 压缩 & 解压缩

```bash
$ 最通俗的用法
$ zip -q -r -e -m -o [yourName].zip someThing
-q 表示不显示压缩进度状态
-r 表示子目录子文件全部压缩为zip  //这部比较重要，不然的话只有something这个文件夹被压缩，里面的没有被压缩进去
-e 表示你的压缩文件需要加密，终端会提示你输入密码的
# 还有种加密方法，这种是直接在命令行里做的，比如zip -r -P Password01! modudu.zip SomeDir, 就直接用Password01!来加密modudu.zip了。
-m 表示压缩完删除原文件
-o 表示设置所有被压缩文件的最后修改时间为当前压缩时间
# 当跨目录的时候是这么操作的
$ zip -q -r -e -m -o '\user\someone\someDir\someFile.zip' '\users\someDir'

# 解压缩
$ unzip zippedfile.zip
```