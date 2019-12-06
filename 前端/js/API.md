1. padStart,padEnd  
    X.padStart(n,'str')=>用str填充X左端，直到长度为n  
      
2. find,findIndex  
    + 数组.find(func())，遍历数组每一个元素，根据func筛选出返回为true的第一个值  
    + findIndex，同上，但返回的是索引  
      
3. 生成器函数：普通函数添加*号  
   + 通过new运算符或函数调用的形式调用生成器函数，均会返回一个生成器实例；且不会马上执行函数体的代码；
   + 调用实例的next方法才会执行生成器函数体的代码。  
   + yield后面的表达式将作为迭代器next函数的返回值；迭代器next函数的传入参将作为yield的返回值  
      ```
      [rv] = yield [expression];
      
      a=next(x) => rv=x,a=[expression]
      ```
3. Array.prototype.includes()  
includes()作用,是查找一个值在不在数组里,若是存在则返回true,不存在返回false.  
    ```
    //单参数
    ['a', 'b', 'c'].includes('a')     // true
    ['a', 'b', 'c'].includes('d')     // false 
    //双参数
    ['a', 'b', 'c', 'd'].includes('b')         // true
    ['a', 'b', 'c', 'd'].includes('b', 1)      // true
    ['a', 'b', 'c', 'd'].includes('b', 2)      // false
    ```  
  
4. Object  
    + entries()  
    作用：将一个对象中可枚举属性的键名和键值按照二维数组的方式返回。若对象是数组，则会将数组的下标作为键值返回。  
        ```
        Object.entries({ one: 1, two: 2 })    //[['one', 1], ['two', 2]]
        Object.entries([1, 2])                //[['0', 1], ['1', 2]]  
        ```  
        + 若是键名是Symbol，编译时会被自动忽略  
        + entries()返回的数组顺序和for循环一样，即如果对象的key值是数字，则返回值会对key值进行排序，返回的是排序后的结果  
        + 原理其实就是将对象中的键名和值分别取出来然后推进同一个数组中  
            ```
            //自定义entries()
            var obj = { foo: 'bar', baz: 42 };
            function myEntries(obj) {
                var arr = []
                for (var key of Object.keys(obj)) {
                    arr.push([key, obj[key]])
                }
                return arr
            }
            console.log(myEntries(obj))
            ```  
    + values(),keys()  
    + Object.getOwnPropertyDescriptors()  
    该方法会返回目标对象中所有属性的属性描述符，该属性必须是对象自己定义的，不能是从原型链继承来的。  
6. splice和slice  
slice截取（start,end）
splice（start,end,new）可截取可添加可替换
    
