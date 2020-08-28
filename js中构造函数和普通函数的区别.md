# js中构造函数和普通函数的区别

1. 构造函数也是一个普通的函数，创建方式和普通函数一样，但是构造函数习惯上首字母大写。

2. 构造函数和普通函数的区别在于：调用方式不一样。作用也不一样（构造函数用来新建实例对象）

3. 调用方式不一样

   普通函数的调用方式：直接调用 person()；

   构造函数的调用方式：需要使用new关键字来调用new Person()；

4. 构造函数的函数名和类名相同，Person()这个构造函数，Person是函数名也是这个对象的类名

5. 构造函数内部用this来构造属性和方法

   ```javascript
   function Person(name,job,age){
       this.name = name;
       this.job = job;
       this.age = age;
       this.sayHi = function(){
           console.log('Hi')
       }
   }
   ```