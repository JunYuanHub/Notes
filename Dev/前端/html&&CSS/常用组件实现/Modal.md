## 模态窗  
```  
<div id="wrapper">
    <div id="content">
    // content
    </div>
</div>
```  
1. wrapper采用绝对布局，覆盖整个页面，visibility控制可视化。  
2. 调用函数切换visibility  
3. content可利用margin、transition等实现平滑动画  
  
> 注意:opacity：0可触发事件，visibility：hidden和display：none不会触发