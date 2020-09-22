# this指向的基本规则

谁调用它，this就指向谁。这是目前判断this指向用的最多的方法，但是仅通过这句话仅能判断最简单的一些this指向，在很多情况下并不能准确的判断this的指向，因此可以用四种规则来判断this指向。

this绑定规则一共分为四种：默认绑定，隐式绑定，显示绑定，new绑定。并且四种规则的优先级是： new绑定>显示绑定>隐式绑定>默认绑定

### new绑定

```js
function One(age){
	this.age = age
}
let two = new One('18')
console.log(two.age)// 18
```

ps:构造函数返回的如果是function 或者 object ,this指向的就是返回的对象

### 显示绑定

```js
var age = 16;
function one(){
	console.log(this.age)
}
const MrWwwu = {
	age:18
}
one.call(MrWwwu)
one.apply(MrWwwu)
one.bind(MrWwwu)()
//这里切记bind绑定不会立即执行 因此如果打印one.bind(MrWwwu) 打印出来的是个function
```

call apply bind 是显示绑定的三种方法 this指向的就是绑定的对象

##### 硬绑定

```js
function foo(){
	console.log(this.a)
}
var obj = {
	a:2
};
var bar = function(){
	foo.call(obj)
}
bar()//2
setTimeout(bar ,100)//2
//硬绑定后bar无论怎么调用，都不会影响foo函数的this绑定
bar.call(window)//2
```

硬绑定的典型应用是如下的包裹函数：

```js
function foo(something){
	console.log(this.a,something);
	return this.a + something;
}
var obj = {
	a:2
}
var bar = function(){
	return foo.apply(obj,arguments);//将obj对象硬编码进去
}
var b = bar(3)//2 3
conosle.log(b)//5
```

即将内部函数用apply硬绑定到某个对象，无论怎么调用这个包裹函数，都不会影响内部函数的this。

### 隐式绑定

当函数引用有上下文对象时，隐式绑定规则会把函数调用中的this绑定到这个上下文对象

对象属性引用链中只有最后一层在调用位置中起作用

```js
function one(){
	console.log(this.age)
}
let MrWwwu = {
	age:18,
	one
}
let age = 20;
Mrwwu.one()//18
```

```js
function foo(){
	console.log(this.a)
}
var obj2 = {
	a:42,
	foo:foo
}
var obj1 = {
	a:2,
	obj2:obj2
}
obj1.obj2.foo();//42
```

##### 隐式丢失

```js
function foo(){
	console.log(this.a)
}
var obj = {
	a:2,
	foo:foo
}
var bar = obj.foo;//这里bar将引用foo函数本身，所以不带有函数对象的上下文
var a = 'oops,global'//a是全局对象的属性
bar();//'opps,global'
```

### 默认绑定

```js
function one(){
	console.log(this.age)
}
var age = 18;
one()//18  (非严格模式下)
```

### this指向实例

#### 全局环境中

在全局执行环境中，this都是指向全局对象。在浏览器中，window对象即是全局对象；

```js
console.log(this)// window
var a = 1;
console.log(window.a); // 1
this.b = 3;
console.log(b); // 3
console.log(window.b); // 3
```

#### 在函数环境中

在函数内容中，this指向取决于函数调用的方式

```js
function f() {
	'use strict';
	console.log(this);
}
f(); // window; 使用严格模式时，输出undefined
```

##### this指向如何发生变化

1. 一般想到的是call和apply方法：将一个对象作为call或者apply的第一个参数，this将会被绑定到这个参数对象上

```js
var obj = {
	parent : '男'
};
var parent = '28';
function child(obj) {
    console.log(this.parent)
}

child(); // 28
child.call(obj); // 男
child.apply(obj); //男
```

2. bind方法，调用f.bind(someObject)会创建一个与f具有相同函数体和作用域的函数，但是在这个新函数中，this将会永久地被绑定到了bind的第一个参数，不管函数是怎样调用的。

```js
function f() {
    return this.a;
}
var g = f.bind({a:'js'});
console.log(g()); // js

var h = g.bind({a:'html'}); // this已经被绑定this的第一个参数，不会重复绑定，输出的值还是js
console.log(h()); // js

var o = {
    a:css,
    f:f,
    g:g,
    h:h
}
console.log(o.f(), o.g(), o.h());// css js js
```

3. 作为对象的方法调用时

当函数作为对象的方法被调用时，this指向调用的该函数的对象：

```js
var obj = {
  a: 37,
  fn: function() {
    return this.a;
  }
};
console.log(obj.fn());  // 37
```

请注意，这样的行为，根本不受函数定义方式或位置的影响。在前面的例子中，我们在定义对象`obj`的同时，将函数内联定义为成员 `fn`。但是，我们也可以先定义函数，然后再将其附属到`obj.fn`。这样做会导致相同的行为：

```js
var obj = {a: 47};
function independent() {
  return this.a;
}
obj.fn = independent;
console.log(obj);  //{a:47,fn:f}
console.log(obj.fn()); //  47
```

对于在对象原型链上某处定义的方法，`this`指向的是调用这个方法的对象，就像该方法在对象上一样

```js
var o = {
  f: function() { 
    return this.a + this.b; 
  }
};
var p = Object.create(o);
p.a = 1;
p.b = 4;
console.log(p.f()); // 5
```

在这个例子中，对象`p`没有属于它自己的`f`属性，它的f属性继承自它的原型。虽然在对 `f` 的查找过程中，最终是在 `o` 中找到 `f` 属性的，这并没有关系；查找过程首先从 `p.f` 的引用开始，所以函数中的 `this` 指向`p`。也就是说，因为`f`是作为`p`的方法调用的，所以它的`this`指向了`p`。

4. 作为构造函数

当一个函数用作构造函数时（使用new关键字），它的`this`被绑定到正在构造的新对象。

虽然构造器返回的默认值是`this`所指的那个对象，但它仍可以手动返回其他的对象（如果返回值不是一个对象，则返回`this`对象）。

```js
function C(){
  this.a = 37;
}

var o = new C();
console.log(o.a); //  37
function C2(){
  this.a = 37;
  return {a:38};
}
o = new C2();
console.log(o.a); //  38，手动设置了返回对象

```

## globalThis

全局属性 `globalThis` 包含全局的 `this` 值，类似于全局对象（global object）。

在以前，从不同的 JavaScript 环境中获取全局对象需要不同的语句。在 Web 中，可以通过 `window`、`self` 或者 `frames` 取到全局对象，但是在 [Web Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Worker) 中，只有 `self` 可以。在 Node.js 中，它们都无法获取，必须使用 `global`。

在松散模式下，可以在函数中返回 `this` 来获取全局对象，但是在严格模式和模块环境下，`this` 会返回 `undefined`。

`globalThis` 提供了一个标准的方式来获取不同环境下的全局 `this` 对象（也就是全局对象自身）。不像 `window` 或者 `self` 这些属性，它确保可以在有无窗口的各种环境下正常工作。所以，你可以安心的使用 `globalThis`，不必担心它的运行环境。为便于记忆，你只需要记住，全局作用域中的 `this` 就是 `globalThis`。