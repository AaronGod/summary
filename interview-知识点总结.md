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

- let 和 var的区别？

  1. 变量提升（先上车后买票）
  2. 局部作用域 （红杏出墙）
  3. 声明覆盖 

- 快速居中布局？

  ~~~html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
      body,
      html {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
      }
  
      body {
        display: flex;
  
      }
  
      .con {
        width: 200px;
        height: 200px;
        border: 1px solid #ccc;
        margin: auto;
      }
    </style>
  </head>
  
  <body>
    <div class="con">
      居中对齐
    </div>
  </body>
  
  </html>
  ~~~

- padding与margin？ padding对自己  margin对外

- vw与百分比区别？ 百分比有继承性相对父级，vw相对设备

- 字体变小？ transform:scale(0.8)

- 行内元素和块级元素？ 行类元素宽高由内容决定，设置宽高无效。

- 深拷贝和浅拷贝？

  1. 基本数据类型，值复制不存在深浅拷贝的说法

  2. 深拷贝主要针对对象和数组。浅拷贝只拷贝一层，拷贝后改变时对原来的对象影响

  3. 深拷贝的实现方式？

     ~~~javascript
     // 深拷贝对象和数组
     // 1. JSON方法
     JSON.parse(JSON.stringify(source))
     // 缺点， 关键字会失效 null ,function ,
     
     //2. 常用方法
     function deepClone(source){
         const targetObj = source.constructor === Array? []: {}
         
         for(let keys in source){
             if(source.hasOwnProperty(keys)){
                   if(source[keys] && typeof source[keys] === 'object'){
                   // 	targetObj[keys] = source[keys].constructor === Array? [] : {}
                      targetObj[keys] = deepClone(source[keys])
            	     }else{
                     // source[keys] 为基本数据类型
                     targetObj[keys] = source[keys]
                   }
             }
         }
         return targetObj
     }
     
     ~~~

     

- 数组操作方法中哪些会改变原数组？

  push，pop，shift， unshift， splice， reverse, sort,

- 输入url时发生了哪些？

  www 万维网，服务器； https 传输协议（在http和tcp之间加了一层TSL或者SSL的安全层）；url统一资源定位符，是IP的一个映射；ping是用来测试连接的；

  URL --> DNS域名系统-->拿到IP地址建立连接（TCP三次握手）-->拿数据，渲染页面 --> 四次挥手

  首次访问浏览器会将域名解析的IP存入本地中

  

- 从哪些点做性能优化？

  运算的效率对浏览器影响很小，不算性能优化

  1. 加载：

     ① 减少http请求次数（精灵图，文件合并）

     ② 减小文件体积（资源压缩，图片压缩，代码压缩）

     ③ CDN （第三方库，大文件，大图）

     ④ SSR服务端渲染，预渲染

     ⑤ 懒加载

  2. 性能：

     ① 减少dom操作，避免回流；文档碎片；

  3. 性能优化的几个方面：

     a. 页面加载性能

     b. 动画与操作性能（是否流畅卡顿）transform能脱离文档流减少回流

     c. 内存占用问题，浏览器崩溃

     d. 电量消耗



- 图片懒加载实现方式，原理？

  1. 可视区高度 + 滚动高  > 图片元素offsetTop；src 赋值。
  2.  document.documentElement.clientHeight + document.documentElement.scrollTop || document.body.scrollTop > imgs[i].offsetTop  

  ~~~javascript
    var num = document.getElementsByTagName('img').length;
    var img = document.getElementsByTagName("img");
    var n = 0; //存储图片加载到的位置，避免每次都从第一张图片开始遍历
    
    lazyload(); //页面载入完毕加载可是区域内的图片
    
    window.onscroll = lazyload;
    
    function lazyload() { //监听页面滚动事件
        var seeHeight = document.documentElement.clientHeight; //可见区域高度
        var scrollTop = document.documentElement.scrollTop || document.body.scrollTop; //滚动条距离顶部高度
        for (var i = n; i < num; i++) {
        if (img[i].offsetTop < seeHeight + scrollTop) {
            if (img[i].getAttribute("src") == "default.jpg") {
            img[i].src = img[i].getAttribute("data-src");
            }
            n = i + 1;
        }
        }
    }
  ~~~

  

- vue2中哪些是函数写法，哪些是对象写法？

  ![1655797666261](assets/1655797666261.png)

  https://blog.csdn.net/layxing27/article/details/108986484

  

  