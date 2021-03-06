# ACID
1. 第一个特性 原子性（Atomicity）  
假如我们有个方法中对一个属性进行了N次的更新，但是执行到一半的时候有一个语句有问题出现了异常，这样就可能使得我们上面所说的操作后的点与我们预先的点不同，这不是我们想要的，所以原子性要求你这个方法要么全部执行成功，要么你就别执行。  
  
2. 第二个特性 一致性（Consistency）  
原子性中规定方法中的操作都执行或者都不执行，但并没有说要所有操作一起执行（一起更新那就乱套了，要哪个结果？），所以操作的执行也是有先后顺序的，那我们要是在执行一半时查询了数据库，那我们会得到中间的更新的属性？答案是不会的，一致性规定事务提交前后只存在两个状态，提交前的状态和提交后的状态，绝对不会出现中间的状态。  
3. 第三个特性 隔离性（Isolation）  
事务的隔离性基于原子性和一致性，每一个事务可以并发执行，但是他们互不干扰，但是也有可能不同的事务会操作同一个资源，这个时候为了保持隔离性会用到锁方案。
4. 第四个特性 持久性（Durability）  
当一个事务提交了之后那这个数据库状态就发生了改变，哪怕是提交后刚写入一半数据到数据库中，数据库宕机(死机)了，那当你下次重启的时候数据库也会根据提交日志进行回滚，最终将全部的数据写入。