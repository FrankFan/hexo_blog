title: 通过nodejs、Express框架搭建Web
date: 2014-11-25 20:49:18
categories: node
---

通过nodejs、Express框架搭建Web

Express 是一个简洁、灵活的 node.js Web 应用开发框架, 它提供一系列强大的特性，帮助你创建各种 Web 和移动设备应用。
官网 [http://expressjs.com/](http://expressjs.com/)

![](https://ws2.sinaimg.cn/large/006tNc79gy1fsbyoewybbj308a048t8k.jpg)

![](https://ws4.sinaimg.cn/large/006tNc79gy1fsbyohvh59j30ax08fwf3.jpg)

0. 安装node.js
这个就略过。

1. 安装 express
$ npm install express --save

2. 安装 express 生成器
$ npm install express-generator -g

3. 检测是否安装成功
$ express -V

4. 生成一个app
$ express myapp

```bash

   create : myapp
   create : myapp/package.json
   create : myapp/app.js
   create : myapp/public
   create : myapp/public/images
   create : myapp/public/stylesheets
   create : myapp/public/stylesheets/style.css
   create : myapp/routes
   create : myapp/routes/index.js
   create : myapp/routes/users.js
   create : myapp/views
   create : myapp/views/index.jade
   create : myapp/views/layout.jade
   create : myapp/views/error.jade
   create : myapp/public/javascripts
   create : myapp/bin
   create : myapp/bin/www

   install dependencies:
     $ cd myapp && npm install

   run the app:
     $ DEBUG=myapp ./bin/www
```

5. 安装npm依赖
$ cd myapp && npm install

6. 启动服务， 注意路径别写错
$ set DEBUG=myapp & node myapp/bin/www

正确的话就可以打开浏览器 http://localhost:3000/

![](https://ws1.sinaimg.cn/large/006tNc79gy1fsbyomejx6j30du094dg2.jpg)
