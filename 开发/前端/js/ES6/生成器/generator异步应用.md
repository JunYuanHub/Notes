## 一、扩展
### 1. 协程  
协程有点像函数，又有点像线程。它的运行流程大致如下。

第一步，协程A开始执行。  
第二步，协程A执行到一半，进入暂停，执行权转移到协程B。  
第三步，（一段时间后）协程B交还执行权。  
第四步，协程A恢复执行。  

上面流程的协程A，就是异步任务，因为它分成两段（或多段）执行。  
### 2. 传值调用与传名调用  
传值调用：在进入函数体之前，就计算传入参数的值，再将这个值传入函数f。JS，C 语言就采用这种策略。  
传名调用：直接将参数的表达式传入函数体，只在用到它的时候求值。Haskell 语言采用这种策略。    
## 二、generator异步处理=>自动执行化  
要实现自动执行所有的异步处理关键在于如何交回执行权。
### 1. thunk  
Thunk，一种“传名调用”实现策略，用来替换某个表达式。（Redux-thunk允许action替换为函数）  
  
在 JavaScript 语言中，Thunk 函数替换的不是表达式，而是多参数函数，将其替换成一个只接受回调函数作为参数的单参数函数（类似函数柯里化，但只拆分成两步，且第二步只接受回调函数为参数）。  
Thunkify 的源码  
```  
function thunkify(fn) {
  return function() {
    // ...args即可
    var args = new Array(arguments.length);
    var ctx = this;

    for (var i = 0; i < args.length; ++i) {
      args[i] = arguments[i];
    }

    return function (done) {
      var called;

      args.push(function () {
        if (called) return;
        called = true;
        done.apply(null, arguments);
      });

      try {
        fn.apply(ctx, args);
      } catch (err) {
        done(err);
      }
    }
  }
};
```  
### 2. CO模块  
回调+promise实现