## 一、synchronize  
synchronized是Java语言层面提供的语法，所以我们不需要考虑异常  
  
配合wait+notify实现线程等待与唤醒

## 二、ReentrantLock(可重入锁)  
[走你！](https://www.liaoxuefeng.com/wiki/1252599548343744/1306581033549858)
可尝试获取锁，但需要错误处理  

可以使用tryLock()尝试获取锁，如果1秒后仍未获取到锁，tryLock()返回false，程序就可以做一些额外处理，而不是无限等待下去。
                   
使用ReentrantLock比直接使用synchronized更安全，线程在tryLock()失败的时候不会导致死锁。  
### 配合condition实现线程等待  
1. await()会释放当前锁，进入等待状态；signal()会唤醒某个等待线程；signalAll()会唤醒所有等待线程；  
2. await还可以传入时间，自己醒来。  
   ```  
   if (condition.await(1, TimeUnit.SECOND)) {
       // 被其他线程唤醒
   } else {
       // 指定时间内没有被其他线程唤醒
   }
   ```
## 三、ReadWriteLock  
使用ReadWriteLock可以提高读取效率：
1. ReadWriteLock只允许一个线程写入；
2. ReadWriteLock允许多个线程在没有写入时同时读取；
3. ReadWriteLock适合读多写少的场景。  
```  
public class Counter {
    private final ReadWriteLock rwlock = new ReentrantReadWriteLock();
    private final Lock rlock = rwlock.readLock();
    private final Lock wlock = rwlock.writeLock();
    private int[] counts = new int[10];

    public void inc(int index) {
        wlock.lock(); // 加写锁
        try {
            counts[index] += 1;
        } finally {
            wlock.unlock(); // 释放写锁
        }
    }

    public int[] get() {
        rlock.lock(); // 加读锁
        try {
            return Arrays.copyOf(counts, counts.length);
        } finally {
            rlock.unlock(); // 释放读锁
        }
    }
}
```  
## 四、stampedLock  
读的过程中也允许获取写锁后写入，但需要判断读的过程中是否有写入，这种读锁是一种乐观锁。  
  
乐观锁的意思就是乐观地估计读的过程中大概率不会有写入，因此被称为乐观锁。反过来，悲观锁则是读的过程中拒绝有写入，也就是写入必须等待。显然乐观锁的并发效率更高，但一旦有小概率的写入导致读取的数据不一致，需要能检测出来，再读一遍就行。
