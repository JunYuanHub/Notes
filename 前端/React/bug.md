### Bug  
1. 相同pathname下改变params不会触发组件更新（测试显示检测不到props.router改变）,解决办法：中间页面跳转