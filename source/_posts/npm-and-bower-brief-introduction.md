title: 前端模块管理器简介
date: 2014-10-13 23:03:45
categories: 前端
---
# npm

### 介绍
npm(Node Packaged Modules)是Node.js的模块依赖管理工具。
安装node.js后会自动安装上npm工具。

npm命令运行时会读取和解释当前目录下的 `package.json` 文件，这个文件可以定义name、description、version、devDependencies等。


### 常用命令

安装模块使用 `npm install package_name`  命令，带上参数 `-g` 命令会把模块安装到全局安装目录中。
安装目录可以通过命令 `$ npm root -g` 查看。


## Bower

Bower的主要作用是，为模块的安装、升级和删除，提供一种统一的、可维护的管理模式

安装：

`$ npm install -g bower`

使用 `bower install` 命令安装各种模块，例如：

```bash
# 模块的名称
$ bower install jquery
# github用户名/项目名
$ bower install jquery/jquery
# git代码仓库地址
$ bower install git://github.com/user/package.git
# 模块网址
$ bower install http://example.com/script.js
# 根据配置文件bower.json安装所需的包
$ bower install
```

所谓"安装"，就是将该模块（以及其依赖的模块）下载到当前目录的bower_components子目录中。下载后，就可以直接签入到网页中。

`<script src="/bower_componets/jquery/dist/jquery.min.js">`

bower update命令用于更新模块。

```bash
$ bower update jquery
```

bower uninstall命令用于卸载模块。

```bash
$ bower uninstall jquery
```

注意，默认情况下，会连所依赖的模块一起卸载。比如，如果卸载jquery-ui，会连jquery一起卸载，除非还有别的模块依赖jquery。

