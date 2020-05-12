## 一、 线程同步  
借助锁，synchronize，性能会下降，加锁解锁也需要耗费资源  
1. synchronize（lockObj）{}  
   ```  
   public void add(int n) {
       synchronized(this) { // 锁住this
           count += n;
       } // 解锁
   }
   ```
2. 用synchronized修饰的方法就是同步方法，它表示整个方法都必须用this实例加锁。  
   ```  
   public synchronized void add(int n) { // 锁住this
       count += n;
   } // 解锁
   ```
1. 引用类型、基本类型（除long和double）赋值为原子性操作，不需要加锁  
## 二、线程安全  
如果一个类被设计允许多线程访问，称"线程安全"的。  
1. java.lang.StringBuffer也是线程安全的。  
2. 还有一些不变类，例如String，Integer，LocalDate，它们的所有成员变量都是final，多线程同时访问时只能读不能写，这些不变类也是线程安全的。  
3. 类似Math这些只提供静态方法，没有成员变量的类，也是线程安全的。 
4. 大部分类，例如ArrayList，都是非线程安全的类，我们不能在多线程中修改它们。但是，如果所有线程都只读取，不写入，那么ArrayList是可以安全地在线程间共享的。 
> 没有特殊说明时，一个类默认是非线程安全的。   
## 三、死锁  
### 可重入锁  
JVM允许同一个线程重复获取同一个锁。每获取一次锁，记录+1，每退出synchronized块，记录-1，减到0的时候，才会真正释放锁。  
### 死锁  
1. 两个线程各自持有不同的锁，然后试图获取对方手里的锁，造成了双方无限等待下去，这就是死锁。  
2. 死锁发生后，没有任何机制能解除死锁，只能强制结束JVM进程  
  
如何避免死锁：线程获取锁的顺序要一致。  
### 线程等待
~~~  
wait和notify用于多线程协调运行：

1. 在synchronized内部可以调用wait()使线程进入等待状态；
2. 必须在已获得的锁对象上调用wait()方法；
3. 在synchronized内部可以调用notify()或notifyAll()唤醒其他等待线程；
4. 必须在已获得的锁对象上调用notify()或notifyAll()方法；
5. 已唤醒的线程还需要重新获得锁后才能继续执行。
~~~  
 