## 一、Set  
1. Set加入值不会发生类型转换。但两个NaN会重复，两个一样的对象不等。  
### 属性  
1. Set.prototype.constructor：构造函数，默认就是Set函数。  
2. Set.prototype.size：返回Set实例的成员总数。  
### 方法  
1. add(value)：添加某个值，返回 Set 结构本身。  
2. delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。  
3. has(value)：返回一个布尔值，表示该值是否为Set的成员。  
4. clear()：清除所有成员，没有返回值。  
5. keys()/values()行为一致。entries方法返回的遍历器，同时包括键名和键值，所以每次输出一个数组，它的两个成员完全相等。  
### 应用  
```  
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
```
### WeakSet  
1. 只能保存对象  
2. 对象弱引用  
3. 不可遍历，没有size，forEach  
4. WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。  

## 二、Map  
对象只接受字符串为键名。Map不限，是一种更完善的Hash实现  
1. 不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作Map构造函数的参数。  
2. 只要两个值严格相等，Map 将其视为一个键，比如0和-0就是一个键，布尔值true和字符串true则是两个不同的键。另外，undefined和null也是两个不同的键。虽然NaN不严格相等于自身，但 Map 将其视为同一个键。  
## 属性与方法  
1. size  
2. set(key,val)  
3. get(key)  
4. has(key)  
5. delete(key)  
6. clear()