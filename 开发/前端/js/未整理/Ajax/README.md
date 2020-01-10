# AJAX  
+ 产生背景：  
以往的技术当需要请求服务端数据时需要**刷新页面（GET请求）**或者**局限于一些特定的结构功能**中（表单POST，特定元素href等）  
+ AJAX介绍：  
  + Asynchronous JavaScript and XML(异步的 JavaScript 和 XML)，现在json取代xml  
  + 浏览器提供的一套API，即通过网络编程的方式，利用js代码发送网络请求，使得发送请求与获取数据更为灵活  
  + AJAX请求本质上还是http请求，遵循http协议  
 
## 1. API使用
1. 基本创建  
```javascript
//1. xhr类似于浏览器，用户代理
var xhr = new XMLHttpRequest();
//2. 打开浏览器，输入网址
xhr.open('请求方法',url, '是否异步'); 
//3. 发送请求
xhr.send() //post的请求体放入这里的参数
//4. 获取响应内容，并回调
xhr.onload=()=>{console.log(responseText)}
or
xhr.onreadystatechange=()=>{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```  
onload:成功
onerror:失败
2. readyState  
   + 0 => 初始化代理对象xhr（请求未初始化）  
   + 1 => 已经调用open,与服务器端口80建立链接（链接已建立）  
   + 2 => 已经接受到了响应报文的响应头（请求已接受）  
      + 还没有拿到报文体，获取报文头：getAllResponseHeader()（请求处理中） 
   + 3 => 正在下载响应体。有可能为空，也有可能不完整（请求处理完成）  
   + 4 => 整个报文完整下载 