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

3. 元素居中

   - line-height 
   - flex布局
   - 定位
   - table
   - margin
   - 定位 + transform

4. vue 数据更新会触发哪些东西

   computed、渲染页面、watcher

5. 数组去重

   - set去重
   - 遍历（正则、indexOf、include。。。）

6. 深拷贝

7. vue mixin的缺点

   mixin当有相同函数时先调用mixin后调用组件中的函数，容易被滥用

8. 描述一下原型与原型链

   每一个对象都有一个属性prototype指向这个对象的原型对象，一个对象的原型是另一个对象的实例形成一个继承关系，当查找一个属性或者方法时，会沿着对象-》原型往上查找这样一个链式就是原型链

9. 继承方式

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

     

10. 判断一个对象是否是另一个对象的实例

    - instanceof
    - 原型上调用isPrototypeOf(实例)

11. object类型属性和方法

    | 名称                 | 含义                                     |
    | -------------------- | ---------------------------------------- |
    | constructor          | 构造函数                                 |
    | hasOwnProperty(prop) | 判断当前对象实例上是否存在给定的属性     |
    | isPrototypeOf(obj)   | 判断对象是否为另一个对象的原型           |
    | toLocalString()      | 返回对象的本地环境字符串表示             |
    | toString()           | 返回对象的字符串表示                     |
    | valueOf()            | 返回对象对应的字符串、数值或者布尔值表示 |

    Object.prototype.toString.call() // vue判断类型

12. let 和 var 的区别

    let是块级作用域 ，var是全局作用域

13. ajax 工作原理、

    XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。