title: shadowsocks server & client
date: 2017-06-26 22:37:13
categories: server
---

本文记录如何在 `Ubuntu 12.04 LTS` 版本的VPS操作系统上安装 shadowsock server 的过程。开启 shadowsocks 服务后，用 ss client 连接到 VPS上，通过VPS上网，从而达到科学上网的目的。


## 安装 shadowsocks
通过 ssh 命令登录到远程服务器，确保 `apt-get install` 命令可用的情况下，一次输入如下命令，安装所需的软件：

```shell
apt-get update
apt-get install build-essential 
apt-get install python-gevent python-pip
apt-get install python-m2crypto 
apt-get install python-dev
apt-get install supervisor
pip install shadowsocks
```

## 配置 shadowsocks.json 文件

编辑 `/etc/shadowsocks.json` 文件。如果没有新建一个。

```js
{
    "server":"your_ip_address",
    "server_port":8388,
    "local_port":1080,
    "password":"my password",
    "timeout":600,
    "method":"aes-256-cfb"
}
```

编辑 `/etc/supervisor/conf.d/shadowsocks.conf` 文件。

```js
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json  
autorestart=true  
user=nobody  
```

## 服务器端启动shadowsocks



运行supervisor
```
service supervisor start
supervisorctl reload 
```

如果出现以下错误: `Error: Another program is already listening on a port that one of our HTTP servers is configured to use. Shut this program down first before starting supervisord`.尝试输入`sudo unlink /tmp/supervisor.sock`, 或者 `unlink /var/run/supervisor.sock `。然后启动supervisor服务。



## 通过以下命令管理shadowsocks进程:


```
ssserver -c /etc/shadowsocks.json -d start
ssserver -c /etc/shadowsocks.json -d stop
```

以上如果正常的话，服务端ss就应该跑起来了。

接下来就是根据自己的OS选择对应的[client](https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients)了


![](/imgs_blog/1@2x.png)


![](/imgs_blog/2@2x.png)

参考：
https://www.chedanji.com/ubuntu-shadowsocks/
http://livezingy.com/ubuntu14-04_digitalocean_shadowsocks/
https://my.oschina.net/letiantian/blog/193418
https://askubuntu.com/questions/426750/how-can-i-update-my-nodejs-to-the-latest-version

