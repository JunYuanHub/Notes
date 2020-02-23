# 一、作用  
嵌套多层次传递数据，无需中间组件通过props传递。  
# 二、使用  
1. 创建context：`let ctx = React.createContext("默认值")`  
2. 外层组件引入ctx，并包裹需要传递数据的子组件：  
   ~~~  
   <ctx.Provider value="传递的值">
     // 子组件
   </ctx>
   ~~~
3. 子组件获取ctx，有两种方式：  
   ```  
   import {Data} from './context'
   
   // 1.借助contextType
   class Children extends React.Component{
       render() {
           return(<div>这是子组件，data为：{this.context}</div>)
       }
   }
   Children.contextType = Data
   export default Children;
   
   // 2.借助consumer  
   <Data.Consumer>
       {data=>(
           <div>这是wrapper,data为：{data}</div>
           )}
   </Data.Consumer>
   
   // 3.借助hook
   const Children = (props,context)=>{
       const data = useContext(Data)
       return (
           <h1>Data is {data}</h1>
       )
   }
   ```