1. Java确保数组会被初始化（null），而且不能在他的范围外被访问到。付出的代价：每个数组上少量的内存以及运行时的下标检查  
## 一、概念  
1. 一种容器，存储相同类型的数据  
2. 自动给数组中的元素从0开始编号，方便操作这些元素。  
```  
int[] arr = new int[5];
int[] arr = new int[]{3,5,1,7};
int[] arr = {3,5,1,7};
```  
## 二、特点  
1. 数组创建后大小便固定，但效率更高
2. 数组能追踪它内部保存的元素的具体类型，插入的元素类型会在编译期得到检查
3. 数组可以持有原始类型 ( int，float等 )，不过有了自动装箱，容器类看上去也能持有原始类型了  
## 三、注意  
Java不支持类型数组，除非是采用通配符的方式：  
1. 如果允许的话，由于JVM的擦除机制，运行时JVM并不知道泛型信息，因此可能允许程序赋值不同的类型信息，但在取出时却要做一次类型转换，此时出现运行时报错  
2. 对于这样的情况，可以在编译期提示代码有类型安全问题，比没有任何提示要强很多。  
## 四、常用API  
0. System.arraycopy > clone > Arrays.copyOf > for循环  
   ```  
   void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)
        src - 源数组
        srcPos - 源数组中的起始位置
        dest - 目标数组(该方法会改变该数组)
        destPos - 目标数据中的起始位置
        length - 要复制的数组元素的数量
   
   Arrays.copyof()
   Arrays.copyOfRange(type[], from, to)
   ```
1. boolean Arrays.equals()  
   boolean Arrays.deepEquals()  
   比较数组元素(引用/地址比较)是否相同,后者用于多维  
2. String Arrays.toString()  
   String deepToString() 将二维数组拼接为字符串形式    
4. void fill(type[] a, type v); 将数组中的所有元素值都设置为v  
5. binarySearch( type[] a, type v)  
   binarySearch(type[] a, int start, int end, type v)  
    二分查找，查找成功返回下标，否则返回-1；
