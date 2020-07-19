## koa  
轻量级nodejs服务端框架，易于拓展，本身并不封装功能  
###1.使用  
+ 基础使用  
    ```
    cosnt Koa = require('koa') 
    
    cosnt server = new Koa()
    server.listen(3000,()=>{
        console.log('koa is running a 3000')
    })
    ```   
    + ctx封装了原生的node请求和响应  
       + ctx.req是原生的node中的request  
       ctx.request是koa中的对象,框架间可能不兼容  
       + ctx.res是原生的response  
       ctx.response同理  
    + ctx.body || ctx.set('Context-Type','application/json')等 
+ 中间件  
    ```
    //所有的请求均按顺序经过中间件处理
    //ctx=>请求相关信息，next下个中间件
    server.use(async (ctx,next)=>{
     
        //如果要执行下一个中间件,不需调用next()，否则不会再调用下个中间件
        await next()
    })
    
    ```  
###2. koa-router  
```
const Router= require('koa-router')
const router = new Router()

router.get(url:params,(ctx)=>{
    处理函数
})
server.use(router.routes())
```  
###3. koa-static  
注意：公开public目录后，获取文件输入路径时不要输入public,比如图片在/public/img/1.png，直接输入./img/1.png
```
npm install koa-static --save

//比如我们要公开public目录
const path = require('path')
const staticFiles = require('koa-static')
server.use(staticFiles(path.join(__dirname + './public/')))  
//或者这样：
server.use(require('koa-static')(__dirname,'/public'));
```