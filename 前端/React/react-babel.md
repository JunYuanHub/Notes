## （1）装饰器方式连接redux  
1. npm run eject （反编译create-react-app的封装，实现自定义配置webpack）  
2. npm install --save-dev @babel/plugin-proposal-decorators 
3.  配置package.json
    ```
    "babel": {
        "presets": [
          "react-app"
        ],
        "plugins": [
          [
            "@babel/plugin-proposal-decorators",
            {
              "legacy": true
            }
          ]
        ]
      }
    ``` 
4. 没有对比就没有伤害  
    ```
    /* 修改前
     const mapStatetoProps = (state)=>{
        return {num : state}    //需要哪些状态数据
    }
     //需要执行的方法
     const actionCreator = { hire, hireAsync ,fire }
     export default App = connect(mapStatetoProps ,actionCreator)(App)
    */
    
    // 修改后
    @connect(
      //需要哪些状态数据
      state=>({num : state}),
      //需要执行的方法，自动dispatch
      { hire, hireAsync ,fire }
    )
    ```  
5. 注意：装饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。另一方面，如果一定要装饰函数，可以采用高阶函数的形式直接执行。
