# JQuery
一个js函数库
# 1.JQ入口  
+ Js的 onload() 要等到页面中所有资源（包括图片、文件）加载完成才开始执行。  
+ jQuery的入口函数 $(document).ready( ）  只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。  
# 2.层次选择  
DOM与JQ对象转换：dom=JQ[0] / get(0) , JQ=$(Dom)  
（1）#d l选择所有子元素  
（2）#d>l选择子元素  
（3）#d+l相邻兄弟选择  
（4）#d,p,div多选择元素  
（5）even/odd 偶数双数下标  
（6）:eq(x) :gt(x) :lt(x)索引等于、大于、小于x  
（7）:last/:first  
# 3.常用函数
（括号有值为设置，没值为获取）  
（1）.text()获取标签文本文本  
（2）.html()获取标签及其中文本  
（3）.val()设置input中的value  
（4）.css()设置style 不能添加或移除类样式  
（5）.show/hide()显示隐藏  
（6）.chidren()获取所有子元素  
（7）.siblings()获取所有兄弟节点  
 　　　.next() / .prev() => 下/上个兄弟  
　　　.nextAll() / prevAll() / .parent() =>　之后所有 / 之前所有 / 父元素  
（9）.addClass/removeClass/hasClass  
（10）.toggleClass() 切换效果。如果不存在则添加，已设置则删除之。
# 3.链式编程  
概念：对象调用方法如果返回还是原对象，则可以继续调用方法  
  
一般的设置方法都会返回自身，获取方法会获取对应属性（即不可链式）  
但Add/removeClass()括号不管有值没值，还是返回原对象（可链）  
# 4.动画  
1. show / hide( time ,callback( ) ) , time单位毫秒，也可以用字符串fast/normal/slow代替
2. slideUp / slideDown / slideToggle ( time, callback( ) ),划入划出效果  
3. fadeIn / fadeOut / fadeToggle 渐入渐出  
　　fadeTo(时间，结束时透明度) ， 控制opacity  
4. Animate(css键值对， 时间 ，回调)　一般采用链式编程设置多个动画形成动画路径  
# 5.元素操作  
1. 元素创建：$('html内容') 对象.html('html内容')  
2. 元素添加：  
父元素.append(子元素)  　　子元素.appendTo(父元素)  
父元素.prepend(子元素)　　子元素.prependTo(父元素)　　加在第一个子元素上  
父元素.after(元素)　　　　　父元素.before(元素) 　　　加在父元素之后/之前的第一个兄弟元素的位置  
3. 元素移除  
父元素.html("");  
父级元素.empty();　　清空  
父级元素.remove(); 　自杀，自己也被删除  
4. 属性操作  
.prop("属性"，“值”) 　　　　　　　　　　设置或返回被选元素的属性和值  
.attr("属性"， “值”)  　　　　　自定义属性  
.width等  
.offset({位置：值}) 　　　　　设置定位  
.scrollLeft()/.scrollTop() 　 　　设置滚动条水平/垂直偏移量  
5. 事件绑定  
   1. 元素.事件名（处理函数）  
   2. 元素.bind（”事件名“，处理函数）  
   3. 元素.bind({”事件名“:处理函数})  
   4. 父元素.delegate("子元素选择器"， 事件名 ， 处理函数)   
   给所有符合条件的子元素添加事件

  
  
 
  

   