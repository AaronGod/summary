1. vuex中 dispatch  和 commit

   dispatch 推送一个action，

    commit 推送一个 mutation

2. string对象扩展一个方法删除前后空格

   ~~~javascript
   String.prototype.deletSpace = function(){
       let str = this
       while(str[0] === ' '){
           str = str.substring(1)
       }
       while(str[str.length -1] === ' '){
           str = str.substring(0,str.length -1)
       }
       return str
   }
   ~~~

   

3. webpack构建流程？

   ​    

4. 权限验证

   - 登录权限验证： 部分页面需要登录才能访问
   - 角色权限验证： 在登录权限的基础上加角色权限的验证，eg：同意页面不同角色展示内容板块不同

![152FA280-5C1D-40D4-BACB-87C12909DBAD-278-0000000B60865A78](assets/152FA280-5C1D-40D4-BACB-87C12909DBAD-278-0000000B60865A78.png)

5. 正则表达式

- /^abc$/ 用于匹配的目标字符必须以a开头 c结尾

  str.match(reg), reg.exex(str)

- 匹配任意字符的写法： [^]* 或者 [\s\S]*

- 使用正则表达式的方法总结：
  1. 正则表达式方法： exec，test；eg: /^张三$/.exec(字符串)
  2. 字符串方法： match, matchAll, search, replace, split;  eg: 字符串.match(正则表达式)

6. vue中的书写易错点总结：
   1. vuex 中 设置命名空间属性为小写 namespaced: true

   2. store.commit('模块名/mutations名'，payload) 而不是 store.emit()

   3. 当使用父级hover控制子元素展开时，如果遇到父级包裹的情况，并且一定要使用到子级的opacity时 会出现放置在子元素也会触发父级hover的bug，所以需要使用`z-index`来控制；

   4. 一些写法

      ~~~vue
      <script>
          setup(){
         	 const {stop} = fn(()=>{
               // 返回的函数 通过解构 可在内部使用
              stop()
            })
          
             const { result, target } = useLoadData()
             return { list: result, target} // 返回重命名数据
          }
      </script>
      ~~~

7. 返回空对象

   ~~~javascript
   () => ({}) // 箭头函数返回空对象写法
   ~~~

8. vue中需要传入函数作为参数，而传入的函数也需要传入参数时-- 处理方法

   ~~~vue
    <script>
   // 注意：useLazyData需要的是API函数，如果遇到要传参的情况，自己写函数再函数中调用API
    const { target, result } = useLazyData(
        () => findBrand(10)
    )
   </script>
   ~~~

   

