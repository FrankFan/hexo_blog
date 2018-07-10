title: 使用webpack+babel开发npm模块
date: 2018-07-10 16:27:25
categories: 前端
---

# 开发npm命令行工具

开发npm包，推荐使用ES6书写，再用babel进行转码，将ES6转成ES5，开发体验好，效率高。

<!-- more -->

![](https://ws2.sinaimg.cn/large/006tNc79ly1ft3sede2lmj305w0bgaaf.jpg)



一个典型的node工程目录解构，bin目录下存放程序入口，libs目录下存放逻辑源码，使用webpack进行模块构建，使用babel进行ES6转码，使用npm script管理脚本。



### 创建node脚本入口

比如创建一个`cli.js`文件：

```js
#!/uisr/bin/env node

console.log('your code goes here');
```

1. 需要注意的是，第一行代码需要添加[片段标识符](https://en.wikipedia.org/wiki/Shebang_%28Unix%29)(也叫hashbang)，使用Node解释器执行该脚本。如果遇到权限问题，使用`sudo chmod +x file` 添加可执行权限 。
2. 其次，在`package.json`中，必须提供`bin`字段： `"bin": "bin/cli"`相当于指定npm的入口。



### 使用commander处理命令参数问题

gituhub的README上写的很详细，<https://github.com/tj/commander.js/blob/master/Readme_zh-CN.md>

![](https://ws3.sinaimg.cn/large/006tNc79gy1ft3teq77flj31a80bcgnp.jpg)

### 调试过程

1. 推荐使用`VS Code`开发node应用，不仅仅代码提示、导航方面做的好，最好用的一点是可以直接F5启动调试模式，可以打断点一行一行的调试node程序，前提是设置好程序入口。对于更加复杂的应用， 可以通过配置`.vscode/launch.json`进行高级配置。

2. 在项目根目录下通过`npm link`可以将项目link到全局`node_modules`目录，这样就可以在任意目录下都可以使用自己的命令，英文名叫`symbolic link`，每次保存原文件会link也会立即生效， 不用再次运行`npm link`命令。

```bash
# 查看链接的位置
$ which your_command
```


### 发布npm包

1. 首先当然是需要在[npm官网](http://npmjs.org/)上进行注册；
2. 在命令行中输入`npm login`登录，验证成功之后就可以发布自己的模块了；
3. 执行`npm publish`发布
4. 升级版本时执行`npm version patch`命令，npm会自动升级`package.json`中的`version`字段并打`tag`,详细可以了解一下[semver](https://docs.npmjs.com/misc/semver)
5. 使用`npm view node_module`,可以查看模块的配置信息
6. 可以通过`npm unpublish --force`删除发布的模块，必须是发布24小时之内（没有测过，有谁亲测了可以说一下）


### 参考

https://codeburst.io/how-to-create-and-publish-your-first-node-js-module-444e7585b738

<https://medium.com/@the1mills/how-to-test-your-npm-module-without-publishing-it-every-5-minutes-1c4cb4b369be>

<https://morning.work/page/2015-11/es6-es7-develop-npm-module-using-babel.html>