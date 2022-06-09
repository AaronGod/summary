#### js篇

- undefined 数值转换为 NaN， null 转换为0
- 数据类型： 数字 字符 和 对象  ， 是否有无未定义； 另外还有Symbol
  1. 基本：Number  String  Boolean  Null  Undefinded  Symbol
  2. 引用： Object   函数  时间 等

- es5中isNaN() 和 es6中的Number.isNaN() 区别?

  - ~~~js
    isNaN(NaN)//true 
    isNaN(undefined) //true , 
    isNaN(true)// false;   
    
    Number.isNaN(NaN)// true ,
    Number.isNaN(undefined) //false   
    Number.isNaN(true)// false
    ~~~

    

