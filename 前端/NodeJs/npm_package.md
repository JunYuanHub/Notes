# npm and package.json
产生原因：  
node_module会将包和包的依赖(项目可能并没有直接使用包的依赖)全部安装，难以查看项目依赖的包，并且在node_modules丢失后更难以查找。于是诞生了package.json(包描述文件 => 包的说明书)
## 一、npm  
即：node package manager 
 
#### 1. npm常用命令：  
+ 查看版本:`node --version /-v  `  
+ 查看配置:`npm config list`  
   + set sth sth 更改配置
+ 执行文件:`npm filename ` 　　　　　　　　(需要先定位到该目录下）  
+ 安装模板:`npm install `  
   + 'name' 安装包，不加name则直接安装package.json所有依赖包 
   + --global || -g 安装到全局 通常用于命令行工具
   + --save会保存到dependencies  
   + --dev会将包保存到devDependencies  
      + –save || -S ： dependencies 键下，发布后还需要依赖的模块，譬如像jQuery库或者Angular框架类似的，我们在开发完后后肯定还要依赖它们，否则就运行不了。
      
      + –save-dev|| -D ： devDependencies 键下，开发时的依赖比如webpack,gulp,babel因为我们在发布后用不到它，而只是在我们开发才用到它。  
   + --global npm 自己更新自己  
+ 删除包：`npm uninstall / un ` 
   + 只删除，依赖项会保留  
   + --save 依赖项同时删除
+ 初始化package.json：`npm init  `
   + -y 可以跳过向导，快速生成  
#### 2. 解决下载速度慢问题  
+ 使用淘宝镜像源：cnpm  
   + npm install --global cnpm  
   + 然后用cnpm代替npm执行安装命令即可  
+ 不安装淘宝镜像，但使用它的服务器：  
   + 每次安装：npm install jquery --registry=https://registry.npm.taobao.org
   + 一次配置：npm config set registry https://registry.npm.taobao.org    
## 二、package.json  
创建：通过`npm init`自动初始化（会让你初始化信息）
+ main:入口文件  
+ dependencies：依赖文件，如果node_modules被删除，npm install会把所有包重新安装一遍  
+ scripts：存储命令行的简写代码  
+ ^aa.bb.cc安装当前大版本下最新的版本（不会更新大版本）  
## 三、package-lock.json  
作用：
+ 5版本以后的npm不需要加--save，它会自动保存依赖。当安装包的时候npm会生成或者更新这个lock文件 
+ 记录依赖树信息：lock文件还会保存所有包依赖树信息（比如下载地址），如此，重新下载包时不用解析包之间的依赖，下载速度更快  
+ 锁版本号：保存了具体的版本号。package.json一般保存的是^版本。防止自动升级新版导致版本冲突

