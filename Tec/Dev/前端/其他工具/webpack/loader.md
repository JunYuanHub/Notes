## 作用  
1. 将打包模块中无法解析的文件类型解析为js文件，或者转换ES67至指定版本的ES(babel)  
2. 每个test的loader数组，默认从右向左执行,从下向上执行
3. 每个loader尽量保持单一功能(css-loader,style-loader)方便移植。  
## 使用  
``` 
... 
    module:{         //模块
        rules:[{
            test:/\.css$/,                     //正则匹配loader要适用的文件类型
            use:['style-loader','css-loader'],   //css解析@import，style解析css语言
            //或者对象形式传入，这样可以传入options
            // use:[
            //     {
            //         loader:'style-loader'，
            //          opstions:{
            //              insert:'head';      //提高优先级，覆盖原HTML的样式
            //          }
            //     },
            //     'css-loader'
            // ]   
        }]
    }
...
```