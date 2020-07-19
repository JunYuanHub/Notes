# 字符串  
- String对象不可变，只可读  
## 构造器  
String，StringBuild,StringBuffer,char数组，byte数组  
## API  
- equals()  
   不仅比较这个字符串的内容还检查另一个被比较的对象是否是String类型  
- contentEquals()  
   只比较两者的内容是否相同，不检查被比较对象的类型。  
- String.format()  
   类似printf,返回字符串  
## Pattern与Matcher 
```  
import java.util.regex.*;
------------------------------------------------
Pattern
...
1. Pattern complie(String regex，int flags)
   创建pattern，pattern不能new创建。
2. String pattern()
   返回正则表达式的字符串形式
3. String[] split(CharSequence input, int limit)
   limit限制分割后的段数
...

-------------------------------------------------
Matcher
...
1. boolean matches()
   只有整个目标字符串完全匹配时才返回真值.
2. boolean find() 
   对字符串进行匹配,匹配到的字符串可以在任何位置
3. boolean lookingAt() 
   匹配到的字符串在最前面才会返回true
...
```

## Scanner类  
~~~  
public static void main(String[] args) throws FileNotFoundException {
        InputStream in = new FileInputStream(new File("C:\\AutoSubmit.java"));
        Scanner s = new Scanner(in);
        while(s.hasNextLine()){
                System.out.println(s.nextLine());
        }
}
delimiter()
  返回此 Scanner 当前正在用于匹配分隔符的 Pattern。
hasNext()
  hasNext()这个方法是如果此扫描器百的输入中有另一个标记，则返回 true。在等待要扫描的输入时，此方法可能阻塞。扫描器度将不执行任何输入。
hasNextLine()
  如果在此扫描器的输入中存在另一行，则返回 true。
next()
  查找并返回来自此扫描器的下一个完整标记。阻塞。
nextLine()
  扫描器获取下一行
~~~