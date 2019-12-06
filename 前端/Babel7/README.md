# @ Babel7  
[参考链接](https://www.jianshu.com/p/cbd48919a0cc)  
用途：  
+ 解决不同版本node环境、浏览器对于es语法差异性和支持性  

babel 7.X的主要变更：
+ 删除对未维护的 Node 版本的支持：0.10,0.12,2,5
+ 删除“Stage” & 年度预设（preset-es2015 等）， 用@babel/preset-env 取代。
+ 对部分软件包进行重命名（e.g. babel-core–>@babel/core） 
## 1. 常用组成成分  
+ @babel/cli
+ @babel/core
+ @babel/preset-env
+ @babel/polyfill
+ @babel/runtime
+ @babel/plugin-transform-runtime
+ @babel/plugin-transform-xxx  
## 2.使用介绍  
+ @babel/cli+@@babel/core+@babel/plugin-transform-xxx   
    + cli提供`babel`这个命令行来对js文件进行编译，但依赖于core  
    + core含有执行编译的transform方法。但还是不能编译，因为6将插件分离出去了，默认情况下babel不会编译代码。  
    + plugin-transform-xx。指定了编译对象，如`plugin-transform-arrow-functions`编译箭头函数  
    + 有了以上三个包，可以开始编译了，但大量plugin启动输入命令行很繁琐：  
        ```
        --plugins @babel/plugin-transform-arrow-functions *n
        ```  
    + .babelrc配置文件。cli在调用之时都会去调用.babelrc文件，这样就不用写老长的命令行参数了  
        ```
        {
          "plugins": [
            "@babel/plugin-transform-arrow-functions"
            "@babel/plugin-transform-block-scoping" 
          ]
        }
        ```  
    + 但过多的插件配制还是很繁琐。于是产生配置的预设@babel/preset-env  
        ```
        {
          "presets": [
            [
              "@babel/preset-env",
              {
                "targets": {
                  “chrome”:58,
                  "node": "10"(版本号)
                }
              }
            ]
          ]
        }
        ```  
    + 还有一个问题，虽然语法转换了，但有些浏览器不支持某些语法。babel-polyfill 处理第二种情况 - 让目标浏览器支持所有特性  
        + 那么要在编译后的代码里加上`require('@babel/polyfill')`  
    + 其他：  
        + @babel/runtime+@babel/plugin-transform-runtime  
        编译之后的index.js代码里面有不少新增加的函数，runtime将这些函数统一模板化。plugin-transform-runtime实现自动导入这些模板
+ babel-plugin-import  
用于按需加载包
    ```
    配置pakage.json
    "plugins":[
        ["import",{"libraryName":"antd"}]
    ]
    
    import { Button } from 'antd'
    => import Button from 'antd/lib/button'
    ```