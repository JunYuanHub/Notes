## API  
1. display：grid  
2. grid-template-rows/columns  
3. fr  
4. grid-row/column => grid-row-start/end  
5. grid-template-areas:(“画图”) <=> grid-area  
6. repeat(9, minmax(250px/auto-fill/auto-fit, 1fr))  
    ```  
    1. auto-fill 倾向于容纳更多的列，所以如果在满足宽度限制的前提下还有空间能容纳新列，那么它会暗中创建一些列来填充当前行。即使创建出来的列没有任何内容，但实际上还是占据了行的空间。 
    
    2. auto-fit 倾向于使用最少列数占满当前行空间，浏览器先是和 auto-fill 一样，暗中创建一些列来填充多出来的行空间，然后坍缩（collapse）这些列以便腾出空间让其余列扩张。
    ```  
7. grid-gap