title: javascript和C#比较
date: 2014-10-13 23:11:57
categories: .net
---

C#和javascript有很多相似的地方，比如：

## 序列化
C#序列化
1. 首先需要引用
`using System.Web.Script.Serialization;//System.Web.Extensions添加dll引用`

2.序列化为字符串
```javascript
JavaScriptSerializer jss = new JavaScriptSerializer();
string str = jss.Serialize(objData);
```

3.反序列化为对象
```javascript
JavaScriptSerializer jss = new JavaScriptSerializer();
//将字符串反序列化为Token对象
myToken = jss.Deserialize<TokenEntity>(jsonStr);
```

Javascript中
1. 字符串 -> Json对象

```javascript
jsondata = data.toJSON()
```

2. 对象 -> Json字符串

```javascript
string jsonStr = JSON.stringify(arrData);

// Note: The JSON object is now part of most modern web browsers (IE 8 & above).
```

## 声明对象

C# 创建匿名对象
```csharp
var studentInfo = new 
{
     Name = "Tom",
     Age = 25
};
```

Javascript创建匿名对象

```javascript
var studentInfo = {
     name: "Tom",
     age: 25
};
```
