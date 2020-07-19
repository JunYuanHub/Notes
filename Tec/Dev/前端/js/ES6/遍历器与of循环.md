enumerable => for in  
iterator => for of  
## 作用 
1. 为各种数据结构，提供一个统一的、简便的访问接口；  
2. 使得数据结构的成员能够按某种次序排列；  
3. ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供for...of消费。  
## 区别  
迭代enumerable是针对for in循环，Object.keys的可列举性。  
遍历是调用生成器函数接口，是个函数的返回结果（可以瞎返回）
## 默认接口  
概述：可迭代对象的Symbol.iterator，即obj\[Symbol.iterator\]是一个返回迭代器的函数，调用它获取迭代器，同时迭代器会具有next方法、  

数据结构只要具有Symbol.iterator属性，就可以认为是“可遍历的”  
  
Symbol.iterator属性本身是一个生成器函数，就是当前数据结构默认的遍历器生成函数。执行这个函数，就会返回一个遍历器。调用时放在方括号里。  
```  
// 直接使用预定义好的
var someString = "hi";
var iterator = someString[Symbol.iterator]();

iterator.next()  // { value: "h", done: false }
iterator.next()  // { value: "i", done: false }
iterator.next()  // { value: undefined, done: true }
  
const obj = {
  [Symbol.iterator] : function () {
    return {
      next: function () {
        return {
          value: 1,
          done: true
        };
      }
    };
  }
};

```  
原生具备 Iterator 接口的数据结构如下(注意object没有)。  
1. Array
2. Map
3. Set
4. String
5. TypedArray
6. 函数的 arguments 对象
7. NodeList 对象  
## 调用接口的场合  
以下情况会自动调用iterator接口  
1. 解构赋值  
   ```  
   let set = new Set().add('a').add('b').add('c');
   
   let [x,y] = set;
   // x='a'; y='b'
   ```
2. !!! 扩展运算符  
   只要某个数据结构部署了 Iterator 接口，就可以对它使用扩展运算符，将其转为数组。\[...arr\]  
3. yield *  
   yield*后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口。  
   ```  
   let generator = function* () {
     yield 1;
     yield* [2,3,4];
     yield 5;
   };
   
   var iterator = generator();
   
   iterator.next() // { value: 1, done: false }
   iterator.next() // { value: 2, done: false }
   iterator.next() // { value: 3, done: false }
   iterator.next() // { value: 4, done: false }
   iterator.next() // { value: 5, done: false }
   iterator.next() // { value: undefined, done: true }  
   ```  
4. 其他场合  
   由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用了遍历器接口。  
   如：Array.from/promise.all等  
## 三、for of  
1. 数组的遍历器接口只返回具有数字索引的属性。  
    ```  
    let arr = [3, 5, 7];
    arr.foo = 'hello';
    
    for (let i in arr) {
      console.log(i); // "0", "1", "2", "foo"
    }
    
    for (let i of arr) {
      console.log(i); //  "3", "5", "7"
    }
    ```  
2. Set和Map和类数组。其中map每次遍历结果为数组\[key,val\]  
### 便利方式比较  
1. for循环；麻烦  
2. forEach，无法中断  
3. for in 为遍历对象而生；遍历所有enermuralble;只能遍历键名，且数组的键名是字符串；会遍历其他属性名。