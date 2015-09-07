title: jquery操作select
date: 2014-11-05 23:50:49
categories: 前端
---

### 设值

根据value设置选中：
```javascript
$("#selector").val("myValue")
```

根据text设置选中：
```javascript
$("#selector").find("option[text='myText']").attr("selected", true)
```

### 取值

获取当前选中项的value
```javascript
$("#selector").val()
```

获取当前选中项的text
```javascript
$("#selector").find("option:selected").text()
```

### select 级联事件

```javascript
$("#selector1").change(function() {
    // 先清空第二个select
    $("#selector2").empty();
    // 实际应用中，循环生成多个options
    var option = $("<option>").val("myValue").text("myText")
    // 将option附加到selector2上
    $("#selector2").append(option);
});
```