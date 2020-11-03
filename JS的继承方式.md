# JS的继承方式

继承需要一个父类，但是在js中实际上没有类的概念，在es6中class虽然很像类，但实际只是es5上的语法糖而已。

```javascript
function People(name){
	//属性
	this.name = name || Annie;
	//实例方法
	this.sleep = function(){
		console.log(this.name + '正在睡觉');
	}
}
//原型方法
People.prototype.eat = function(food){
	console.log(this.name + '正在吃：' + food);
}
```

### 原型链继承

父类实例作为子类的原型

```javascript
function Woman(){
}
Woman.prototype = new People();
Woman.prototype.name = 'haixia';
let womanObj = new Woman();
```

优点：简单易于实现，父类的新增的实例与属性子类都可以访问

缺点：创建子类时不能向父类构造函数中传参数。无法实现多继承。

### 借构造函数继承（伪造对象、经典继承）

复制父类的实例属性给子类

```javascript
function Woman(name){
    //继承了People
   	People.call(this);//People.call(this,'wangxiaoxia');
    this.name = name || 'rendo'
}
let womanObj = new Woman();
```

优点：解决了子类构造函数向父类构造函数中传递参数。可以实现多继承（call或者apply多个父类）

缺点：方法都在构造函数中定义，无法复用。不能继承原型属性/方法，只能继承父类的实例属性和方法。

### 实例继承（原型式继承）

```javascript
function Woman(name){
    let instance = new People();
    instance.name = name || 'wangxiaoxia';
    return instance;
}
let womanObj = new Woman();
```

优点：不限制调用方式，简单

缺点：不能多次继承

### 组合式继承

```javascript
function People(name,age){
    this.name = name || 'wangxiao'
    this.age = age || 17
}
People.prototype.eat = function(){
    return this.name + this.age + 'eat sleep'
}
function Woman(name,age){
    People.call(this)
}
Woman.prototype = new People();
Woman.prototype.constructor = Woman;
let womanObj = new Woman(ren,27);
womanObj.eat();
```

优点：函数可以复用，不存在引用属性的问题。可以继承属性和方法，并且可以继承原型的属性和方法。

缺点：由于调用了两次父类，所以产生了两份实例。

### es6继承

```javascript
//class 相当于es5中构造函数
//class中定义方法时，前后不能加function，全部定义在class的protopyte属性中
//class中定义的所有方法是不可枚举的
//class中只能定义方法，不能定义对象，变量等
//class和方法内默认都是严格模式
//es5中constructor为隐式属性
class People{
  constructor(name='wang',age='27'){
    this.name = name;
    this.age = age;
  }
  eat(){
    console.log(`${this.name} ${this.age} eat food`)
  }
}
//继承父类
class Woman extends People{ 
   constructor(name = 'ren',age = '27'){ 
     //继承父类属性
     super(name, age); 
   } 
    eat(){ 
     //继承父类方法
      super.eat() 
    } 
} 
let wonmanObj=new Woman('xiaoxiami'); 
wonmanObj.eat();
```

### es5继承和es6继承的区别

es5继承首先是在子类中创建自己的this指向，最后将方法添加到this中

Child.prototype=new Parent() || Parent.apply(this) || Parent.call(this)

es6继承是使用关键字先创建父类的实例对象this，最后在子类class中修改this