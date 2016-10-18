---
title: Javascript键盘事件
category: [javascript]
date: 2016-08-27 18:00:06
tags: [javascript]
---

Javascript键盘事件。

<!--more-->

>   keyup键盘弹起事件

```javascript
$("input[name='password']",loginForm).keyup(function(e){
    var ev = document.all ? window.event : e;  
    if(ev.keyCode==13) {
    // 如（ev.ctrlKey && ev.keyCode==13）为ctrl+Center 触发
        $("#ulogin").click();
    }  
});
```
