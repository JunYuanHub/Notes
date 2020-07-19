## state hook  
+ useState  
    + const [count,setCount] = useState(0)  
    在函数组件刚挂载时会执行，之后更新不会再执行；setState(c=>{}),c是最新的state对应值，这里要调用回调函数，不然触发闭包陷阱，传给外层函数的state从刚开始就固定了  
    + 另外如果不传入新的对象，而是给其赋值的话，子组件无法判断是否改变，进而无法渲染更新  
+ useReducer  
    + 
    ```
    function countReducer(state,action){
        swich(ation.type){
            case 'add':
                return state+1
            case 'minus':
                return state-1
            default:
                return state
        }
    }
    
    function MyCountFunc=()=>{
        const [count,dispachCount] = userReducer(countReducer,0)
        useEffect(()=>{})
    }
    ```  
## Effect hook  
+ useEffect  
    ```    
    userEffect(()=>{
        A;
        return B
    },[dependencies])
    ```
    默认每次组件重新渲染时执行A，加入dependency控制后，每次检测到dependencies中的state变化时才会执行A,当组件重新渲染时执行return的清除语句
    + 默认情况，类似于componentDidAmount和DidUpdate  
    + 一般return语句用于清除组件订阅等操作。  
+ useLayoutEffect  
    在更新状态后，计算出节点树但还未更新到HTML的DOM之前执行；useEffect是之后执行  
    在较长时间的请求时，使用useLayoutEffect会卡住DOM，用户体验不佳，避免用  
## Context Hook  
## Ref hook  
+ useRef
    ```
    import {useRef} from "react" 
    
    const domRef = useRef()
    
    <Dom ref={domRef}></Dom>
    
    即可通过{domRef}获取该节点
    ```  
## hook优化(ComponentShouldUpdate)  
+ memo,useMemo,useCallback  
优化原理：useMemo帮助记忆特定部分是否更新。限制render部分只有在特定state更新时才更新
    + 先用memo组件包裹DOM组件（即return DOM的部分），检测组件  
    + 将组件中声明的部分提取出来，如匿名函数声明，变量声明  
       + 每次调用函数组件都会重新声明，会自动触发组件更新    
    + 用useMemo包裹这些声明部分useMemo（（）=>orig,[dependency]）  
       + 如果是函数声明==>   
       + useMemo（()=>orig）,useCallback(()=>()=>orig )  
## 闭包陷阱  
解决办法：使用useRef  
useRef.current=target永远获取的是最新的state  

##HOOK使用规则  
1. 只在最顶层使用 Hook  
    + 不要在循环，条件或嵌套函数中调用 Hook，确保 Hook 在每一次渲染中都按照同样的顺序被调用
2. 只在 React 函数中调用 Hook  
    + 不要在普通的 JavaScript 函数中调用 Hook

