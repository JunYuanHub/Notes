#Redis  
以key-val形式存储  
###API  
+ set key value  
+ setex key ex(过期时间) val  
+ get key  
+ KEYs * =>获取所有keys  
+ DEL key  
###连接nodejs  
+ ioredis  
    ```
    async function test(){
        const Redis = require('ioredis')
        
        const redis = new Redis({
            port:6378,
            password:123456
        })
        //读取数据库是异步的
        const keys = await redis.keys('*')
        console.log(keys)
    }
    test()
    ```