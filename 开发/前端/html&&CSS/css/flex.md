（1）flex1的计算规则  
第一步：先明确：flex 是 flex-grow | flex-shrink | flex-basis 的缩写。  
1、默认情况：flex：0 1 auto;

2、flex取值为none 0 0 auto;

3、flex取值auto: 1 1 auto

4、flex取值为一个非负的值时：则该数值是flex-grow的值。flex-shrink: 1， flex-basis: 0；即为： num 1 0%;

5、flex取值是一个长度或百分比 60%，200px：则该数值是flex-basis的值。取值（ 1 1 60%）（ 1 1 200px）；

6、flex取值是2个非负数字（2，3），则分别视为flex-grow和flex-shrink的值。flex-basis取值0%。（2 3 0%）；

7、flex 取值是1个非负数字一个百分比(长度)(2 200px)，则flex-grow 和 flex-shrink的值是非负数字的值。(2 2 200px)