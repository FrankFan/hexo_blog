title: Mac下启动server的方法汇总
date: 2015-12-01 13:13:34
categories: mac
---

Mac是一个对开发者特别友好的操作系统，除了好看的UI、好用的控制台，还有Terminal都是开发者的好助手。
比如在开发前端页面的过程中，通常需要在


以 Mac 下的 http server 为例子。


- Python起一个静态server

默认8000端口
`python -m SimpleHTTPServer` 

可以指定端口：
`python -m SimpleHTTPServer 8080`  

python会以当前目录作为根目录起一个本地server, 根据终端的反馈比如访问`localhost:8000`就可以看到效果了。

![](http://images2015.cnblogs.com/blog/282019/201512/282019-20151208194159480-1498313497.png)


- PHP 自带web server

启动php Web Server
`php -S localhost:8080`

指定网站根目录，-t命令
`php -S localhost:8080 -t /www`

支持远程访问
`php -S 0.0.0.0:8080 -t /www`

![](http://images2015.cnblogs.com/blog/282019/201512/282019-20151208195302386-395401372.png)

- nodejs

推荐使用[browsersync](http://www.browsersync.cn/#install)

```
npm install -g browser-sync
npm install --save-dev browser-sync
```

然后在`package.json`文件中指定启动命令：
```
"scripts": {
    "start": "browser-sync start --server --files '*.css, *.html' "
}
```


- Apache 

最后介绍下Mac自带的Apache服务器,默认80端口，启动后直接访问`locahost`可以看到`It works!`页面。

```
# 查看版本信息
$ apachectl -v
# 启动与关闭Apache，该操作需要root权限
$ sudo apachectl start
$ sudo apachectl stop
```

默认wwww跟目录在`/Library/WebServer/Documents`, apache的安装目录在`/etc/apache2`.

![](http://images2015.cnblogs.com/blog/282019/201512/282019-20151208201626402-1471863449.png)

以上所说的Server用于个人测试及小网站的开发是没有任何问题的，不过生产发布时大型应用还是要配合Nginx或Apache以达到最高效率。