title: 用DocBlockr写更好看的注释
date: 2016-02-05 13:50:49
categories: 前端
---

DocBlockr很好用，不仅仅可以自动生成注释，还可以手动控制注释的格式。

安装方法：
`Cmd+Shift+P` -> `Install Package` -> `docblockr`

自定义配置：
`Preference` -> `Package Settings` -> `DocBlockr` -> `Settings - User`

配置成如下内容：
```js
{
    "jsdocs_extra_tags":[
        "@Author Hybrid",
        "@DateTime {{date}}",
        "@copyright ${1:[copyright]}",
        "@license ${1:[license]}",
        "@version ${1:[version]}"
    ],
    "jsdocs_function_description": false
}
```

![](http://images2015.cnblogs.com/blog/282019/201603/282019-20160309201825335-1871140404.gif)

参考： [https://github.com/spadgos/sublime-jsdocs/](https://github.com/spadgos/sublime-jsdocs/)