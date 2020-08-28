# var let和const的区别（暂时性死区问题）

### 暂时性死区

let/const是使用区块作用域；var是使用函数作用域

在let/const声明之前就访问对应的变量与常量，会抛出ReferenceError错误；但在var声明之前就访问对应的变量，则会得到undefined

```javascript
console.log(aVar) //undefined
console.log(aLet) //causes ReferenceError:aLet is not defined
var aVar = 1
let aLet = 2
```

由let/const声明的变量，当它们包含的词法环境(Lexical Environment)被实例化时会被创建，但只有在变量的词法绑定(LexicalBinding)已经被求值运算后，才能够被访问。

`注: 这里指的"变量"是let/const两者，const在ES6定义中是constant variable(固定的变量)的意思。`

当程序的控制流程在新的作用域(module, function或block作用域)进行实例化时，在此作用域中的用let/const声明的变量会先在作用域中被创建出来，但因此时还未进行词法绑定，也就是对声明语句进行求值运算，所以是不能被访问的，访问就会抛出错误。所以在这运行流程一进入作用域创建变量，到变量开始可被访问之间的一段时间，就称之为TDZ(暂时死区)。

用一个简单的例子来说明let声明的变量会在作用域中被提升，就像下面这样:

```javascript
let x = 'outer value'
 
(function() {
  // 这里会产生 TDZ for x
  console.log(x) // TDZ期间访问，产生ReferenceError错误
  let x = 'inner value' // 对x的声明语句，这里结束 TDZ for x
}())
```

在例子中的IIFE里的函数作用域，变量x在作用域中会先被提升到函数区域中的最上面，但这时会产生TDZ，如果在程序流程还未运行到x的声明语句时，算是在TDZ作用的期间，这时候访问x的值，就会抛出`ReferenceError`错误。

以let/const声明的变量或常量，必需是经过对声明的赋值语句的求值后，才算初始化完成，创建时并不算初始化。如果以let声明的变量没有赋给初始值，那么就赋值给它`undefined`值。也就是经过初始化的完成，才代表着TDZ期间的真正结束，这些在作用域中的被声明的变量才能够正常地被访问。

### 三者区别

对于这个问题，我们应该先来了解提升（hoisting）这个概念

```js
console.log(a) // undefined
var a = 1
```

从上述代码中我们可以发现，虽然变量还没有被声明，但是我们却可以使用这个未被声明的变量，这种情况就叫做提升，并且提升的是声明。

对于这种情况，我们可以把代码这样来看

```js
var a
console.log(a) // undefined
a = 1
```

到这里为止，我们已经了解了 var 声明的变量会发生提升的情况，其实不仅变量会提升函数也会被提升。

```js
console.log(a) // ƒ a() {}
function a() {}
var a = 1
```

对于上述代码，打印结果会是 ƒ a() {} ，即使变量声明在函数之后，这也说明了函数会被提升，并且优先于变量提升。

来看 let 和 const 。

```js
var a = 1
let b = 1
const c = 1
console.log(window.b) // undefined
console.log(window. c) // undefined
function test(){
console.log(a)
let a
}
test()
```

首先在全局作用域下使用 let 和 const 声明变量，变量并不会被挂载到 window 上，这一点就和 var 声明有了区别。
再者当我们在声明 a 之前如果使用了 a ，就会出现**报错的情况**

首先报错的原因是因为存在暂时性死区，我们不能在声明前就使用变量，这也是 let 和 const 优于 var 的一点。

其实提升存在的根本原因就是为了解决函数间互相调用的情况

```js
function test1() {
test2()
}
function test2() {
test1()
}
test1()
```

假如不存在提升这个情况，那么就实现不了上述的代码，因为不可能存在 test1 在 test2 前面然后 test2 又在test1 前面。

### 作用域区别

**1.块级作用域**

任何一对花括号 {} 中的语句集都属于一个块，在这之中定义的所有变量在代码块外都是不可见的，我们称之为块级作用域。比如if(){} ,for(){}中的花括号都是块级作用域

**2.函数作用域**

很明显是function(){}的形式，定义在函数中的参数和变量在函数外部是不可见的

而三个变量中 var是忽视块级作用域的，也就是说在块级作用域中用var定义，在外部是可以访问到变量值得，var只有在函数作用域中声明外部才不能访问。而且var声明的变量会被声明提前，被提升到作用域顶部，并被赋值为undefinded

const和let是有块级作用域概念的，也就是说在块级作用域中用const或者let定义，外部无法访问变量！且不可以声明提前

### 1.const

const就是一个定义的常量，在声明的时候就必须要赋值，且这个值不能再被改变，否则会报错。

重点：

1）当声明时不赋值报错

```
const a;
```

![img](https://img-blog.csdnimg.cn/20181214102901220.png)

2） 当试图改变const常量时报错

```
const a=1;
a=2;
```

![img](https://img-blog.csdnimg.cn/20181214103123440.png)

3）在同一作用域中重复定义报错

```
const a=1;
const a=2;
```

 ![img](https://img-blog.csdnimg.cn/20181214103208459.png)

4）不会被声明提前（与var有区别）

```
console.log(a)
const a=2;
```

![img](https://img-blog.csdnimg.cn/20181214103527915.png)

5）可以声明块级作用域的变量，块级作用域外无法访问内部变量！

```
if(true){
	const a=1;
}
console.log(a)
```

![img](https://img-blog.csdnimg.cn/20181214103738762.png)

### 2.let

let和var比较相似，区别就是let不能被声明提前且可以声明块级作用域的变量，还有就是不能被重复声明

1）可以声明时不赋值

```
let a;
a=1;
console.log(a)
```

2）在同一作用域中不可以重复定义

```
let a;
let a=1;
console.log(a)
```

或

```
let a=1;
var a=1;
console.log(a)
```

都报错

![img](https://img-blog.csdnimg.cn/20181214105309107.png)

3）不会被声明提前（与var有区别）

```
console.log(a)
let a=1;
```

![img](https://img-blog.csdnimg.cn/20181214110344435.png) 

4）可以声明块级作用域的变量，块级作用域外无法访问内部变量！

```
if(true){
	let a=1;
}
console.log(a)



for(let a=0;a<10;a++){

}
console.log(a)



let a=1;
if(true){
	let a=2;
}
console.log(a) //1
```

 

![img](https://img-blog.csdnimg.cn/2018121410583688.png)

###  3.var

var我们最熟悉了，就是声明变量用的，但它不能定义块级作用域变量，且会被声明提前

1）可重复定义 

```js
var a=1;
var a=2;
console.log(a)  //2
```

2) 声明时可以不赋值

```js
var a;
console.log(a) //undefined
```

3）js程序在正式执行之前，会将所有var 声明的变量和function声明的函数，预读到所在作用域的顶部，但是对var 声明只是将声明提前，赋值仍然保留在原位置

```js
console.log(a)  //undefined
var a=10; 
console.log(a) //10
```

相当于变成了这样

```js
var a;
console.log(a)  //undefined
a=10; 
console.log(a) //10
```

4）无法定义块级作用域变量，在块级作用域中定义相当于定义了一个全局变量

```js
for(var a=0;a<10;a++){

}
console.log(a)  //10



console.log(a) //undefined
if(true){
	var a=1;
}
console.log(a) //1
```