# MongDB
简介：非关系型数据库。  
+ 关系型数据库  
    + 所有的关系型数据都需要通过sql语言来操作  
    + 所有的关系型数据都需要设计表结构  
    + 所有的关系型数据都支持约束  
+ MongDB  
    + 数据库结构  
        + 数据库=>数据库  
        + 数据表=>集合（数组）  
        + 表记录=>文档对象  
    + 不需要设计表结构  
##使用说明  
###1. 启动和关闭数据库  
启动：
```
# 默认使用命令行根盘目录下/data/db作为存储目录，若没有会报错
mongod
```  
如果想要修改默认的数据存储目录，可以：
```
mongod --dbpath=数据存储目录 
```  
停止：`Ctrl+c`  
###2. 连接数据库  
连接与退出：
```
# 默认链接本机的mongodb服务
mongo
# 退出
exit
```  
## 3.基本命令  
+ `show dbs` ： 显示所有数据库  
+ `db` ： 显示当前的数据库  
+ `use 数据库名称` ： 切换到指定数据库，没有则新建并切换到该数据库，但必须要有数据才会真正新建  
+ `db.表名.insertOne（json）` ：向表名中插入一行数据  
+ `show collections` ： 显示表名（集合）  
+ `db.表名.find()` ： 显示集合所有内容  
## 4.操作MongoDB  
###一、使用官方的`mongdb`包  
###二、使用第三方`mongoose`包  
+ 安装：  
```
npm i mongoose
```  
+ 创建数据库：  
   + 连接数据库  
    ```
    var mongoose =require('mongoose');
    
    //链接数据库，第一个参数为链接的数据库名字，不存在也没关系，一旦数据库里创建了数据，数据库会自动建立
    mongoose.connect('mongod://localhost/test',{ userMongoClient:true });  
    ```  
    + 设计文档模型结构schema（表结构）
    ``` 
    var userSchema = new Schema({
        username:{
            type:String,
            reuired:true
        },
        XXX{
        }
    })
    ```
    + 将结构发布为模型  
    ```
    var Person = mongoose.model('Person',userSchema) // =>最终会生成小写的cats集合  
    ```  
+ 新增数据库  
    + 创建实例，新增文档  
    ```
    var jim = new Person({
        username:Jim,
        XXX:XXX
    })
    ```
    + 保存到数据库  
    ````
    jim.save((err,result)=>{
        //result 是刚存储的数据
    })
    ````  
+ 查询数据库  
   + 查询所有：  
   ```
   Person.find( (err,result) => {} )  
   ```  
   + 条件查询：
   ```
   Person.find( {条件}, (er.re)=>{} )  //返回数组  
   Person.findOne( {条件}, (er.re)=>{} )  //返回单个对象
   ```  
   + 复合条件查询：  
   ```
   
   ```  
+ 删除数据  
   find = > remove  
+ 更新修改  
   ```
   //更新所有
   update(conditions,doc,callback)
   //更新一个
   findOneAndUpdate(conditions,doc,callback)
   //根据id更新一个
   finByIdAndUpdate(cond,doc,(er,re)=>{})
   ```
     

