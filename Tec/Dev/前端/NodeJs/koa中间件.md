## 原理  
实例化koa时内部会生成一个中间件数组，当调用use方法时会向数组中传入中间件，内部有个compose函数，倒循环依次把所有中间件用async，await包装(Promise对象)并传入ctx和next参数，然后作为next传入给上一个中间件  
  
所以当我们调用中间件的next时，就会进入下一个中间件，结合async和await可以实现洋葱模型。