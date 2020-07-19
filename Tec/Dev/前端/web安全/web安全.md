# 网站攻击  
## 一、XSS  
跨站脚本（Cross-site scripting，通常简称为XSS）是一种网站应用程序的安全漏洞攻击，是代码注入的一种。它允许恶意用户将代码注入到网页上，其他用户在观看网页时就会受到影响。这类攻击通常包含了HTML以及用户端脚本语言。  
## 分类  
存储性XSS（数据库注入）、反射型XSS（URL注入）、DOM型XSS（DOM注入，前端范围）  
## 注入方式：  
1. 在 HTML 中内嵌的文本中，恶意内容以 script 标签形成注入。
2. 在内联的 JavaScript 中，拼接的数据突破了原本的限制（字符串，变量，方法名等）。
3. 在标签属性中，恶意内容包含引号，从而突破属性值的限制，注入其他属性或者标签。
4. 在标签的 href、src 等属性中，包含 javascript: 等可执行代码。
5. 在 onload、onerror、onclick 等事件中，注入不受控制代码。
6. 在 style 属性和标签中，包含类似 background-image:url("javascript:..."); 的代码（新版本浏览器已经可以防范）。
7. 在 style 属性和标签中，包含类似 expression(...) 的 CSS 表达式代码（新版本浏览器已经可以防范）。  
## 解决办法  

> 防御措施
> 1. 过滤特殊字符（如js）
> 2. 转义特殊字符(<>等)  
> 3. 使用 HTTP 头指定类型  
> 4. 避免拼接 HTML. 如果框架允许，使用 createElement、setAttribute 之类的方法实现。或者采用比较成熟的渲染框架，如 Vue/React 等。
  
## 二、CSRF  
### 1. 特点
1. 攻击一般发起在第三方网站  
2. 攻击利用受害者在被攻击网站的登录凭证(如cookie)，冒充受害者提交操作；而不是直接窃取数据。  
3. 攻击者并不能获取到受害者的登录凭证，仅仅是“冒用”。  
4. 跨站请求可以用各种方式：图片URL、超链接、CORS、Form提交等等。部分请求方式可以直接嵌入在第三方论坛、文章中，难以进行追踪。  
### 2. 防范措施  
1. 同源检测。一般的异步请求都会有origin和referer，可以用来确定来源地址  
2. SCRF token。在原页面生成token（服务端存储在session），请求时附带上进行验证。  
3. 双重cookie，将部分cookie嵌入到请求中用来验证。  
4. sameSite Cookie:  
   `Set-Cookie: foo=1; Samesite=Strict`  
   + Samesite=Strict:表明这个 Cookie 在任何情况下都不可能作为第三方 Cookie  
   + 假如这个请求是这种请求（改变了当前页面或者打开了新页面）且同时是个GET请求（不能是异步和跳转），则这个Cookie可以作为第三方Cookie。  
   > Samesite Cookie目前有一个致命的缺陷：不支持子域。  
     
## 三、CSP（Iframe嵌套）  
1. [新开窗口](https://imweb.io/topic/584cd0459be501ba17b10aaa)  
    opener引发的血案。  
    chrome有不同的标签页面使用不同进程和线程，但是有个例外，通过a标签的target="_blank"属性，或者window.open(url)在新窗口中打开页面, 会与父窗口共用进程和线程。  
    2. [深入浅出Iframe](https://www.jianshu.com/p/7ec986aa28a7)  
    Iframe广告劫持  
    1. `<meta http-equiv="Content-Security-Policy" content="child-src 'unsafe-inline' 'unsafe-eval' www.easonwong.com">`  
    2. 通过HTTP头部信息加上Content-Security-Policy字段

