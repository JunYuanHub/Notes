## （1）flex1的计算规则  
flex 是 flex-grow | flex-shrink | flex-basis 的缩写。  
1、默认情况：flex：0 1 auto;  
2、flex取值为none 0 0 auto;  
3、flex取值auto: 1 1 auto  
4、flex取值为一个非负的值时：则该数值是flex-grow的值。默认flex-shrink: 1， flex-basis: 0；即为： num 1 0%;  
5、flex取值是一个长度或百分比 60%，200px：则该数值是flex-basis的值。默认1，1取值（ 1 1 60%）（ 1 1 200px）；  
6、flex取值是2个非负数字（2，3），则分别视为flex-grow和flex-shrink的值。flex-basis取值0%。（2 3 0%）；  
7、flex 取值是1个非负数字一个百分比(长度)(2 200px)，则flex-grow 和 flex-shrink的值是非负数字的值。(2 2 200px)  
> 在左边固定，右边自适应布局中flex:1  
> 对于左边，默认是可缩小，当右边的basis为0，即不占用任何空间但可以伸缩时，会自动放大到填满，如果是100%，即设置初始状态为右边占满，这样则会导致空间不足，使得左边压缩。
## （2）各个属性  
1. flex-direction:主轴。  
    ```  
    flex-direction: row（默认） | row-reverse | column | column-reverse;  
    ```
2. flex-wrap：一行放不下了是否换行。  
    ```  
    flex-wrap: nowrap(默认) | wrap | wrap-reverse(换行，新行在上面);
    ```  
3. （1和2的简写）：flex-flow  
4. justify-content：在主轴上的对齐方式（水平方向）  
   ```  
   justify-content: flex-start(默认) | flex-end | center | space-between | space-around;
   ```  
5. align-content:宏观整体在垂直方向上的布局（整体垂直方向，可用于垂直居中），只有一行时不生效
   ```  
   align-content: stretch(默认，轴线加起来占满) |  
                  flex-start | flex-end | center | space-between | space-around 
   ```  
6. align-items:每个主轴线在交叉轴上的对齐方式（局部垂直方向）  
   ```  
   align-items: stretch(默认，子元素没设置高度时会占满) | flex-start | flex-end | center | baseline | 
   ```  
## （3）元素属性  
~~~  
顺序：数值越小越靠前，默认为0
order: <number>; 

放大比例：默认为0，如果有剩余空间也不放大，值为1则放大，2是1的双倍大小，以此类推
flex-grow: <number>; 

缩小比例：默认为1，如果空间不足则会缩小，值为0不缩小
flex-shrink: <number>;

项目自身大小：默认auto，为原来的大小，会根据此计算是否有剩余，即会影响其他元素缩放，可设置固定值 50px/50%
flex-basis: <length> | auto;
   > 在左边固定，右边自适应布局中flex:1  
   > 对于左边，默认是可缩小，当右边的basis为0，即不占用任何空间但可以伸缩时，会自动放大到填满，如果是100%，即设置初始状态为右边占满，这样则会导致空间不足，使得左边压缩。 
快捷值：
默认值：(0 1 auto)【父控件有剩余空间也不放大，父控件空间不足按1缩小，保持本身的空间大小】
auto (1 1 auto)
none (0 0 auto)
  1  (1 1  0% )  【父控件有剩余空间占1份放大，父控件空间不足按1缩小，自身的空间大小是0%】
  

项目自身对齐：继承父元素（默认） | 起点对齐 | 终点对齐 | 居中对齐 | 基线对齐 | 拉伸对齐
align-self: auto | flex-start | flex-end | center | baseline | stretch;

~~~