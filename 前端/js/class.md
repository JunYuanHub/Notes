# 面向对象  
+ 传统类面向对象：
```
//利用构造函数仿类面向对象
function Animal(name){
 this.name=name
}
```  
+ class:  
```
class Person {
    static info = {name:XXX}
}
```  
+ 静态属性和实例属性：  
    + static可以通过类名直接调用，存储于类的内存上  
    + 实例属性只能通过实例调用，存储于new的实例上