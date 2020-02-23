# 获取子节点  
1. node.childNodes:返回nodeList，会把换行（用于排版的）和空格也当做子节点  
2. node.children:返回HTMLCollection，不含空格和换行  
3. node.firstChild:获取第一个子元素，包含换行和空格  
4. node.firstElementChild:不含  
5. node.last....同34  
# 获取父节点  
1. node.parentNode：w3c标准  
2. node.parentElement：IE标准  
3. node.offsetParent:获取所有结点  
# 获取兄弟结点  
1. 先父再子：node.parentNode.children\[2\]  
2. node.previousElementSibling || node.previousSibling;  
3. node.nextElementSibling ||  node.nextSibling;

