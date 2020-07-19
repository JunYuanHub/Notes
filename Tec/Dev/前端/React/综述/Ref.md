1. React 会在组件挂载时给 current 属性传入 DOM 元素，并在组件卸载时传入 null 值。  
   ref 会在 componentDidMount 或 componentDidUpdate 生命周期钩子触发前更新。
   ```
   this.myRef = React.createRef();
   
   <APP ref={this.myRef}></App>
   
   this.myRef.current
   ```   
2. 函数组件没有实例，所以不能使用ref  
3. [转发ref](https://react.docschina.org/docs/forwarding-refs.html)