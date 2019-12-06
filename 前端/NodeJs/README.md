# 来吧 Node.js
######Date：2019-10-1　　　Writer:均远
先BB几句：  
　　主攻的React框架，但之前在做服务器渲染时发现babel支持es6这块有个坑填不上，之后就异常抵触node，于是学了flask。然鹅，昨天与某鹅面试官的全程尬聊，也算让我认识到了自己的许多不足，作为年轻的小猿就这么排斥新技术，以后还想不想飞黄腾达了（狗头）？！  
　　我决心不再回避了，来吧Node.js，亮剑吧！  
  
##Node.js简介
　　官方解释：node.js是js运行时的环境，使用事件驱动和非阻塞IO模型（异步）,轻量且高效。其伴生的npm是世界上最大的开源生态系统，绝大多数js相关包都存放在了npm上，方便开发人员下载。node移植于Chrome V8引擎，which is 目前公认解析js最快的引擎.<br>  
　　作用：可以解析和执行js代码（类似浏览器）。使得js能够脱离浏览器执行。但此时的js与浏览器中的js有所不同：  
* 浏览器中js：ECMAScript,Bom,Dom  
* node.js中：有ECMAScript，没有DOM和BOM，但额外提供了一些服务器级别的API  
  * 文件读写  
  * 网络服务的构建
  * 网络通信  
  * http服务器等　　
  
  本文主要记载 API 的使用  
##Node.js用途  
1. Web服务器后台  
2. 命令行工具等  
##Node.js下载安装  
1. 官网下载  
2. 一路安装，配置环境变量  
3. 命令行查看版本node --veision显示当前版本号即成功

## Node须知  
#### 1.黑盒模型与"哑巴"  
与java,php不同，Node开启的web服务器默认不会向外公布任何文件，若要实现公开能访问，需要开发者设置；访问资源需要通过事先设定好的url访问，url通常不会暴露文件地址或者文件名信息 
##目录
  
2. [npm和包文件](npm_package.md)
3. [模块系统](mokuai.md) 
4. [核心模块](1.main.md)
5. [模板引擎](2.art-template.md)  
6. [Express框架](express.md) 
100. [注意事项](attention.md)  