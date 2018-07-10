title: 原生Ajax全解析
date: 2014-12-29 23:51:53
categories: javascript
---

##一、介绍
本文介绍利用原生态Javascript打造Ajax的全过程。

达到的效果是：点击页面上的按钮，通过传统的Javascript的Ajax方式从服务端取回一个"Hello Ajax!"的字符串显示在页面上。

如图所示：
![](https://ws3.sinaimg.cn/large/006tNc79gy1fsbyo1u75sj309p05m0sr.jpg)

## 二、前端准备

1. 页面上的HTML元素
```html
<input type="button" value="Ajax提交" onclick="Ajax();" />
<div id="resText"></div>
```
2. Javascript代码

```javascript
/*
*  Description:原生态Javascript实现的Ajax
*  效果：点击按钮通过传统Javascript的Ajax方式从服务端取回一个"Hello Ajax!"的字符串显示在页面上
*  Author: FrankFan
*  Date：2012-8-11
*/

// 声明一个空对象用来装入XMLHttpRequest
var xmlHttpReq = null;

//该函数用来异步获取信息
function Ajax() {
    // 给xmlHttpReq对象赋值
    if (window.ActiveXObject) { // IE5 IE6是以ActiveXObject的形式引入XMLHttpRequest对象的
        xmlHttpReq = new ActiveXObject("Microsoft.XMLHTTP");
    }
    else if (window.XMLHttpRequest) {   //除IE5 IE6以外的浏览器XMLHttpRequest是window的一个子对象
        xmlHttpReq = new XMLHttpRequest(); //实例化一个XMLHttpRequest对象
    }
    if (!xmlHttpReq) {
        alert("创建xmlhttp对象异常！");
        return false;
    }

    //实例化成功后，用open方法初始化XMLHttpRequest对象
    xmlHttpReq.open("GET", "Server.ashx", true); //调用open方法并采用异步方式
    xmlHttpReq.onreadystatechange = RequestCallBack; // 设置回调函数

    xmlHttpReq.send(); //最后才正式发送请求
}

// 请求的回调函数
function RequestCallBack() {
    if (xmlHttpReq.readyState == 4) {
        if (xmlHttpReq.status == 200) {
            document.getElementById("resText").innerHTML = xmlHttpReq.responseText;
        }
        else {
            alert("Ajax服务器返回错误！");
        }
    }
}
```

## 三、服务端
本例是将xmlHttpRequest请求提交到了一般处理文件Server.ashx,代码如下：

```csharp
namespace AjaxDemo
{
    public class Server : IHttpHandler
    {

        public void ProcessRequest(HttpContext context)
        {
            context.Response.ContentType = "text/plain";
            context.Response.Write("Hello Ajax!");
        }

        public bool IsReusable
        {
            get
            {
                return false;
            }
        }
    }
}
```

