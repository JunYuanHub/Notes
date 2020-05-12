## 一、概念  
状态机，可以依次遍历 Generator 函数内部的每一个状态。  
1. function关键字与函数名之间有一个星号；  
2. 函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）。  
## 二、使用  
1. 调用generator函数返回生成器（本身并不会执行函数内部代码）  
2. 调用next方法，运行至下一个yield（yield后面的代码会运行），返回{value: val ,done:false/true},value为yield后的返回值。如此循环  
3. 调用next时传入的参数会作为上一次yield后面表达式的结果。  
示例：  
```  
let a = function* () {
    console.log(1)
    let b = yield 100
    console.log(b)
    return console.log(3)
}
a=a()       // a {<suspended>}
a.next()    // 1 2 {value: undefined, done: false}
a.next()   // 1 3 {value: undefined, done: true}
```  
### (1). generator与iterator  
1. 由于 Generator 函数就是遍历器生成函数，因此可以把 Generator 赋值给对象的Symbol.iterator属性，从而使得该对象具有 Iterator 接口。  
2. 生成器函数返回的迭代器本身具有iterator接口。  
   即Generator 函数执行后，返回一个遍历器对象。该对象本身也具有Symbol.iterator属性，执行后返回自身。  
### (2). 错误处理throw方法  
1. 注意区分gen.throw与全局throw。两者无关，互不影响。
2. gen.throw方法抛出的错误要被内部捕获，前提是必须至少执行过一次next方法(执行next相当于启动内部程序)。  
3. gen.throw会附带执行一次next方法，相当于抛错同时不会影响本次生成器执行。  
4. Generator 执行过程中抛出错误，且没被内部捕获，就不会再执行下去了。如果此后还调用next方法，将返回一个value属性等于undefined、done属性等于true的对象，即 JavaScript 引擎认为这个 Generator 已经运行结束了。  
## (3). return方法  
1. 调用return后终止函数遍历，value为传入参数||undefined，done：true  
2. 如果有try finally语句，则会执行完finally语句后退出函数。  
### (4). yield*  
相当for of循环  
嵌套生成器时使用。yield* gen()相当于进入生成器函数gen;否则yield gen()返回生成器  
```  
function* bar() {
  yield 'x';
  yield* foo();
  yield 'y';
}

// 等同于
function* bar() {
  yield 'x';
  for (let v of foo()) {
    yield v;
  }
  yield 'y';
}
```  
### (5). 生成器实例  
Generator 函数总是返回一个遍历器，ES6 规定这个遍历器是 Generator 函数的实例,也继承了 Generator 函数的prototype对象上的方法。  
但不能当构造函数使用new。若要使用new创建实例，可借助原型  
```  
function* gen() {
  this.a = 1;
  yield this.b = 2;
  yield this.c = 3;
}

function F() {
  return gen.call(gen.prototype);
}

var f = new F();

f.next();  // Object {value: 2, done: false}
f.next();  // Object {value: 3, done: false}
f.next();  // Object {value: undefined, done: true}

f.a // 1
f.b // 2
f.c // 3
```  
### (6). 内部协程与上下文  
1. 协程  
   多(单)线程下，多个线程(函数)并行执行，但只有一个线程(函数)处于运行状态。其他线程（或函数）都处于暂停态（suspended），互相之间可以切换执行权，即协程。  
   在内存中，子例程只使用一个栈（stack）(类似下文的上下文堆)，而协程是同时存在多个栈，但只有一个栈是在运行状态，也就是说，协程是以多占用内存为代价，实现多任务的并行。

   Generator 函数是 ES6 对协程的实现，但属于不完全实现。Generator 函数被称为“半协程”（semi-coroutine），意思是只有 Generator 函数的调用者，才能将程序的执行权还给 Generator 函数(通过yield)。如果是完全执行的协程，任何函数都可以让暂停的协程继续执行。  
2. 上下文  
   Js运行时，会产生一个全局的上下文环境（context，又称运行环境），包含了当前所有的变量和对象。然后，执行函数（或块级代码）的时候，又会在当前上下文环境的上层，产生一个函数运行的上下文，变成当前（active）的上下文，由此形成一个上下文环境的堆栈（context stack）。后进先出。知道代码全部执行完清空堆栈为止。  
     
   Generator 函数不是这样，它执行产生的上下文环境，一旦遇到yield命令，就会暂时退出堆栈，但是并不消失，里面的所有变量和对象会冻结在当前状态。等到对它执行next命令时，这个上下文环境又会重新加入调用栈，冻结的变量和对象恢复执行。
## 三、注意事项  
1. 普通函数当中不能使用yield，嵌套函数也不行（如外生成器，里面普通函数，普通函数里不能使用yield）  
2. yield表达式如果用在另一个表达式之中，必须放在圆括号里面 
   ```
   function* demo() {
     console.log('Hello' + yield); // SyntaxError
     console.log('Hello' + yield 123); // SyntaxError
   
     console.log('Hello' + (yield)); // OK
     console.log('Hello' + (yield 123)); // OK
   }  
   ```  
3. yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号。  
   ```  
   function* demo() {
     foo(yield 'a', yield 'b'); // OK
     let input = yield; // OK
   }
   ```  
4. 由于 Generator 函数就是遍历器生成函数，因此可以把 Generator 赋值给对象的Symbol.iterator属性，从而使得该对象具有 Iterator 接口。  
  
## 应用  
1. 二叉树创建与遍历  
```  
// 下面是二叉树的构造函数，
// 三个参数分别是左树、当前节点和右树
function Tree(left, label, right) {
  this.left = left;
  this.label = label;
  this.right = right;
}

// 下面是中序（inorder）遍历函数。
// 由于返回的是一个遍历器，所以要用generator函数。
// 函数体内采用递归算法，所以左树和右树要用yield*遍历
function* inorder(t) {
  if (t) {
    yield* inorder(t.left);
    yield t.label;
    yield* inorder(t.right);
  }
}

// 下面生成二叉树
function make(array) {
  // 判断是否为叶节点
  if (array.length == 1) return new Tree(null, array[0], null);
  return new Tree(make(array[0]), array[1], make(array[2]));
}
let tree = make([[['a'], 'b', ['c']], 'd', [['e'], 'f', ['g']]]);

// 遍历二叉树
var result = [];
for (let node of inorder(tree)) {
  result.push(node);
}

result
```
