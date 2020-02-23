# Json With padding  
目的：解决跨域问题  
原理：html中的标签可以不受同源策略影响申请。创建script标签，请求远程服务器地址，获取函数字符串（需要服务端配合，返回一个函数的字符串形式）
前端收到后自动调用该函数，实现数据的获取。  

html文件：
```  
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>test</title>
</head>
<script  src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<body>

</body>
<script type="text/javascript">
    // // 1.用jQuery
    $.getJSON('http://localhost/callback=?',function(data){
        var dt = JSON.parse(data);
        console.log(data);
        console.log(data.name);
    });
    // 2.原生
    function addScript(url){
        var scpt = document.createElement('script');
        scpt.src = url;
        document.body.appendChild(scpt);
    }
    function person(dt){
        document.open();
        document.write(dt.name)
        document.close();
        console.log(dt)
    }

    window.onload=function(){
        addScript('http://localhost:3000/callback=person')
    }
</script>
</html>
```
  
服务端文件：  
```  
var express = require('express');
var app = express();

app.get('/',function(req,res){
    console.log('index')
    res.send({name:'John',age:18});
})
app.get('/callback=:cbk',function(req,res){
    var bk = req.params.cbk
    var vt = {name:'Tim',age:28,id:bk};
    res.send(bk+'('+JSON.stringify(vt)+')');
})
app.listen(3000);
```