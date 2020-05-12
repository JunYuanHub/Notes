[走你！](https://juejin.im/post/5cd2ce1e6fb9a032092ea160)  
## 生成器函数  
生成器函数：状态机。yield处中断。next(x)开启下一个状态，yield本身不返回值，x指定为上个yield的返回值。  
## async and await  
async保证return的必定是个promise对象；  
await会等到后面的（异步）代码执行完后马上跳出当前函数去执行主线程其他内容。（如果是普通异步代码，挂起，按正常执行；如果后面是promise，则会等待promise里的异步全部执行完并返回）  
yield返回一个promise。没完成继续调用next（）  
~~~  
// 定义了一个promise，用来模拟异步请求，作用是传入参数++
function getNum(num){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(num+1)
        }, 1000)
    })
}

//自动执行器，如果一个Generator函数没有执行完，则递归调用
function asyncFun(func){
  if(!gen) return
  var gen = func();

  function next(data){
    var result = gen.next(data);
    if (result.done) return result.value;
    result.value.then(function(data){
      next(data);
    });
  }

  next();
}

// 所需要执行的Generator函数，内部的数据在执行完成一步的promise之后，再调用下一步
var func = function* (){
  var f1 = yield getNum(1);
  var f2 = yield getNum(f1);
  console.log(f2) ;
};
asyncFun(func);
~~~