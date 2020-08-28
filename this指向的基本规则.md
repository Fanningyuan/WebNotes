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

