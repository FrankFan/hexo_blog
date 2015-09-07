title: 前端知识ABC
date: 2015-03-16 22:52:28
categories: 前端
---

经常有人问我前端怎么学，怎么才能快速上手。其实我也没有标准答案。前端虽然可以简单的概括为 `HTML + CSS + JavsScript`, 但实际上要刨根问底儿的话远不止这些。

下面从26个字母表的顺序整理一下前端相关的知识点。

## Angular
一款优秀的前端js框架，WebApp的优秀解决方案。包含MVVM模式、自动化双向绑定等特色功能。现由 `google`维护，每个前端不能错过的框架。

![](http://images.cnitblog.com/blog2015/282019/201504/162310471679265)

## Backbone
`Backbone`小巧但很强大，基于MVC，上手容易，入门难度低，灵活性高。

![backbone](http://images.cnitblog.com/blog2015/282019/201504/162315098543313)

## Console
`Console API`虽然还没有成为一个正式标准，但是作为js调试利器，无人不知，无人不晓。
chrome下的F12、FireFox下的Firebug都有，IE8+ 在打开控制台时也可以使用该对象。

注意：在一些较老的浏览器中，只有在控制台打开时`console`对象才有定义。如果在控制台关闭的情况下运行那些使用 `Console API` 的脚本会导致错误。

## D3.js
D3.js是一个用于网页作图、生成互动图形的JavaScript函数库。它提供一个d3对象，所有方法都通过这个对象调用。

![](http://d3js.org/logo.svg)

## Express

Express 是一个简洁、灵活的 node.js Web 应用开发框架, 它提供一系列强大的特性，帮助你创建各种 Web 和移动设备应用。
官网 [http://expressjs.com/](http://expressjs.com/)

![](http://images.cnitblog.com/blog/282019/201412/042022281396234)

## Fork
玩`github`的人都懂，`fork`本意是`叉子`之意，此处为`分支分流`的意思，执行`fork `动作后就会将别人的项目clone一份到自己的仓库，但是owner变成自己，目的是将来能够为项目贡献代码，一起 `social coding`.

## Grunt/Gulp
前端自动化工具。
对于需要反复重复的任务，例如压缩（minification）、编译、单元测试、linting等，自动化工具可以减轻你的劳动，简化你的工作。当你正确配置好了任务，任务运行器就会自动帮你或你的小组完成大部分无聊的工作。

![](http://www.gruntjs.net/img/grunt-logo.svg)

## Haslayout
CSS布局相关知识点。
haslayout 是Windows Internet Explorer渲染引擎的一个内部组成部分。在InternetExplorer中，一个元素要么自己对自身的内容进行计算大小和组织，要么依赖于父元素来计算尺寸和组织内容。为了调节这两个不同的概念，渲染引擎采用了 hasLayout 的属性，属性值可以为true或false。当一个元素的 hasLayout属性值为true时，我们说这个元素有一个布局（layout）

## Iconfont
在此之前我们使用`CSS Sprite`来进行碎图合并，减少http请求。现在使用的`Icon font`技术，是指用字体文件取代图片文件，来展示图标、特殊字体等元素的方法。

推荐2个在线字体库：
[阿里icon font字库](http://www.iconfont.cn/)
[Font-Awesome](http://fortawesome.github.io/Font-Awesome/)

## Jsonp
用于js跨域请求，原理是使用`script`标签的`src`属性的可跨域性质请求其他域名下的接口，使用灵活。缺点是只支持get请求，不支持post请求。

我封装过一个关于`jsonp.js`的类库：
[fyjs.jsonp.js](https://github.com/FrankFan/fyjs/blob/master/src%2Ffyjs.jsonp.js)

## Kissy
KISSY 是由淘宝前端工程师们发起创建的一个开源 JS 类库。
它遵循的原则是 小巧灵活、简洁实用、愉悦编码、快乐开发。
Keep It，Simple & Stupid, Short & Sweet, Slim & Sexy...Yeah!

## LocalStorage
`HTML 5 `新增本地存储功能。
参考：[Html5中的sessionStorage和localStorage简介](http://fy98.com/2014/12/15/sessionStorage-localStorage-in-html5/)

## Media Query
`CSS3`新增特性，中文称为媒体查询。`Responsive Design`的基础。

[响应式设计示例](http://codepen.io/FrankFan/pen/YPjwMO)

## Npm
NPM的全称是`Node Package Manager`，是一个NodeJS包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准

![](https://www.npmjs.com/static/images/npm-logo.svg)

## Opacity
`CSS` 属性，可以设置元素滤镜和半透明效果。

## Prototype
`prototype`既是一个js类库，又是`javascript`语言的核心，js是基于原型的语言。


## Querystring
url中传参的好地方。

## Referrer
互联网的本质是连接一切， `Referrer` 可以告诉搜索引擎上一个页面来自哪里。

## Seajs
SeaJS是一个遵循CommonJS规范的JavaScript模块加载框架，可以实现JavaScript的模块化开发及加载机制。
SeaJS的作者是前淘宝UED,现支付宝前端工程师玉伯。

常与之并肩的是国外的`require.js`

## Trim
任何编程语言都可以实现 `trim` 字符串的功能，与之对应还有 `trimeLeft`、 `trimRight` 以及 `trimAll` 等。

## Underscore
`underscore`是`backbone`唯一依赖的js类库。
Underscore是一个非常实用的JavaScript库，提供许多编程时需要的功能的支持，它在不扩展任何JavaScript的原生对象的情况下提供很多实用的功能。

Underscore提供60多个方法，即有普通的功能，例如: map, select, invoke — 也有更多特殊的编程辅助方法，例如：函数绑定、javascript模板、绝对相等判断等待。 如果一些现代的浏览器提供了内置的 forEach, map, reduce, filter, every, some 和 indexOf方法，Underscore就委托给浏览器原生的方法。 

## Vim
`Vim`号称编辑器之神。是每个有情怀的程序员不可或缺的编辑器。

## Web Worker
`Web Workers` 是 HTML5 提供的一个javascript多线程解决方案，可以将一些大计算量的代码交由web Worker运行而不冻结用户界面。Web Worker的基本原理就是在当前javascript的主线程中，使用Worker类加载一个javascript文件来开辟一个新的线程，起到互不阻塞执行的效果，并且提供主线程和新线程之间数据。

## XSS
跨站脚本攻击(Cross Site Scripting)，恶意攻击者往Web页面里插入恶意html代码，当用户浏览该页之时，嵌入其中Web里面的html代码会被执行，从而达到恶意攻击用户的特殊目的。（我的项目就被攻击过，骇客监听我的键盘事件，每秒都要发送一次请求到他的服务器，真是卑鄙啊）

## Yslow
雅虎军规—— `Yslow`优化23条规则。每个前端必知必会。

```javascript
1. 减少HTTP请求次数
合并图片、CSS、JS，改进首次访问用户等待时间。
2. 使用CDN
就近缓存==>智能路由==>负载均衡==>WSA全站动态加速
3. 避免空的src和href
当link标签的href属性为空、script标签的src属性为空的时候，浏览器渲染的时候会把当前页面的URL作为它们的属性值，从而把页面的内容加载进来作为它们的值。测试
4. 为文件头指定Expires
使内容具有缓存性。避免了接下来的页面访问中不必要的HTTP请求。
5. 使用gzip压缩内容
压缩任何一个文本类型的响应，包括XML和JSON，都是值得的。旧文章
6. 把CSS放到顶部
7. 把JS放到底部
防止js加载对之后资源造成阻塞。
8. 避免使用CSS表达式
9. 将CSS和JS放到外部文件中
目的是缓存，但有时候为了减少请求，也会直接写到页面里，需根据PV和IP的比例权衡。
10. 权衡DNS查找次数
减少主机名可以节省响应时间。但同时，需要注意，减少主机会减少页面中并行下载的数量。
IE浏览器在同一时刻只能从同一域名下载两个文件。当在一个页面显示多张图片时，IE 用户的图片下载速度就会受到影响。所以新浪会搞N个二级域名来放图片。
11. 精简CSS和JS
12. 避免跳转
同域：注意避免反斜杠 “/” 的跳转；
跨域：使用Alias或者mod_rewirte建立CNAME（保存域名与域名之间关系的DNS记录）
13. 删除重复的JS和CSS
重复调用脚本，除了增加额外的HTTP请求外，多次运算也会浪费时间。在IE和Firefox中不管脚本是否可缓存，它们都存在重复运算JavaScript的问题。
14. 配置ETags
它用来判断浏览器缓存里的元素是否和原来服务器上的一致。比last-modified date更具有弹性，例如某个文件在1秒内修改了10次，Etag可以综合Inode(文件的索引节点(inode)数)，MTime(修改时间)和Size来精准的进行判断，避开UNIX记录MTime只能精确到秒的问题。 服务器集群使用，可取后两个参数。使用ETags减少Web应用带宽和负载
15. 可缓存的AJAX
“异步”并不意味着“即时”：Ajax并不能保证用户不会在等待异步的JavaScript和XML响应上花费时间。
16. 使用GET来完成AJAX请求
当使用XMLHttpRequest时，浏览器中的POST方法是一个“两步走”的过程：首先发送文件头，然后才发送数据。因此使用GET获取数据时更加有意义。
17. 减少DOM元素数量
是否存在一个是更贴切的标签可以使用？人生不仅仅是DIV+CSS
18. 避免404
有些站点把404错误响应页面改为“你是不是要找***”，这虽然改进了用户体验但是同样也会浪费服务器资源（如数据库等）。最糟糕的情况是指向外部 JavaScript的链接出现问题并返回404代码。首先，这种加载会破坏并行加载；其次浏览器会把试图在返回的404响应内容中找到可能有用的部分当作JavaScript代码来执行。
19. 减少Cookie的大小
20. 使用无cookie的域
比如图片 CSS 等，Yahoo! 的静态文件都在主域名以外，客户端请求静态文件的时候，减少了 Cookie 的反复传输对主域名的影响。
21. 不要使用滤镜
png24的在IE6半透明那种东西，别乱使，淡定的切成PNG8+jpg
22. 不要在HTML中缩放图片
23. 缩小favicon.ico并缓存
```

## Zepto
`zepto.js` 是一个专为 `mobile WebKit` 浏览器(如：Safari和Chrome)而开发的一个JavaScript框架,移动端开发利器。 
它标榜自己在其简约的开发理念，能够帮助开发人员简单、快速地完成开发交付任务。更重要的是这个JS框架，是超轻量级的，只有5KB。

`zepto.js` 的语法借鉴并且兼容jQuery。

![](http://zeptojs.com/logo.png)