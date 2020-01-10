# CSS知识点  
### 1. 元素居中  
##### 水平居中  
1. 块状元素，margin的auto方法。  
2. 元素内部文本水平居中，text-align: center。  
3. 内联元素居中，块元素包裹，再设置text-align: center。  
4. flex布局：justify-content:center

##### 垂直居中  
1. flex布局，align-items:center 
2. inline-block元素：vertical-align:middle  

### 2. BFC  
触发条件：
1. 浮动元素，float除none以外的值 (float部分脱离文档流) 
2. 绝对定位元素，position(absolute，fixed) (这俩完全脱离文档流)
3. display，为以下其中之一的值inline-block，table-cells，table-captions； 
4. overflow，除了 visible 以外的值（hidden，auto，scroll）
5. body根元素  

布局规则：  
1. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。  
2. 每个盒子（块盒与行盒）的左边界(含margin)，与BFC容器border的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。  
  
用途：  
1. 阻止外边距折叠（用bfc包裹边距不会重叠）
2. 包含浮动元素（解决高度坍塌）
3. 阻止元素被浮动元素覆盖(第二个元素有部分被浮动元素所覆盖，但是文本信息不会被浮动元素所覆盖，如果想避免元素被覆盖，可触发第二个元素的BFC特性，在第二个元素中加入overflow：hidden)  
### 3. grid布局  
### 4. table-ceil  
### 5. box-sizing
(1) content-box : 以初始定义的width为基准，在此基础上拓展padding+border加入最后width  
(2) border-box : 以初始定义的width为最终width,不因内部border和padding变化  



