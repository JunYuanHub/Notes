## 一. 复用经验  
1. HOC  
2. 抽象公共部分抽离出来，并进行继承
3. 减小副作用。  
   尽量只通过属性输入，避免通过context，更要避免读取全局，调用IO等，即副作用。  
4. 组件的属性添加默认值，且尽量避免复杂的数据结构，使得使用起来更方便。  
5. 提高灵活性，不要给自己设置宽高度，适用性。
6. 做好属性的类型、缺省检测和边界异常情况处理，提高健壮性。
  
## 二. 性能经验  
1. shouldComponentUpdate实现浅比较优化  
2. immutable  

