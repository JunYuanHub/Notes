## 一、组件  
1. 类组件。有生命周期与状态，继承React.Component  
2. 无状态组件（函数组件），并不继承React.Component  
3. PureComponent  
   pureComponent和Component的功能几乎一样，但 PureComponent的shouldComponentUpdate
   不会直接返回 true 而是会对属性和状态进行浅层比较，也就是仅比较直接属性是否相等。  
   
### （1）. 何时使用Component或PureComponent
1、当组件是独立的，组件在页面中的个数为1或2的，组件有很多props，state，并且当中还有些是数组和对象的，组件需要每次都渲染的，使用Component  
2、当组件经常作为子组件，作为列表，组件在页面中数量众多，组件props, state属性少，并且属性中基本没有数组和对象，组件不需要每次都渲染，只有变化了才渲染，使用PureComponent
### （2）. PureComponent问题
1、数组和对象的浅比较，只比较引用，所以数组和对象内部产生变化，但引用未变的话，则不会重新渲染。而Component不会有这问题。  
2、浅比较也要计算，也需要花费时间  
## 二、周期  
### （1）挂载阶段  
~~~
• constructor() 
• componentWil!Mount() 
• render() 
• componentDidMount()  
~~~  
### （2）更新阶段  
React更新组件三种方式：父组件更新、自身状态变化、自身强制更新。  

1. 当父组件发生变时，子组件需要重新渲染，此时会触发下面的函数  
   ~~~
    •componentWillRceveProps()
    •shouldComponentUpdate()
    •componentWillUpdate()
    •render()
    •componentDidUpdate()  
   ~~~
2. 当自身状态发生变化，就是调用setState时，会触发下面的函数
    ~~~  
    •shouldComponentUpdate()
    •componentWilIUpdate()
    •render()
    •componentDidUpdate()  
    ~~~
3. 调用forceUpdate会发生强制更新，此时会触发下面的函数
    ~~~  
    •componentWillUpdate()
    •render()
    •componentDidUpdate()  
    ~~~
shouldComponentUpate可以用来提升性能，componentWillReceiveProps般用来将新的props步到tate  
### (3)卸载阶段  
当组件被卸载时会执行 componentWillUnmount 函数，一般会在这个函数里做一些清理工作，比如清除定时器（不清理会一直留在内存当中）、解绑自定义事件等