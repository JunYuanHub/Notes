# 2D图形绘制  
fill和stroke，一个为填充一个描边  
## 一、绘制矩形  
1. 新建\<canvas\>元素  
2. js获取该元素  
3. 调用el.getContext获取绘制对象  
3. 设置fillStyle或者strokeStyle，再调用fillRect()或者strokeRect()  
```  
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);  // （起点坐标x,y,x长度，y长度）
```  
清除矩形：clearRect(x,y,wid,hei)  
控制线条：lineWidth线条粗细~ ~lineCap线条末端形状~ ~lineJoin线条相交方式  
## 二、绘制路径  
1. 调用ctx.beginPath()开始绘制  
2. 调用各类绘制函数  
   ```  
   ctx.arc(x,y,r,startAngle,endAngle,counterclockwise) 
   // 以(x,y)为圆心，r为半径，从角度start到角度end。最后一个参数决定是否逆时针。
   
   ctx.arcTo(x1,y1,x2,y2,r)
   // 从上一点绘制一条半径为r的弧线，经过(x1,y1)，到(x2,y2)为止
   
   ctx.moveTo(x,y)
   // 移动绘制起始点
   
   ctx.line(x,y)
   // 绘制一条直线到(x,y)
   
   ctx.rect(x,y,width,height)
   // 聪明如我已经不用解释了
   
   ctx.bezierCurveTo(c1x,c1y,c2x,c2y,x,y)
   //绘制一条曲线，以(c1x,c1y),(c2x,c2y)为控制点，到(x,y)为止
   
   ctx.quadraticCurveTo(cx,cy,x,y)  
   // quadratic平方,cx,cy为控制点。
   ```  
3. 最后调用stroke或者fill函数闭合。  
## 三、绘制文本  
```  
ctx.font = "bold 14px Arial"  
ctx.textAlign = "center"/"start"/"end"
ctx.textBaseline = "middle/top/bottom/hanging" //垂直的基线坐标  
ctx.fillText("文本内容",x,y)
```  
## 四、其他功能  
1. 变换  
```  
改变原点：translate(x,y)
旋转：rotate(angle)
缩放：scale(scaleX,scaleY)
```  
2. 渐变  
```  
let gradient = ctx.createLinearGradient(30,30,200,200) //起止坐标
let gradient = ctx.createRadialGradient(55,55,10,55,55,30) //起止坐标和r
gradient.addColorStop(0,"red")
gradient.addColorStop(1,"green")
console.log(ctx)
ctx.fillStyle=gradient    // 将渐变赋值
ctx.fillRect(30,30,250,250)
```
