## Bind  
```
// ES6简单版 支持函数柯里化  
function MyBind (ctx) {
    let self = this
    let args = [...arguments].slice(1)
    return function () {
        self.apply(ctx,[...arguments].concat(args))
    }
}

// ES5
Function.prototype.bind = function() {
  if (typeof this !== 'function') {
    throw new TypeError(`${this} is not callable`);
  }
  var self = this;
  var slice = [].slice;
  // 模拟es6的解构效果
  var that = arguments[0];
  var argv = slice.call(arguments, 1);
  return function() {
    // slice.call(arguments, 0)将类数组转换为数组
    return self.apply(that, argv.concat(slice.call(arguments, 0)));
  };
};

// 继承原型版本
Function.prototype.bind = function(that, ...argv) {
  if (typeof this !== 'function') {
    throw new TypeError(`${this} is not callable`);
  }
  // 保存原函数
  let self = this;
  let func = function() {};
  // 获取bind后函数传入的参数
  let bindfunc = function(...argu) {
    return self.apply(this instanceof func ? this : that, [...argv, ...argu]);
  };
  // 把this原型上的东西挂载到func原型上面
  func.prototype = self.prototype;
  // 为了避免func影响到this，通过new 操作符进行复制原型上面的东西
  bindfunc.prototype = new func();

  return bindfunc;
};
```  
  
## call && apply 
```  
// apply将args用参数传入的数组替代即可
Function.prototype.myCall1 = function(context) {
    // 如果没有传或传的值为空对象 context指向window
    context = context || window
    
    let fn = new Symbol()
    context[fn] = this //给context添加一个方法 指向this
    
    // 处理参数 去除第一个参数this 其它传入fn函数
    let arg = [...arguments].slice(1) 
    context[fn](...arg) //执行fn
    delete context[fn] //删除方法
}
```  
