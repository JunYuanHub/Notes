# Express  
框架，用于简化http模板的操作  
## 1. 使用nodenon  
+ 作用：工具，通过nodemon启动的服务，会监听文件的变化，当发生变化时自动重启服务，即调试模式  
+ 安装：`npm install --global nodemon ` 
## 2. 搭建服务器  
+ 基本搭建：
    ```javascript
    //安装引包
    const express= require('express');
    //创建服务器
    const app = express();
    
    //公开资源
    app.use('/public/',express.static('./public'));
    
    //当服务器收到get请求时，执行回调函数；已经处理好了中文乱码，很贴心
    app.get('/',(req,res)=>{
        res.status(200).send('请求内容为：nothing')
    });
    
    //开启端口，监听器
    app.listen(3000,function () {
        console.log('server in running at port 3000')
    })
    ```  
+ 静态资源服务  
路由：url与其对应资源或程序的映射关系  
公布静态资源，使得客户端可通过路由路径访问该目录下的所有文件  
    ```javascript
    app.use(路由与SPA,express.static('文件目录')) 　　//访问方式：/public/+文件名；注意文件目录要以启动服务的目录为准
    app.user(express.static('/public/')) 　　　　　　　　　　　 //此时可以省略/public/，直接加具体文件路径访问
    ``` 
　　即通过‘路由’访问‘文件’  
+ 其他优化  
express封装了许多API  
   + req可以直接.query获取请求参数  
   + req.redirect('')取代了底层的statusCode和setHeader(location) 
## 3. 使用模板引擎  
+ 安装  
```
npm install --save art-template
npm install --save express-art-template 
```  
+ 配置  
```
app.engine('art'(文件后缀名)，require('express-art-template'))  //会自动加载包，不需要手动导入
```
+ 使用  
```
app.get('/',(req,res)=>{
    //默认会去目录Views下去找该文件
    res.render('index.art'，{键值对})
})
//修改默认目录
app.set('Views',目录路径)
```  
## 4.框架API  
+ 解析POST请求  
需要用到第三方包，也是中间件:  
`npm install --save body-parser`  
```
const express = require('express')
const bodyParser = require('body-parser')

const app=express()

//配置:加入配置后，在req中会解锁body属性，用于取出post表单数据
app.use(bodyParser,urlencoded({extended:false}))
app.use(bodyParser.json())

```  
+ 路由系统  
express提供了一个路由容器，便于将Route文件分离出来  
```
const router = express.Router()
router.get(...)
router.post(...)
module.exports = router

//引入文件并挂载
cosnt router = require('router')
app.use(router)
```




