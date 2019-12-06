# Webpack  
##一、介绍  
+ **产生背景：**  
　　网页中加载的静态资源变多后（js,css,img,字体文件，模板文件等），需要发送很多的二次请求，网页加载速度慢，且要处理错综复杂的依赖关系　　
+ 解决办法：  
   + 合并。减少二次请求  
   + 压缩。加快加载速度  
   + 精灵图。  
   + 图片base64编码。可以第一次变随着html发送并加载  
+ Webpack  
  是前端的一个基于nodejs开发的项目构建工具。可以帮助开发者解决依赖关系，进行压缩，合并  
  + gulp基于小范围工作点构建  
  + webpack基于项目构建  
+ 用途：  
  + 处理js文件的相关依赖关系  
  + 能够把浏览器不识别的，高级的语法转化为低级的，能识别的语法 (还需借助babal)  
##二、基本使用  

+ 单独使用：cmd:　**webpack 入口文件 输出文件（默认./dict目录下）名**  
+ 配置文件使用：新建`webpack.config.js`文件  
    ```
    //单入口文件
    const config = {
        //入口文件，要打包的文件
        entry:path.join(__dirname,'./src/main.js'),
        //输出文件的相关配置
        output：{
            path:path.join(__dirname,'./dist'),
            filename:'bundle.js'
        }
    }
    //多入口文件
    const config = {
         entry: {
           app: './src/app.js',
           search: './src/search.js'
         },
         output: {
           filename: '[name].js',
           path: __dirname + '/dist'
         }
       }            
       // 写入到硬盘：./dist/app.js, ./dist/search.js
    
    module.exports = config
    ```  
    1. webpack没有从命令行接受入口出口文件，便回去根目录下寻找配置文件  
    2. 找到该文件后，根据配置解析并执行打包构建  
##三、使用webpack-dev-server  
1. 类似nodemon=>node，能够实时监控代码变化，重新打包文件  
2. 安装：**npm -i webpack-dev-server -D**  
3. 常用命令(建议将命令加入package.json的script)：  
    ```
    //package.json中
    script:{
        dev:'webpack-dev-server --open --port 3000 --contentBase XXX --hot'
    }
    
    //webpack.config.json中
    const webpack = reuire('webpack) //启用热更新需要
    devserver:{
        open:true,
        port:3000,
        contenBase:'src',
        hot:true
    }，
    plugins:[
        new webpack.HotModuleReplacementPlugin() //启用热更新需要    
    ]
    ```
    + webpack-dev-server 开启服务  
        + dev根据帮我们打包好的bundle.js文件以内存形式托管到项目根目录中，要生效，注意路径  
    + --open开启后自动打开服务器界面  
    + --port XXX 修改端口号  
    + --contentBase XXX 修改服务器根目录  
    + --hot 热更新。打补丁修改，不会生成新的bundle.js，无刷新更新。异步修改代码，无刷新接口更新  
## 四、html-webpack-plugin  
作用：在内存中生成html文件，且会自动引用bundle.js   
+ 安装：`npm install html-webpack-plugins`  
+ 使用：  
    ```
    const htmlWebpackPlugin = require('html-webpack-plugin')  
    
    plugins:[
        new htmlWebpackPlugin({
            template://指定的模板页面，将来会根据指定的模板生成，
            filename：‘index.html’  //指定生成的页面的内容
        })
    ]
    ```  
## 五、非js文件的处理  
webpack默认只能处理js类型文件，其他的文件需要加载第三方loader  
+ css文件  
    1. `npm install style-loader css-loader -D`  
    2. 配置webpack.config.js文件：module对象rules数组 => 存放了所有第三方文件的匹配规则和处理规则  
        ```
        module{
            rules{
                {test:/\.css$/,use:['style-loader','css-loader']} //从后往前调用
            }
        }
        ```  
+ less/sass文件  
    ```
    rules{
        {test:/\.css$/,use:['style-loader','css-loader','less-loader']} //从后往前调用
    }
    ```  
+ url(如img链接)  
    ```
    test:/(png|jpg|gif|bmp|jpeg)$/, use:'url-loader?limit=7631&name=[hash:8]-[name].[ext]'  
    => limit:给出限定值
        => 当图片实际大小<limit,将图片转为base64字符串；若>=limit,按照原格式url存储  
    => name：图片的新命名 
        => [name]，之前图片的name；[ext]之前图片的拓展名  
        => [hash:8],此时可能重复命名。故在前面加哈希值（最大32位）
    ```  
+ 字体文件  
    ```
    { test: /(\.(ttf|eot|woff|woff2)$)/, use:'url-loader'}
    ```  
## 六、高级js语法  
默认webpack仅支持部分es6语法，对于不支持的语法需要借助babel转化。详情见：[babel](./babel.md)  
```
module: {
    rules: [
      {
        // 对以 `.js` 结尾的文件使用 `babel-loader` 处理
        // `babel-loader` 会自动加载`babel.config.js` 配置文件
        test: /\.js$/,
        use: 'babel-loader',

        // 排除 `node_modules` 目录，不对它做处理
        exclude: /node_modules/
      }
    ]
  },
```
        