## Promise基础  
容器，三种状态，不可逆。  
1. 状态：pending-resolve（fulfilled）-reject  
2. 如果不调用catch，错误内部静默处理。promise执行出错会直接进入reject  
3. then会将  
## async && await  
async是generator的语法糖.就是将 Generator 函数和自动执行器，包装在一个函数里。  
```  
const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};

const asyncReadFile = async function () {
  const f1 = await readFile('/etc/fstab');
  const f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```  
### async
1. async函数返回一个 Promise 对象，可以使用then方法添加回调函数。当函数执行的时候，一旦遇到await就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。  
2. async函数返回的 Promise 对象，必须等到内部所有await命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到return语句或者抛出错误。也就是说，只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数。  
### await  
1. await命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）。  
2. 另一种情况是，await命令后面是一个thenable对象（即定义then方法的对象），那么await会将其等同于 Promise 对象。  
  
### 应用与注意事项  
1. 实现sleep函数(await+setTimeout)  
   ```  
   function sleep(interval) {
       return new Promise(resolve => {
           setTimeout(resolve, interval);
       })
   }
   
   // 用法
   async function one2FiveInAsync() {
       for(let i = 1; i <= 5; i++) {
           console.log(i);
           await sleep(1000);
       }
   }
   ```  
2. 部署一系列动画(借鉴调用方式)  
   ```  
   // Promise版本
   function chainAnimationsPromise(elem, animations) {
   
     // 变量ret用来保存上一个动画的返回值
     let ret = null;
   
     // 新建一个空的Promise
     let p = Promise.resolve();
   
     // 使用then方法，添加所有动画
     for(let anim of animations) {
       p = p.then(function(val) {
         ret = val;
         return anim(elem);
       });
     }
   
     // 返回一个部署了错误捕捉机制的Promise
     return p.catch(function(e) {
       /* 忽略错误，继续执行 */
     }).then(function() {
       return ret;
     });
   
   }
   
   // generator版本，需要提供自执行函数 
   function chainAnimationsGenerator(elem, animations) {
   
     return spawn(function*() {
       let ret = null;
       try {
         for(let anim of animations) {
           ret = yield anim(elem);
         }
       } catch(e) {
         /* 忽略错误，继续执行 */
       }
       return ret;
     });
   
   }
   
   // async版本，非常语义化
   async function chainAnimationsAsync(elem, animations) {
     let ret = null;
     try {
       for(let anim of animations) {
         ret = await anim(elem);
       }
     } catch(e) {
       /* 忽略错误，继续执行 */
     }
     return ret;
   }
   ```
2. await命令后面的Promise对象，运行结果可能是rejected，所以最好把await命令放在try...catch代码块中。  
3. 多个await命令后面的异步操作，如果不存在继发关系，最好让它们同时触发。（即使用promise.all）  
4. await命令只能用在async函数之中，如果用在普通函数，就会报错。  
