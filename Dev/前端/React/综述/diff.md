[走你](https://juejin.im/post/5c8e5e4951882545c109ae9c)
比较规则
+ 新的DOM节点不存在{type: 'REMOVE', index}
+ 文本的变化{type: 'TEXT', text: 1}
+ 当节点类型相同时，去看一下属性是否相同，产生一个属性的补丁包{type: 'ATTR', attr: {class: 'list-group'}}
+ 节点类型不相同，直接采用替换模式{type: 'REPLACE', newNode}