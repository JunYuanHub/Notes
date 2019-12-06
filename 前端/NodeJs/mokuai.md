# 模块系统  
##产生背景：  
　　nodejs无法同时执行多个文件，解决办法就是让一个文件以代码形式执行另一个文件，这个过程就用到了require（），它用来导入模块；　　
  
+ nodejs的模块：  
　　   1. 具名的核心模块。如fs,os,http等  
　　   2. 用户自己编写的核心模块。导入时注意相对路径编写必须加 './'  
　　   3. 第三方导入包。导入方式类似核心模板 
## 导入与导出：  
node中，没有全局作用域，只有模块作用域：外部/内部互相访问不到，不会污染；如果要暴露，则使用exports  
+ 导入require:  
   + ```javascript
     var 变量名= requrie('模板名')   
     ```  
   两个作用：  
   + 执行被加载的模板文件  
   + 得到被加载的exports导出接口的对象  
     
   加载规则：  
   + 优先从缓存加载  
   + 导入第三方模板时，先找到对应目录下的node_modules目录，然后找到对应的package.json中main属性，没有main.js默认寻找index.js文件，main属性记录了该模板的入口模板文件  
   + 如果当前目录没有node_module，则往上寻找，没有继续往上知道磁盘根目录没有，报错
   
+ 导出exports:  
   + 导出多个目标
     ```javascript
     exports.a="hello" //将a挂载到exports里，后续调用，需要.a出来  
     exports.b=function() {
        console.log('hello')
     }  
     module.exports = {多个目标}
     ```  
   + 导出单个目标
       ```javascript
     module.exports=function() {} //后面导出的会覆盖前者，导入后直接就是该对象
       ```   
 + 原理解析  
    + exports只是引用了=>module.exports。对每个模板的引用最终都是用return的module.exports；对exports赋值会让其脱离module.exports的引用关系