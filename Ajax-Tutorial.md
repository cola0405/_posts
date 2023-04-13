---
title: Ajax Tutorial
date: 2021-05-11 10:26:00
tags:
categories:
---



```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```

```js
$.ajax({
            type: "GET",
            url: "http://localhost:8080/getRecord?area="+area,
            dataType: "json",
            jsonp: "callback",
            success: function (json) {
                console.log(json);
                let mainBody = document.getElementById("main-body");
                let table = "<table class='table'>";
                for(const key in json){
                    table += "<tr><td>"+key+"</td><td>"+json[key]+"</td></tr>"
                }
                table+="</table>"
                mainBody.innerHTML=table;
            },
            error: function () {
                alert("error");
            }
        });
```



---

#### ajax不发送请求

原因：没有正确引入jquery

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```

虽然某些别的js脚本也有引入jquery

但是那个版本可能不支持ajax

以导致ajax失效

