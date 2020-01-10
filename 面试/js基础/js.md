# JS知识点  
### 1. JS数据类型分类和判断  
1. js基本数据类型：number，string，boolean，undefined，null，object  
2. typeof判断结果：number，string，boolean，undefined，function，object (null返回object)  
### 2. 值类型与引用类型  
1. 值类型（基本类型）：字符串（string）、数值（number）、布尔值（boolean）、undefined、null  （这5种基本数据类型是按值访问的，因为可以操作保存在变量中的实际的值）(ECMAScript 2016新增了一种基本数据类型：symbol。
2. 引用类型：对象（Object）、数组（Array）、函数（Function）  

（1）值类型：
1. 占用空间固定，保存在栈中（当一个方法执行时，每个方法都会建立自己的内存栈，在这个方法内定义的变量将会逐个放入这块栈内存里，随着方法的执行结束，这个方法的内存栈也将自然销毁了。因此，所有在方法中定义的变量都是放在栈内存中的；栈中存储的是基础变量以及一些对象的引用变量，基础变量的值是存储在栈中，而引用变量存储在栈中的是指向堆中的数组或者对象的地址，这就是为何修改引用类型总会影响到其他指向这个地址的引用变量。）  
2. 保存与复制的是值本身  
3. 使用typeof检测数据的类型4. 基本类型数据是值类型  

（2）引用类型：  
1. 占用空间不固定，保存在堆中（当我们在程序中创建一个对象时，这个对象将被保存到运行时数据区中，以便反复利用（因为对象的创建成本通常较大），这个运行时数据区就是堆内存。堆内存中的对象不会随方法的结束而销毁，即使方法结束后，这个对象还可能被另一个引用变量所引用（方法的参数传递时很常见），则这个对象依然不会被销毁，只有当一个对象没有任何引用变量引用它时，系统的垃圾回收机制才会在核实的时候回收它。）  
2. 保存与复制的是指向对象的一个指针  
3. 使用instanceof检测数据类型4、使用new()方法构造出的对象是引用型  

### 3. 本地对象、内置对象、宿主对象  
1. 原生/本地对象：  
独立于宿主环境，ECMA提供。在javascript（远景浏览器）、nodejs（node平台）、jscript（ie浏览器）、typescript（微软平台）等等中均有这些对象。Object、Function、Array、String、Boolean、Number、Date、RegExp、Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、URIError、Global  
2. 内置对象：不必明确实例化内置对象，它已被实例化了(类似静态方法)。每个内置对象都是本地对象。Global(函数parseInt等,实际上不存在),Math。常与原生对象同义。  
3. 全局对象：运行环境提供的对象，如浏览器中window，nodejs中Global等  

### 4. 深拷贝与浅拷贝  
拷贝对象引用和拷贝对象
### 5. 原型与原型链（待补充）  
原型=构造函数的prototype=对象的__proto__  
原型的constructor=构造函数  
![](../../开发/前端/js/原型/原型链.png)  
比如，这里的Person.prototype=new Object()，实现继承，此时Person.prototype.__proto__=object(实例).__proto__=Object().prototype)  

当读取实例对象person的属性时，如果找不到，就会查找与该实例对象关联的原型person.__proto__中的属性，如果还查不到，就去找原型的原型Object.prototype，一直找到最顶层为止。  
### 6. call和apply  
1. call 方法第一个参数是要绑定给this的值，后面传入的是一个参数列表。当第一个参数为null、undefined的时候，默认指向window。  
    ```
    var obj = {
        message: 'My name is: '
    }

    function getName(firstName, lastName) {
        console.log(this.message + firstName + ' ' + lastName)
    }
    
    getName.call(obj, 'Dot', 'Dolby')
    ```  
2. apply和call类似，不过传入的参数要以数组形式。  
3. bind。第一个参数是this的指向，从第二个参数开始是接收的参数列表。区别在于bind方法返回值是函数以及bind接收的参数列表的使用。apply和call直接改变函数this指向。  
    ```
    var obj = {
        name: 'Dot'
    }
    
    function printName() {
        console.log(this.name)
    }
    
    var dot = printName.bind(obj)
    console.log(dot) // function () { … }
    dot()  // Dot
    ```
### 7. this指向
### 6. 继承  
### 8. js文件引入位置  
如果JanaScript是外部脚本，不是嵌入脚本，放在head里，会在页面加载之时就被执行，也就是文件要被下载，执行之后才会呈现页面内容；放在body底部，在解析js代码之前，页面的内容就会完全呈现在浏览器中。所以，在body里的js应该是在页面加载之后执行的吧。  
之所以把js放在body之后，是为了预防外部js文件过多时，浏览器呈现页面出现延迟，延迟期间浏览器的窗口一片空白。  
### 9. reducer  
对reduce的理解：  
reduce(callback,initiaValue)会传入两个变量，回调函数(callback)和初始值(initiaValue)。假设函数有4个传入参数，prev和next，index和array。 Prev和next是你必须要了解的。当没有传入初始值时，prev是从数组中第一个元素开始的，next数组是第二个元素。但是当传入初始值（initiaValue）后,第一个prev将是initivalValue，next将是数组中的第一个元素。


