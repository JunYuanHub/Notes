## 一、基本  
唯一标识。每次调用symbol函数必定得到不重复的标识。不能new。 
1. symbol(name),name为标识。可通过symbol.description获取。  
   name可以是对象，传入时会自动调用其toString方法  
2. symbol不能参加运算，可以转化为布尔值、字符串。  
## 二、symbol作为定义的属性  
1. 用作定义属性
    对象内部symbol定义属性时必须使用方括号包裹  
    ```  
    let obj = {
      [s]: function (arg) { ... }
    };
    
    // 增强写法
    let obj = {
      [s](arg) { ... }
    };
    ```  
    因为点运算后面总是字符串，如果直接用点运算符，会将其解析为字符串  
    ```  
    const mySymbol = Symbol();
    const a = {};
    
    a.mySymbol = 'Hello!';
    a[mySymbol] // undefined
    a['mySymbol'] // "Hello!"
    ```  
2. 
## 应用：  
1. [消除魔术字符串](https://es6.ruanyifeng.com/#docs/symbol)，解耦  