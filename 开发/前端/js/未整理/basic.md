### 一、基础数据类型转换  
1. 字符串与数组  
字符串转化数组：str.split('分隔符')  
数组转化为字符串：array.join('分隔符')  
2. Json对象，Json字符串与数组  
字符串转对象：JSON.parse(jsonStr)  
字符串转数组：先转对象再遍历
对象转字符串：JSON.stringify(jsonObj)  
对象转数组：遍历  
数组转字符串：JSON.stringify(arr1)  

