1. 普通函数this指向最后调用它的最后调用者  
2. 箭头函数指向外层最近的非箭头函数的函数所在作用域
3. 优先级：取属性. > new () > 调用函数 > new 
  
1. ES5中，顶层对象的属性等价于全局变量。  
   ES6中，var、function声明的全局变量，依然是顶层对象的属性(对浏览器；node遵循下面的)；let、const、class声明的全局变量不属于顶层对象的属性，也就是说ES6开始，全局变量和顶层对象的属性开始分离、脱钩。let const声明的全局变量不属于顶层对象的属性，
    ```  
    let len = 10;
    function fn() {
    	console.info(this.len)
    }
    fn();
    let Person = {
    	len: 5,
    	say: function() {
    		fn();
    		arguments[0]();   // 以arguments形式调用，arguments对象上没有
    	}
    }
    Person.say(fn);
    
    ///////////////////
    undefined
    undefined
    undefined
   ```