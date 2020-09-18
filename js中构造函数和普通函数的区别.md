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

# js中函数定义的几种方式

1. function 函数名（参数列表） {

}

```js
function add(a,b) {
    var sum = a + b;
    alert(sum);
}
add(3,5);
```

2. 匿名函数

也就是不写函数名，将函数当作一个变量

var test = function(参数列表) {

//函数体

}

```js
var add = function(a,b){
    var sum = a + b;
    alert(sum);
}
add(1,3);
```

3. 第三种方式，(使用的很少，一般作为了解)我们需要使用js中的内置对象，Function

var add=new Function（"参数列表" ，"方法体和返回值"）;

```js
var add = new Function('x,y','var sum;sum = x+y;return sum;');
alert(add(1,2));
```

# 构造函数和工厂函数

