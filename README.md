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

3. 防抖与节流

4. 前端性能优化

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

5. 元素居中

   - line-height 
   - flex布局
   - 定位
   - table
   - margin
   - 定位 + transform

6. vue 数据更新会触发哪些东西

   computed、渲染页面、watcher

7. 数组去重

   - set去重
   - 遍历（正则、indexOf、include。。。）

8. 深拷贝

9. vue mixin的缺点

   mixin当有相同函数时先调用mixin后调用组件中的函数，容易被滥用

10. 描述一下原型与原型链

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

16. let 和 var 的区别

    let是块级作用域 ，var是全局作用域

17. ajax 工作原理、

    XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。

18. 前端缓存

    前端缓存主要是分为HTTP缓存和浏览器缓存。其中HTTP缓存是在HTTP请求传输时用到的缓存，主要在服务器代码上设置；而浏览器缓存则主要由前端开发在前端js上进行设置。

19. 强制缓存

    强制缓存就是向浏览器缓存查找该请求结果，并根据该结果的缓存规则来决定是否使用该缓存结果的过程，主要通过Expires和Cache-Control控制

20. 协商缓存

    协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程，返回304或者200

21. 数组包含哪些方法

    from、isArray、of、concat、copyWithin、entries、every、fill、filter、find、findIndex、flat、flatMap、forEach、includes、indexOf、join、keys、lastIndexOf、map、pop、push、reduce、reduceRight、reverse、shift、slice、some、sort、splice、toLocalString、toSource、toString、unshift、values

