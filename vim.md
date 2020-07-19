https://www.vpser.net/manage/vi.html
~~~  
x         //删除当前字符
nx         //删除从光标开始的n个字符
dd      //删除当前行
ndd   //向下删除当前行在内的n行
u       //撤销上一步操作
U      //撤销对当前行的所有操作

n+        //向下跳n行
n-         //向上跳n行
nG        //跳到行号为n的行
G           //跳至文件的底部

:set  nu     //显示行号
:set nonu    //取消显示行号

yy    //将当前行复制到缓存区，缓存区和cmd+c的存储内容不一样
nyy   //将当前行向下n行复制到缓冲区
yw    //复制从光标开始到词尾的字符
nyw   //复制从光标开始的n个单词
y^      //复制从光标到行首的内容
y$      //复制从光标到行尾的内容
p        //粘贴剪切板里的内容在光标后
P        //粘贴剪切板里的内容在光标前

:s/old/new      //用new替换行中首次出现的old
:s/old/new/g         //用new替换行中所有的old
:n,m s/old/new/g     //用new替换从n到m行里所有的old
:%s/old/new/g      //用new替换当前文件里所有的old
~~~