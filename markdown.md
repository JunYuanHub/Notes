#Markdown学习笔记 (JetBrains 系列编辑器)

######Time：2019-10-1　　　Writer:均远
### [jetbrain快捷键](https://www.cnblogs.com/zhuchenglin/p/10058494.html)  
1. 选中多个相同字符串：control + g;
2. 全选：control + command + g  
1. Ctrl + Alt + Shift + T:重构这段代码（显示所有可用的重构），比如if else if 这种语句转switch语句  
2. ctrl + Alt + 左右：回到历史编辑位置  
3. ctrl + alt + l : 整理代码
##Part.1 标题与段落
* 标题  
使用 ‘#’ ，1-6个 # 分别代表从大到小的标题样式；或者在段落下一行加上‘====’  
* 段落
    + 换行：‘\<br>’ 或者 末尾处两个`空格`+`回车`
    + 字体：  
    \_hello_　　　=>　斜体字 _hello_  
    \_\_hello__　　=>　粗体字 __hello__  
    \_\_\_hello___　=>　粗斜体 ___hello___  
    \~~hello~\~　　=>　删除线  ~~hello~~  
* 引用  
段落开头使用` > 符号` ，然后后面紧跟一个`空格`符号。  
  > 这是引用的段落
* 代码区域  
用\```包裹代码块，如：  
\```javascript
$(document)
\```
  ```javascript
  $(document).ready(function () {
    alert('RUNOOB');  //一起来复习下JQuery吧
  });
  ```
##Part.2 列表  
列表十分好用，它会自动帮你缩进对齐列表头，使得排版很美观
* 无序列表  
任选一个`+/*/-`+`空格`+`内容`即可，如：\* 列表（空格不能少！）  
* 有序列表  
`数字`+` . `+`内容 `
* 嵌套列表  
上一级与下一级列表之间敲三个空格即可  
##Part.3 拓展  
* 链接  
\[链接名称](链接地址) 或者 <链接地址>  
前一种方法可以指定链接名称，后一种默认链接名称为链接地址本身
* 图片  
  * 指定宽高：  
  \<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">  
  * 不指定宽高：  
  !\[alt 属性文本](图片地址 "可选标题")  
  ![alt 属性文本](http://static.runoob.com/images/runoob-logo.png )  
* 表格  
----用于分割表头表尾，| 用于分割单元格  
|  表头   |　表头  |  
|  ----　| 　----　|  
| 单元格  | 单元格 |  
| 单元格  | 单元格 |  
  
  
  


