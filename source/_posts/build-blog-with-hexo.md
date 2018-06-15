title: 基于Hexo搭建个人博客
date: 2014-03-03 21:07:45
categories: github
---

## 前言
Hexo出自台湾大学生之手，是一款基于node.js的静态博客框架程序，使用方便，编译速度快，几道命令就能拥有一个自己的个人博客，比基于Ruby的Jekyll用起来很舒服。
Hexo相对于Wordpress来说，最大的区别就是一个完全静态，静态博客的特点：

 - 不用配置服务器
 - 不用数据库
 - 访问速度相当快
 - 支持markdown方式书写
 - 没有安全性可言（代码都托管在github或者gitcafe）
 - 更加注重博客内容

我的博客是托管在`github pages`上的，具体做法可以参考 [https://pages.github.com/](https://pages.github.com/)

## 环境准备
### 安装Node.js环境
到[Node.js官网](http://www.nodejs.org)下载相应平台的最新版本，安装即可。
我用的版本是：
![](https://ws1.sinaimg.cn/large/006tNc79gy1fsc02h32r0j30dg08d3yn.jpg)


### 安装Hexo
npm是node package manager的缩写，成功安装node后就可以使用了。
```bash
npm install -g hexo-cli
npm install # 根据package.json安装依赖模块
```

### 初始化
```bash
hexo init <folder>
```
> 也可以cd到目标目录，执行hexo init

### 生成静态页面
cd到你的init目录，执行generate命令，博客静态页面将会生成到目录hexo/public 下
```bash
hexo generate
```
### 本地启动预览模式
执行以下命令，启动本地服务，开启预览模式
```bash
hexo server
```
hexo会自动打开浏览器地址为 http://localhost:40000 的地址，一个博客的雏形就可以看到。最好使用现在浏览器，如Chrome、Firefox等，因为有些特性不被古老的浏览器不所支持。

### 写文章
hexo和jekyll一样，都可以用markdown来写博客，这也是吸引我的原因之一。
执行new命令，hexo会生成指定名称的文章至目录hexo/source/_posts/postName.md 
```bash
hexo new [layout] 'postName' # 新建文章
```
其中layout是可选参数，默认值是post，具体有哪些值可以到hexo/scaffolds/目录下看，文件名就是layout名称。
其实也可以通过手动的方式在_posts目录下新建文章。

### 发布
写完第一篇文章就可以发布了，让我们拭目以待吧。在init的目录下执行以下命令，会在hexo根目录生成一个.deploy目录，放置编译后的html文件。
```bash
hexo delpoy
```
执行deploy命令之后，hexo的目录结构如下:
```plain
.
├── .deploy
├── node_modules
├── public
├── scaffolds
├── scripts
├── source
|   ├── _drafts
|   └── _posts
|   └── about
|   └── 404.html
|   └── CNAME
├── themes
├── _config.yml
└── package.json
```

 - .deploy：执行hexo deploy命令后准备发布的内容
 - node_modules：执行npm install安装的组件
 - public：执行 hexo g命令后，输出的静态html内容
 - scaffolds：脚手架，layout模板文件目录
 - scripts：扩展脚本目录，可以自定义javascript脚本
 - source：文章的源码目录，该目录下的markdown和html均会被hexo处理；404文件、CNAME文件都应该放在这里
	 - drafts：草稿
	 - posts：要发布的文章
 - themes：主题
 - _config.yml：全局配置文件，大多数设置都在这里
 - package.json：配置文件，说明nodejs依赖

### 常用命令总结
```bash
hexo new "postName" # 新建文章
hexo new page "about" # 新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo clean # 有时候配置没有立即生效需要删除cache
```
如果觉得以上这些命令太长的话，可以使用对应的简写方式：
```bash
hexo n === hexo new # 新建文章
hexo g === hexo generate # 生成html
hexo s === hexo server # 启动预览
hexo d === hexo deploy # 一键发布
```

## 自定义博客
### 主题
首先要下载主题放在themes目录下，
```bash
cd hexo/themes
git clone remote_themes_url
```
然后修改配置文件_config.yml 的 theme配置项：
```javascript
# Extensions
## Plugins: https://github.com/hexojs/hexo/wiki/Plugins
## Themes: https://github.com/hexojs/hexo/wiki/Themes
theme: jacman
exclude_generator:
Plugins:
- hexo-generator-feed
- hexo-generator-sitemap
```

### 配置发布信息
在根目录下_config.yml文件中添加deploy配置项，每次执行hexo d命令后会自动把deploy目录中的内容push到github上。
```bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: github
  repository: https://github.com/FrankFan/frankfan.github.io.git
  branch: master
```

### 添加自定义页面
执行以下命令，可以添加一个新页面：
```bash
hexo new page "about"
```
该命令会生成hexo/source/about/index.md文件，该文件继承了站点的风格，只需编辑编辑markdown文件即可。
最后不要忘记在theme的配置文件中显示出来：
```bash
##### Menu
menu:
  首页: /
  归档: /archives
  关于: /about
```

### 添加统计
hexo默认使用Google Analytics，但是ga经常被墙从而会导致一些没有翻墙工具的用户加载速度过慢，转而使用百度统计。添加统计配置很简单，编辑theme目录下的_config.yml文件，增加配置项：
```bash
baidu_tongji: true
```
然后新建文件 theme/jackman/layout/_partial/baidu_tongji.ejs , 内容如下：
```javascript
<% if (theme.baidu_tongji){ %>
<script type="text/javascript">
#你的百度统计代码,可以从百度统计官网注册获得
</script>
<% } %>
```
最后，编辑文件 hexo/themes/jackman/_partial/footer.ejs,在最后添加一行代码：
```javascript
<%- partial('baidu_tongji') %>
```

### 添加自定义（微博）挂件
除了hexo默认提供的挂件外，还可有自定义小挂件，比如添加一个微博挂件。
首先在hexo/themes/jackman/layout/_widget/目录下新建一个ejs文件，如weibo.ejs，然后在配置文件hexo/themes/jackman/_config.yml中添加配置：
```javascript
#### Widgets
widgets: 
- category
- weibo
- rss
```
微博挂件代码可以从[这里](http://open.weibo.com/widgets?cat=wb)获取。

### 插件
首先安装插件：
```bash
npm install <plugin-name> --save
```
然后在hexo根目录下配置文件_config.yml中启用：
```bash
Plugins:
- hexo-generator-feed ## RSS插件
- hexo-generator-sitemap
```
插件的升级与卸载：
```bash
npm update
npm uninstall <plugin-name>
```
### 图床
图床问题可参考我之前的[这篇文章](http://fy98.com/2014/03/15/2014-03-15-cnblogs-image-bed/)，完美解决使用markdown书写文章的图片问题。

### 最后
更新 hexo：
```bash
npm update -g hexo
```
更新主题：
```bash
cd themes/theme_name
git pull
```

## 感谢
博主携每一颗DOM元素、每一个CSS样式以及每一句Javascript代码感谢以下网友的文章，排名不分先后：

 1. [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
 2. [如何搭建一个独立博客——简明Github Pages与Hexo教程](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)
 3. [感谢博客园伴我成长](http://www.cnblogs.com/)
 4. [感谢Dnspod提供免费域名解析服务,恭喜被企鹅收了](http://www.dnspod.cn/)
 5. [感谢强大的github提供免费资源托管](http:///www.github.com/)