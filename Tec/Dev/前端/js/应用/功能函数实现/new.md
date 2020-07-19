```  
function _new(fn, ...arg) {
    const obj = Object.create(fn.prototype);
    const ret = fn.apply(obj, arg);
    return ret instanceof Object ? ret : obj;
}
```  
1. 创建构造函数的 新原型对象  
2. 将构造函数的this指向新对象  
3. 若2返回对象直接return，若2不是对象返回1新建的对象