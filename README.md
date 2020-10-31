# 问题记录

1. 宏任务与微任务与事件循环(Event Loop)

   ![img](https://img2018.cnblogs.com/blog/1107494/201908/1107494-20190813234853418-2103401274.png)

   | 宏任务                | 微任务           |
   | --------------------- | ---------------- |
   | 同步代码              | process.nextTick |
   | UI rendering          | Promise          |
   | I/O                   | MutationObserver |
   | setTimeout            |                  |
   | setInterval           |                  |
   | requestAnimationFrame |                  |

2. set 和 map的区别

   set 一个类数组集合，不能有重复的，map键值对集合（hash结构）

3. get 和 post的区别

   - Get是不安全的，因为在传输过程，数据被放在请求的URL中；Post的所有操作对用户来说都是不可见的。 
   - Get传送的数据量较小，这主要是因为受URL长度限制；Post传送的数据量较大，一般被默认为不受限制。 
   - Get限制Form表单的数据集的值必须为ASCII字符；而Post支持整个ISO10646字符集。 
   - Get执行效率却比Post方法好。Get是form提交的默认方法。

4. let 和 var 的区别

   - var 是函数作用域，且存在变量提升；let 是块作用域，没有变量提升
   - let 相同作用域不能重复声明
   - let 的暂时性死区（块作用域中let申明之前不允许访问属性，会报ReferenceError）

5. 防抖与节流

6. vue 浏览器兼容性

   引入 babel-polyfill

7. http的请求状态码

8. http的请求方式

9. 请求方式 OPTIONS

   OPTIONS请求即**预检请求**，可用于检测服务器允许的http方法。当发起跨域请求时，由于安全原因，触发一定条件时浏览器会在正式请求之前**自动**先发起OPTIONS请求，即**CORS预检请求**，服务器若接受该跨域请求，浏览器才继续发起正式请求。

10. url从输入到页面呈现过程解析

   输入url -> 查看本地页面缓存（有返回304） -> DNS服务器解析域名 -> 访问IP地址web服务器 -> 建立TCP链接 -> 发送http请求 -> 根据状态码返回数据 -> 浏览器渲染页面

11. 前端性能优化

   + 加载资源优化
     - 静态资源合并和压缩
     - 静态资源缓存
     - 使用CDN
   + 渲染优化
     - css放head中，js放body后
     - 图片懒加载
     - 减少dom操作
   + 事件节流
   + 非核心代码异步加载
   + 浏览器缓存

11. 元素居中

    - line-height 
    - flex布局
    - 定位
    - table
    - margin
    - 定位 + transform

13. 数组去重

    - set去重
    - 遍历（正则、indexOf、include。。。）

14. 深拷贝

15. vue mixin的缺点

    mixin当有相同函数时先调用mixin后调用组件中的函数，容易被滥用

16. 描述一下原型与原型链

   每一个对象都有一个属性prototype指向这个对象的原型对象，一个对象的原型是另一个对象的实例形成一个继承关系，当查找一个属性或者方法时，会沿着对象-》原型往上查找这样一个链式就是原型链

11. 继承方式

    + 原型链继承（通过修改原型对象指向父级对象实例）

      + 引用值会在所有实例间共享。

      + 解决问题方式：盗用构造函数

        ```javascript
        function SuperType() {
            this.colors = ['red','green']
        }
        function SubType() {
            SuperType.call(this)
        } // 产生问题：必须在构造函数中定义方法，因此，函数无法重用；子类无法访问父类原型上的方法
        ```

    + 组合继承（盗用构造函数解决引用值问题 + 原型链继承解决原型方法继承问题）

      存在效率问题，父类构造函数会被调用两次

    + 原型式继承

      Object.create(obj, {key: {options}}) // 第二个参数可以以描述符描述对象（value、enumable、writeable、configable）,存在问题：引用值数据共享

    + 寄生式继承

      类似于寄生构造函数和工厂模式：创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象

      ```javascript
      function createAnother(original) {
          let clone = object(original)
          clone.sayHi = function () {
              console.log(sayHi)
          }
          return clone;
      }
      ```

    + 寄生式组合继承

      相当于就是组合继承然后可以增强属性

      ```javascript
      function SuperType(name) {
          this.name = name;
          this.colors = ['red', 'green']
      }
      
      SuperType.prototype.sayHi = function () {
          console.log('hi')
      }
      
      function SubType(name, age) {
          SuperType.call(this, name)
          this.age = age; //此次
      }
      
      SubType.prototype = new SuperType();
      SubType.prototype.constructor = SuperType;
      ```

    + 类继承

      派生类中构造函数必须调用super

12. 删除一个对象的属性

    - Reflect.deleteProperty(obj, prop)
    - delete obj[prop]

13. 判断一个对象中是否具有一个属性

    | 方法                            | 描述                     | 注意                  |
    | ------------------------------- | ------------------------ | --------------------- |
    | in                              | 'prop' in obj            | 包括原型链上          |
    | obj[prop]                       | 属性调用                 | 无法判断值为undefined |
    | Object.keys(obj).includes(prop) |                          | 只能判断可枚举的属性  |
    | hasOwnProperty                  | obj.hasOwnProperty(prop) | 实例上                |

14. 判断一个对象是否是另一个对象的实例

    - instanceof
    - 原型上调用isPrototypeOf(实例)

15. object类型属性和方法

    | 名称                 | 含义                                     |
    | -------------------- | ---------------------------------------- |
    | constructor          | 构造函数                                 |
    | hasOwnProperty(prop) | 判断当前对象实例上是否存在给定的属性     |
    | isPrototypeOf(obj)   | 判断对象是否为另一个对象的原型           |
    | toLocalString()      | 返回对象的本地环境字符串表示             |
    | toString()           | 返回对象的字符串表示                     |
    | valueOf()            | 返回对象对应的字符串、数值或者布尔值表示 |

    Object.prototype.toString.call() // vue判断类型

16. valueOf的使用场景

    console.log/alert等调用是调用了对象的valueOf

17. let 和 var 的区别

    let是块级作用域 ，var是全局作用域

18. ajax 工作原理、

    XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。

19. 前端缓存

    前端缓存主要是分为HTTP缓存和浏览器缓存。其中HTTP缓存是在HTTP请求传输时用到的缓存，主要在服务器代码上设置；而浏览器缓存则主要由前端开发在前端js上进行设置。

20. 强制缓存

    强制缓存就是向浏览器缓存查找该请求结果，并根据该结果的缓存规则来决定是否使用该缓存结果的过程，主要通过Expires和Cache-Control控制

21. 协商缓存

    协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程，返回304或者200

22. 数组包含哪些方法

    from、isArray、of、concat、copyWithin、entries、every、fill、filter、find、findIndex、flat、flatMap、forEach、includes、indexOf、join、keys、lastIndexOf、map、pop、push、reduce、reduceRight、reverse、shift、slice、some、sort、splice、toLocalString、toSource、toString、unshift、values

23. 对象中包含哪些方法

    | 方法           | 描述                         |
    | -------------- | ---------------------------- |
    | hasOwnProperty | 判断对象是否具有某一个属性   |
    | isPrototypeOf  | 判断一个是否是一个对象的示例 |
    | toLocalString  |                              |
    | toString       |                              |
    | valueOf        | 返回 Array 对象的原始值      |

24. 箭头函数和普通函数的区别

    - 语法不一样
    - 箭头函数是匿名函数，不能作为构造函数，所以不能实例化
    - 箭头函数没有arguments
    - 箭头函数没有原型对象即prototype
    - 箭头函数中没有this指向，即无法绑定this，只能调用上下文中的this
    - 箭头函数call/apply调用时，第一个参数不会修改this指向，因为箭头函数中不能绑定this

## vue

1. vue 数据更新会触发哪些东西
   - computed、渲染页面、watcher
2. vue 路由中history和hash的区别
   - hash 模式下，仅 hash 符号之前的内容会被包含在请求中，不会出现404错误
   - history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致

