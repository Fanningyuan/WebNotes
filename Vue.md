# Vue

### 什么是vue

一款用于构建用户界面的渐进式js框架，vue被设计为自底向上逐层应用，它的核心库只关注图层，方便与第三方库或者已有项目整合。vue.js的核心是一个允许采用简洁的模板语法来声明式将数据渲染进DOM (DocumentObjectModel)的系统，vue特性之一是[响应式原理](https://cn.vuejs.org/v2/guide/reactivity.html)。

### Vue.js 是一个JavaScript  MVVM库

MVVM 是Model-View-ViewModel 的缩写，它是一种基于前端开发的架构模式，其**核心是提供对View 和 ViewModel 的双向数据绑定，这使得ViewModel 的状态改变可以自动传递给 View，即所谓的数据双向绑定**。

Vue.js 是一个提供了 MVVM 风格的双向数据绑定的 Javascript 库，专注于View 层。它的核心是 MVVM 中的 VM，也就是 ViewModel。 ViewModel负责连接 View 和 Model，保证视图和数据的一致性，这种轻量级的架构让前端开发更加高效、便捷。

**为什么会出现 MVVM 呢？**

　　MVC 即 Model-View-Controller 的缩写，就是 模型—视图—控制器，也就是说一个标准的Web 应用程式是由这三部分组成的：

　　View ：用来把数据以某种方式呈现给用户

　　Model ：其实就是数据

　　Controller ：接收并处理来自用户的请求，并将 Model 返回给用户

　　在HTML5 还未火起来的那些年，MVC 作为Web 应用的最佳实践是OK 的，这是因为 Web 应用的View 层相对来说比较简单，前端所需要的数据在后端基本上都可以处理好，View 层主要是做一下展示，那时候提倡的是 Controller 来处理复杂的业务逻辑，所以View 层相对来说比较轻量，就是所谓的**瘦客户端思想**。

　　**为什么要使用MVC？** 

　　相对 HTML4，HTML5 最大的亮点是**它为移动设备提供了一些非常有用的功能**，使得 HTML5 具备了开发App的能力， HTML5开发App 最大的好处就是**跨平台、快速迭代和上线，节省人力成本和提高效率**，因此很多企业开始对传统的App进行改造，逐渐用H5代替Native，到2015年的时候，市面上大多数App 或多或少嵌入都了H5 的页面。既然要用H5 来构建 App， 那View 层所做的事，就不仅仅是简单的数据展示了，它不仅要管理复杂的数据状态，还要处理移动设备上各种操作行为等等。因此，前端也需要工程化，也需要一个类似于MVC 的框架来管理这些复杂的逻辑，使开发更加高效。 但这里的 MVC 又稍微发了点变化：

　　View ：UI布局，展示数据

　　Model ：管理数据

　　Controller ：响应用户操作，并将 Model 更新到 View 上

　　这种 MVC 架构模式对于简单的应用来看是OK 的，也符合软件架构的分层思想。 但实际上，随着H5 的不断发展，人们更希望使用H5 开发的应用能和Native 媲美，或者接近于原生App 的体验效果，于是前端应用的复杂程度已不同往日，今非昔比。这时前端开发就暴露出了三个痛点问题：

　　1、 开发者在代码中大量调用相同的 DOM API，处理繁琐 ，操作冗余，使得代码难以维护。

　　2、大量的DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。

　　3、 当 Model 频繁发生变化，开发者需要主动更新到View ；当用户的操作导致 Model 发生变化，开发者同样需要将变化的数据同步到Model 中，这样的工作不仅繁琐，而且很难维护复杂多变的数据状态。

　　其实，早期jquery 的出现就是为了前端能更简洁的操作DOM 而设计的，但它只解决了第一个问题，另外两个问题始终伴随着前端一直存在。

　　**MVVM 的出现，完美解决了以上三个问题。**

　　MVVM 由 Model、View、ViewModel 三部分构成，Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

　　**在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上**。

　　ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM， 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

Vue.js 是**采用 Object.defineProperty 的 getter 和 setter，并结合观察者模式来实现数据绑定的**。**当把一个普通 Javascript 对象传给 Vue 实例来作为它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化。**

**![img](D:\fanningyuan\Desktop\1158910-20180306234148823-430002059.png)**

 

　　Observer ：数据监听器，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者，内部采用Object.defineProperty的getter和setter来实现

　　Compile ：指令解析器，它的作用对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数

　　Watcher ：订阅者，作为连接 Observer 和 Compile 的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数

　　Dep ：消息订阅器，内部维护了一个数组，用来收集订阅者（Watcher），数据变动触发notify 函数，再调用订阅者的 update 方法

　　从图中可以看出，**当执行 new Vue() 时，Vue 就进入了初始化阶段，一方面Vue 会遍历 data 选项中的属性，并用 Object.defineProperty 将它们转为 getter/setter，实现数据变化监听功能；另一方面，Vue 的指令编译器Compile 对元素节点的指令进行扫描和解析，初始化视图，并订阅 Watcher 来更新视图， 此时Wather 会将自己添加到消息订阅器中(Dep)，初始化完毕。**

　　**当数据发生变化时，Observer 中的 setter 方法被触发，setter 会立即调用Dep.notify()，Dep 开始遍历所有的订阅者，并调用订阅者的 update 方法，订阅者收到通知后对视图进行相应的更新。**

### vue的核心功能

#### 计算属性

计算属性就是当其依赖属性的值发生变化时，这个属性的值会自动更新，与之相关的DOM部分也会同步自动更新。除了getter。我们还可以设置计算属性的setter。

```vue
data:{
            JD:'JD',
            family:'family'
        },
        computed:{
            <!-- 一个计算属性的getter -->
            JDFamily:function(){
                return this.JD+this.family
            }
             <!-- 一个计算属性的setter -->
            set:function(newVal){
                let names = newVal.split('')
                this.JD = names[0]
                this.family = names[1]
            }
        }
```

除了使用计算属性外，我们也可以通过在表达式中调用方法来达到同样的效果。然而，不同的是**计算属性是基于它们的依赖进行缓存的**。计算属性只有在它的相关依赖发生改变时才会重新求值。

这就意味着只要 JD和family还没有发生改变，多次访问 JDFamily计算属性会立即返回之前的计算结果，而不必再次执行函数。

如果不希望有缓存，就用方法来替代。

#### 模板语法

Vue.js 使用了基于 HTML 的模版语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。Vue的模版语法包括了使用双大括号插入文本、使用v-html插入纯HTML内容、使用v-bind插入对象、类似angular的v-if、v-show、v-for指令、以及过滤器等等。 

这里单独放一下过滤器

**过滤器是用来干什么的**

对文本进行格式化的

**过滤器用在什么地方**

过滤器可以用在两个地方：mustache 插值和 v-bind 表达式。

【反转案例】

```vue
<div id="app">
    {{msg|guolvqi}}
    {{msg|guolvqi}}
    {{msg|guolvqi}}
</div>
<script>
    var app = new Vue({
        el:"#app",
        data:{
            msg:"xue xi vue!"
        },
        //定义过滤器
        filters: {
            guolvqi:function(value){
                return value.split("").reverse().join("")
            }
        }
    });
</script>
打印结果：!euv ix eux !euv ix eux !euv ix eux
```

【串联一个大写案例】

```vue
<div id="app">
    {{msg|guolvqi|daxie}}
    {{msg|guolvqi|daxie}}
    {{msg|guolvqi|daxie}}
</div>
<script>
    var app = new Vue({
        el:"#app",
        data:{
            msg:"xue xi vue!"
        },
        //定义过滤器
        filters: {
            guolvqi:function(value){
                return value.split("").reverse().join("")
            },
            daxie:function(value){
                return value.toUpperCase();
            }
        }
    });
</script>
打印结果：!EUV IX EUX !EUV IX EUX !EUV IX EUX
```

过滤器也可以接收参数

#### 组件化

**组件的分类**

1. 页面级别的组件。
2. 业务上可复用的基础组件。
3. 与业务无关的独立组件。

**页面级别的组件**

页面级别的组件，通常是pages目录下的.vue组件，是组成整个项目的一个大的页面。一般不会有对外的接口。我们通常开发时，主要就是编写这种组件。如下所示：pages下面的Home.vue(主页)和About.vue(关于我们)等都是一个独立的页面，也是一个独立的组件。

```
  pages
  ├─ About.vue
  └─ Home.vue
```

**业务上可复用的基础组件**

这一类组件通常是在业务中被各个页面复用的组件，这一类组件通常都写到components目录下，然后通过import在各个页面中使用。这一类组件通常是实现某个功能，比如外卖中各个页面都会使用到的评分系统。这个部分就可以实现评分功能，可以写成一个独立的业务组件。比如下面的components中的Star.vue就是一个业务组件。这一类组件的编写通常涉及到组件常用的`props`,`slot`和自定义事件等。

```
  components
  └─ Star.vue
```

**与业务无关的独立组件**

这一类组件通常是与业务功能无关的独立组件。这类组件通常是作为基础组件，在各个业务组件或者页面组件中被使用。目前市面上比较流行的ElementUI中包含的组件都是独立组件。

**属性prop**

**数组形式：**

```vue
props:['name','age']
```

**对象形式：** 使用对象的形式，可以对数据的类型，是否必填，以及其他特征进行校验。这对于组件化开发非常有利。

Child.vue定义组件

```vue
<template>
  <div class="container">
    姓名：{{name}}
    年龄：{{age}}
  </div>
</template>

<script>
export default {
  name:'Child',
  props:{
    name:{
      type:String,
      require:true
    },
    age:{
      type:Number
    }
  }
}
</script>
```

Parent.vue使用组件

```vue
<Child :name = name  :age = age></Child>
```

**自定义事件**

如何触发组件上定义的事件：
假设现在我们需要给我们定义的Child组件添加点击事件：这时候我们一般是通过在组件内部的button上通过$emit触发事件，然后在父组件中监听。
在组件中通过$emit定义事件：
Child.vue

```vue
<template>
  <div class="container">
    姓名：{{name}}
    年龄：{{age}}
    <!-- 触发事件 -->
    <button @click ="$emit('onClick','自定义事件')">点击</button>
  </div>
</template>
```

Parent.vue监听事件

```vue
 <Child @onClick = 'handleClick' :age = age></Child>
```

**slot**

我们定义的组件通常会被用到各个地方，但是并不一定能够满足所有的使用场景，有时候我们需要进行一些功能的扩展。这时候就需要用到slot了。一句话描述slot:**就是用来在组件中插入新的内容**。
比如我们刚刚定义的Child组件，需要插入一段话。那么这时候就需要用到slot了。
Child.vue中使用slot

```vue
<template>
  <div class="container">
    姓名：{{name}}
    年龄：{{age}}
    <button @click ="$emit('onClick','自定义事件')">点击</button>
    <slot></slot>
  </div>
</template>
```

Parent.vue中扩展功能。插入一段话：

```vue
<template>
  <div class="container">
    <Child @onClick = 'handleClick' :age = age>
      <div>这是通过slot插入的一段话</div>
    </Child>
  </div>
</template>
```

如上所示：在Child.vue中使用了slot，在Parent.vue中使用Child时，插入了一段话。

### Vue的配置文件

#### env文件

**关于文件名：必须以如下方式命名，不要乱起名，也无需专门手动控制加载哪个文件**

.env 全局默认配置文件，不论什么环境都会加载合并

.env.development 开发环境下的配置文件

.env.production 生产环境下的配置文件

![image-20210602173223841](D:\fanningyuan\Desktop\image-20210602173223841.png)

**关于文件内容：**

注意：属性名必须以VUE_APP_开头，比如VUE_APP_XXX

![image-20210602173247064](D:\fanningyuan\Desktop\image-20210602173247064.png)

**关于文件的加载：**

根据启动命令vue会自动加载对应的环境，vue是根据文件名进行加载的，所以上面说“不要乱起名，也无需专门控制加载哪个文件

比如执行npm run dev命令，会自动加载.env.dev文件

#### vue.config.js

这个文件应该导出一个包含了选项的对象：

![img](D:\fanningyuan\Desktop\webp.png)

**配置选项** 

**publicPath** 

> Type: string
>
> Default: '/'
>
>  部署应用包时的基本 URL， 用法和 webpack 本身的 output.publicPath 一致。
>
> 这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径。

​	把开发服务器架设在根路径，可以使用一个条件式的值：![image-20210602173529936](D:\fanningyuan\Desktop\image-20210602173529936.png)

**outputDir**

> Type: string
>
> Default: 'dist'
>
> 输出文件目录，当运行 vue-cli-service build 时生成的生产环境构建文件的目录。注意目标目录在构建之前会被清除 (构建时传入 --no-clean 可关闭该行为)。

![image-20210602173639138](D:\fanningyuan\Desktop\image-20210602173639138.png)

**lintOnSave**

> Type: boolean | 'error'
>
> Default: true
>
> 是否在保存的时候使用 `eslint-loader` 进行检查。 有效的值：`ture` | `false` | `"error"` 当设置为 `"error"` 时，检查出的错误会触发编译失败。

![image-20210602173750654](D:\fanningyuan\Desktop\image-20210602173750654.png)

**runtimeCompiler**

> Type: boolean
>
> Default: false
>
> 是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。

![image-20210602173836489](D:\fanningyuan\Desktop\image-20210602173836489.png)

**productionSourceMap**

> Type: boolean
>
> Default: true
>
> 如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。

![image-20210602173919888](D:\fanningyuan\Desktop\image-20210602173919888.png)

**Webpack相关配置**

**chainWebpack**

> Type: Function
>
> 是一个函数，会接收一个基于 webpack-chain 的 ChainableConfig 实例。允许对内部的 webpack 配置进行更细粒度的修改。

![image-20210602174125083](D:\fanningyuan\Desktop\image-20210602174125083.png)

**css相关设置**

![img](D:\fanningyuan\Desktop\1111.png)

**css.loaderOptions**

> Type: Object
>
> Default: {}
>
> 向 CSS 相关的 loader 传递选项。

支持的 loader 有：

> css-loader
>
> postcss-loader
>
> sass-loader
>
> less-loader
>
> stylus-loader

**devServer设置**

> Type: Object
>
> 所有 webpack-dev-server 的选项都支持。注意：
>
> 有些值像 host、port 和 https 可能会被命令行参数覆写。
>
> 有些值像 publicPath 和 historyApiFallback 不应该被修改，因为它们需要和开发服务器的 [publicPath](https://links.jianshu.com/go?to=https%3A%2F%2Fcli.vuejs.org%2Fzh%2Fconfig%2F%23baseurl) 同步以保障正常的工作。

**devServer.proxy**

> Type: string | Object
>
> 如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。这个问题可以通过 vue.config.js 中的 devServer.proxy 选项来配置。

![image-20210602174512048](D:\fanningyuan\Desktop\image-20210602174512048.png)



#### package.json

**scripts**

指定了运行脚本命令的npm命令行缩写

![image-20210602174753688](D:\fanningyuan\Desktop\image-20210602174753688.png)

**dependencies，devDependencies**

dependencies和devDependencies两项，分别指定了项目运行所依赖的模块、项目开发所需要的模块。它们都指向一个对象，该对象的各个成员，分别由模块名和对应的版本要去组成，表示依赖的模块及其版本范围

--save参数表示将该模块写入dependencies属性，
--save-dev表示将该模块写入devDependencies属性。

![image-20210602174848562](D:\fanningyuan\Desktop\image-20210602174848562.png)

**engines 字段**

指明了该项目所需要的node.js版本

![image-20210602174937089](D:\fanningyuan\Desktop\image-20210602174937089.png)

#### package-lock.json

​		npm5之前的版本，是不会生成package-lock.json这个文件的。npm5版本及以后，才会生成package-lock.json文件；当使用npm安装包的时候，npm都会生成或者更新package-lock.json文件，npm5版本及以后的版本，在安装包的时候，不需要加 --save（-s） 参数，也会自动在package.json中保存依赖项，当安装包的时候，会自动创建或者更新package-lock.json文件。

　　package-lock.json文件内保存了 node_modules中所有包的信息，包含着这些包的名称、版本号、下载地址。这样带来好处是，如果重新 npm install 的时候，就无需逐个分析包的依赖项，因此会大大加快安装速度。

　　package-lock.json文件，lock代表的是“锁定”的意思。用来锁定当前开发使用的版本号，防止npm install的时候自动更新到了更新版本。因为新版本可能替换掉老的api，导致之前的代码报错。

　　package.json 文件只能锁定大版本，也就是版本号的第一位，并不能锁定后面的小版本，你每次npm install都是拉取的该大版本下的最新的版本，为了稳定性考虑我们几乎是不敢随意升级依赖包的，这将导致多出来很多工作量，测试/适配等，这个时候package-lock.json文件应运而生，所以当你每次安装一个依赖的时候就锁定在你安装的这个版本。

　　package.json文件记录你项目中所需要的所有模块。当你执行npm install的时候，node会先从package.json文件中读取所有dependencies信息，然后根据dependencies中的信息与node_modules中的模块进行对比，没有的直接下载，已有的检查更新（最新版本的nodejs不会更新，因为有package-lock.json文件，下面再说）。另外，package.json文件只记录你通过npm install方式安装的模块信息，而这些模块所依赖的其他子模块的信息不会记录。

　　package-lock.json文件锁定所有模块的版本号，包括主模块和所有依赖子模块。当你执行npm install的时候，node从package.json文件读取模块名称，从package-lock.json文件中获取版本号，然后进行下载或者更新。因此，正因为有了package-lock.json文件锁定版本号，所以当你执行npm install的时候，node不会自动更新package.json文件中的模块，必须用npm install packagename（自动更新小版本号）或者npm install packagename@x.x.x（指定版本号）来进行安装才会更新，package-lock.json文件中的版本号也会随着更新。

### Vue2.0和3.0的主要区别

这里我主要列举了一些用法的变化，并没有列举完全，如果想详细了解，可以查看[Vue官方文档](https://v3.vuejs.org/guide/installation.html)

#### **main.js的变化**

```jsx
//vue3.0
import { createApp } from 'vue';
import App from './App.vue'
createApp(App).mount('#app')

//vue2.0
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false
new Vue({
  render: h => h(App),
}).$mount('#app')
```

我们会发现3.0比2.0的要精简了许多，同时还引入了一个新的函数名createApp,会把容器挂载到它上面来。

#### **生命周期**

beforeCreate/created => setup
boforeMount => onBeforeMount
Mounted => onMounted
beforeUpdata => onBeforeUpdate
Updated => onUpdated
beforeDestroy -> onBeforeUnmount
destoryed => onUmonted
errorCaptured -> onErrorCaptured

如果要想在页面中使用生命周期函数的，根据以往2.0的操作是直接在页面中写入生命周期，而现在是需要去引用的，这就是为什么3.0能够将代码压缩到更低的原因。

```jsx
import {reactive, ref, onMounted} from 'vue'
export default {
 setup(){
   const name = reactive({
     name:'王'
   })
   const count=ref(0)
   const increamt=()=>{
     count.value++
   }
   onMounted(()=>{
     console.log('123')
   })
   return {name,count,increamt}
 }  
```

#### **Data**

```js
export default {
  data(){
    return{

    }
  }
},
///////////////////////
取而代之是使用以下的方式去初始化数据:



// 基本数据类型
import { ref } from 'vue'
let count = ref('aaa')   //  注意，这里多了一个ref()
console.log(count.value)   // aaa
count.value = 'bb' // 赋值
/*
基本数据类型获取变量的值需要使用（变量.value）来获取值，在模板中可以直接使用（变量）
*/

// 对象
import { reactive  } from 'vue'
const obj = reactive({
  name: '111'
})
console.log(obj.name)   // 111
return  {
  count,
  obj
}
```

#### **模板可以有多个根标签**

```
<template>
   <div></div>
   <div></div>
</template>
```

#### **Vue 3.0**实现响应式基于ES6:Proxy

Vue2.0

- 基于**Object.defineProperty**，不具备监听数组的能力，需要重新定义数组的原型来达到响应式。
- **Object.defineProperty** 无法检测到对象属性的添加和删除 。
- 由于Vue会在初始化实例时对属性执行getter/setter转化，所有属性必须在data对象上存在才能让Vue将它转换为响应式。
- 深度监听需要一次性递归，对性能影响比较大。

Vue3.0

- 基于**Proxy**和**Reflect**，可以原生监听数组，可以监听对象属性的添加和删除。
- 不需要一次性遍历data的属性，可以显著提高性能。
- 因为Proxy是ES6新增的属性，有些浏览器还不支持,只能兼容到IE11 

Vue3.0基于**Proxy**来做数据大劫持代理，可以原生支持到数组的响应式，不需要重写数组的原型，还可以直接支持新增和删除属性， 比Vue2.x的**Object.defineProperty**更加的清晰明了。

核心代码

```js
 const proxyData = new Proxy(data, {
   get(target,key,receive){ 
     // 只处理本身(非原型)的属性
     const ownKeys = Reflect.ownKeys(target)
     if(ownKeys.includes(key)){
       console.log('get',key) // 监听
     }
     const result = Reflect.get(target,key,receive)
     return result
   },
   set(target, key, val, reveive){
     // 重复的数据，不处理
     const oldVal = target[key]
     if(val == oldVal){
       return true
     }
     const result = Reflect.set(target, key, val,reveive)
     return result
   },
   // 删除属性
   deleteProperty(target, key){
     const result = Reflect.deleteProperty(target,key)
     return result
   }
 })
```

### Proxy

#### proxy概述

> `proxy`在目标对象的外层搭建了一层拦截，外界对目标对象的某些操作，必须通过这层拦截



```js
var proxy = new Proxy(target, handler);
```

> `new Proxy()`表示生成一个`Proxy`实例，`target`参数表示所要拦截的目标对象，`handler`参数也是一个对象，用来定制拦截行为



```js
var target = {
   name: 'poetries'
 };
 var logHandler = {
   get: function(target, key) {
     console.log(`${key} 被读取`);
     return target[key];
   },
   set: function(target, key, value) {
     console.log(`${key} 被设置为 ${value}`);
     target[key] = value;
   }
 }
 var targetWithLog = new Proxy(target, logHandler);
 
 targetWithLog.name; // 控制台输出：name 被读取
 targetWithLog.name = 'others'; // 控制台输出：name 被设置为 others
 
 console.log(target.name); // 控制台输出: others
```

- `targetWithLog` 读取属性的值时，实际上执行的是 `logHandler.get` ：在控制台输出信息，并且读取被代理对象 `target` 的属性。
- 在 `targetWithLog` 设置属性值时，实际上执行的是 `logHandler.set` ：在控制台输出信息，并且设置被代理对象 `target` 的属性的值



```js
// 由于拦截函数总是返回35，所以访问任何属性都得到35
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

proxy.time // 35
proxy.name // 35
proxy.title // 35
```

**Proxy 实例也可以作为其他对象的原型对象**



```js
var proxy = new Proxy({}, {
  get: function(target, property) {
    return 35;
  }
});

let obj = Object.create(proxy);
obj.time // 35
```

> `proxy`对象是`obj`对象的原型，`obj`对象本身并没有`time`属性，所以根据原型链，会在`proxy`对象上读取该属性，导致被拦截

**Proxy的作用**

> 对于代理模式 `Proxy` 的作用主要体现在三个方面

- 拦截和监视外部对对象的访问
- 降低函数或类的复杂度
- 在复杂操作前对操作进行校验或对所需资源进行管理

#### Proxy所能代理的范围--handler

> 实际上 `handler` 本身就是`ES6`所新设计的一个对象.它的作用就是用来 自定义代理对象的各种可代理操作 。它本身一共有`13`中方法,每种方法都可以代理一种操作.其`13`种方法如下



```js
// 在读取代理对象的原型时触发该操作，比如在执行 Object.getPrototypeOf(proxy) 时。
handler.getPrototypeOf()

// 在设置代理对象的原型时触发该操作，比如在执行 Object.setPrototypeOf(proxy, null) 时。
handler.setPrototypeOf()

 
// 在判断一个代理对象是否是可扩展时触发该操作，比如在执行 Object.isExtensible(proxy) 时。
handler.isExtensible()

 
// 在让一个代理对象不可扩展时触发该操作，比如在执行 Object.preventExtensions(proxy) 时。
handler.preventExtensions()

// 在获取代理对象某个属性的属性描述时触发该操作，比如在执行 Object.getOwnPropertyDescriptor(proxy, "foo") 时。
handler.getOwnPropertyDescriptor()

 
// 在定义代理对象某个属性时的属性描述时触发该操作，比如在执行 Object.defineProperty(proxy, "foo", {}) 时。
andler.defineProperty()

 
// 在判断代理对象是否拥有某个属性时触发该操作，比如在执行 "foo" in proxy 时。
handler.has()

// 在读取代理对象的某个属性时触发该操作，比如在执行 proxy.foo 时。
handler.get()

 
// 在给代理对象的某个属性赋值时触发该操作，比如在执行 proxy.foo = 1 时。
handler.set()

// 在删除代理对象的某个属性时触发该操作，比如在执行 delete proxy.foo 时。
handler.deleteProperty()

// 在获取代理对象的所有属性键时触发该操作，比如在执行 Object.getOwnPropertyNames(proxy) 时。
handler.ownKeys()

// 在调用一个目标对象为函数的代理对象时触发该操作，比如在执行 proxy() 时。
handler.apply()

 
// 在给一个目标对象为构造函数的代理对象构造实例时触发该操作，比如在执行new proxy() 时。
handler.construct()
```

#### Proxy场景

##### 实现私有变量

```js
var target = {
   name: 'poetries',
   _age: 22
}

var logHandler = {
  get: function(target,key){
    if(key.startsWith('_')){
      console.log('私有变量age不能被访问')
      return false
    }
    return target[key];
  },
  set: function(target, key, value) {
     if(key.startsWith('_')){
      console.log('私有变量age不能被修改')
      return false
    }
     target[key] = value;
   }
} 
var targetWithLog = new Proxy(target, logHandler);
 
// 私有变量age不能被访问
targetWithLog.name; 
 
// 私有变量age不能被修改
targetWithLog.name = 'others'; 
```

> 在下面的代码中，我们声明了一个私有的 `apiKey`，便于 `api` 这个对象内部的方法调用，但不希望从外部也能够访问 `api._apiKey`



```js
var api = {  
    _apiKey: '123abc456def',
    /* mock methods that use this._apiKey */
    getUsers: function(){}, 
    getUser: function(userId){}, 
    setUser: function(userId, config){}
};

// logs '123abc456def';
console.log("An apiKey we want to keep private", api._apiKey);

// get and mutate _apiKeys as desired
var apiKey = api._apiKey;  
api._apiKey = '987654321';
```

> 很显然，约定俗成是没有束缚力的。使用 `ES6 Proxy` 我们就可以实现真实的私有变量了，下面针对不同的读取方式演示两个不同的私有化方法。第一种方法是使用 `set / get` 拦截读写请求并返回 `undefined`:



```js
let api = {  
    _apiKey: '123abc456def',
    getUsers: function(){ }, 
    getUser: function(userId){ }, 
    setUser: function(userId, config){ }
};

const RESTRICTED = ['_apiKey'];
api = new Proxy(api, {  
    get(target, key, proxy) {
        if(RESTRICTED.indexOf(key) > -1) {
            throw Error(`${key} is restricted. Please see api documentation for further info.`);
        }
        return Reflect.get(target, key, proxy);
    },
    set(target, key, value, proxy) {
        if(RESTRICTED.indexOf(key) > -1) {
            throw Error(`${key} is restricted. Please see api documentation for further info.`);
        }
        return Reflect.get(target, key, value, proxy);
    }
});

// 以下操作都会抛出错误
console.log(api._apiKey);
api._apiKey = '987654321';  
```

> 第二种方法是使用 `has` 拦截 `in` 操作



```js
var api = {  
    _apiKey: '123abc456def',
    getUsers: function(){ }, 
    getUser: function(userId){ }, 
    setUser: function(userId, config){ }
};

const RESTRICTED = ['_apiKey'];
api = new Proxy(api, {  
    has(target, key) {
        return (RESTRICTED.indexOf(key) > -1) ?
            false :
            Reflect.has(target, key);
    }
});

// these log false, and `for in` iterators will ignore _apiKey
console.log("_apiKey" in api);

for (var key in api) {  
    if (api.hasOwnProperty(key) && key === "_apiKey") {
        console.log("This will never be logged because the proxy obscures _apiKey...")
    }
}
```

##### 抽离校验模块

> 让我们从一个简单的类型校验开始做起，这个示例演示了如何使用 `Proxy` 保障数据类型的准确性



```js
let numericDataStore = {  
    count: 0,
    amount: 1234,
    total: 14
};

numericDataStore = new Proxy(numericDataStore, {  
    set(target, key, value, proxy) {
        if (typeof value !== 'number') {
            throw Error("Properties in numericDataStore can only be numbers");
        }
        return Reflect.set(target, key, value, proxy);
    }
});

// 抛出错误，因为 "foo" 不是数值
numericDataStore.count = "foo";

// 赋值成功
numericDataStore.count = 333;
```

> 如果要直接为对象的所有属性开发一个校验器可能很快就会让代码结构变得臃肿，使用 `Proxy` 则可以将校验器从核心逻辑分离出来自成一体



```js
function createValidator(target, validator) {  
    return new Proxy(target, {
        _validator: validator,
        set(target, key, value, proxy) {
            if (target.hasOwnProperty(key)) {
                let validator = this._validator[key];
                if (!!validator(value)) {
                    return Reflect.set(target, key, value, proxy);
                } else {
                    throw Error(`Cannot set ${key} to ${value}. Invalid.`);
                }
            } else {
                throw Error(`${key} is not a valid property`)
            }
        }
    });
}

const personValidators = {  
    name(val) {
        return typeof val === 'string';
    },
    age(val) {
        return typeof age === 'number' && val > 18;
    }
}
class Person {  
    constructor(name, age) {
        this.name = name;
        this.age = age;
        return createValidator(this, personValidators);
    }
}

const bill = new Person('Bill', 25);

// 以下操作都会报错
bill.name = 0;  
bill.age = 'Bill';  
bill.age = 15;  
```







－－－－－－－－－－－－－－－－－－－－－－－－－－这是一条分割线－－－－－－－－－－－－－－－－－－－－－－－－－－－

＜！．．．以下暂时没学太明白，先放在这慢慢理解．．．--->

##### 访问日志

> 对于那些调用频繁、运行缓慢或占用执行环境资源较多的属性或接口，开发者会希望记录它们的使用情况或性能表现，这个时候就可以使用 `Proxy` 充当中间件的角色，轻而易举实现日志功能



```js
let api = {  
    _apiKey: '123abc456def',
    getUsers: function() { /* ... */ },
    getUser: function(userId) { /* ... */ },
    setUser: function(userId, config) { /* ... */ }
};

function logMethodAsync(timestamp, method) {  
    setTimeout(function() {
        console.log(`${timestamp} - Logging ${method} request asynchronously.`);
    }, 0)
}

api = new Proxy(api, {  
    get: function(target, key, proxy) {
        var value = target[key];
        return function(...arguments) {
            logMethodAsync(new Date(), key);
            return Reflect.apply(value, target, arguments);
        };
    }
});

api.getUsers();
```

##### 预警和拦截

> 假设你不想让其他开发者删除 `noDelete` 属性，还想让调用 `oldMethod` 的开发者了解到这个方法已经被废弃了，或者告诉开发者不要修改 `doNotChange` 属性，那么就可以使用 `Proxy` 来实现



```js
let dataStore = {  
    noDelete: 1235,
    oldMethod: function() {/*...*/ },
    doNotChange: "tried and true"
};

const NODELETE = ['noDelete'];  
const NOCHANGE = ['doNotChange'];
const DEPRECATED = ['oldMethod'];  

dataStore = new Proxy(dataStore, {  
    set(target, key, value, proxy) {
        if (NOCHANGE.includes(key)) {
            throw Error(`Error! ${key} is immutable.`);
        }
        return Reflect.set(target, key, value, proxy);
    },
    deleteProperty(target, key) {
        if (NODELETE.includes(key)) {
            throw Error(`Error! ${key} cannot be deleted.`);
        }
        return Reflect.deleteProperty(target, key);

    },
    get(target, key, proxy) {
        if (DEPRECATED.includes(key)) {
            console.warn(`Warning! ${key} is deprecated.`);
        }
        var val = target[key];

        return typeof val === 'function' ?
            function(...args) {
                Reflect.apply(target[key], target, args);
            } :
            val;
    }
});

// these will throw errors or log warnings, respectively
dataStore.doNotChange = "foo";  
delete dataStore.noDelete;  
dataStore.oldMethod();
```

##### 过滤操作

> 某些操作会非常占用资源，比如传输大文件，这个时候如果文件已经在分块发送了，就不需要在对新的请求作出相应（非绝对），这个时候就可以使用 `Proxy` 对当请求进行特征检测，并根据特征过滤出哪些是不需要响应的，哪些是需要响应的。下面的代码简单演示了过滤特征的方式，并不是完整代码，相信大家会理解其中的妙处



```js
let obj = {  
    getGiantFile: function(fileId) {/*...*/ }
};

obj = new Proxy(obj, {  
    get(target, key, proxy) {
        return function(...args) {
            const id = args[0];
            let isEnroute = checkEnroute(id);
            let isDownloading = checkStatus(id);      
            let cached = getCached(id);

            if (isEnroute || isDownloading) {
                return false;
            }
            if (cached) {
                return cached;
            }
            return Reflect.apply(target[key], target, args);
        }
    }
});
```

##### 中断代理

> `Proxy` 支持随时取消对 `target` 的代理，这一操作常用于完全封闭对数据或接口的访问。在下面的示例中，我们使用了 `Proxy.revocable` 方法创建了可撤销代理的代理对象：



```js
let sensitiveData = { username: 'devbryce' };
const {sensitiveData, revokeAccess} = Proxy.revocable(sensitiveData, handler);
function handleSuspectedHack(){  
    revokeAccess();
}

// logs 'devbryce'
console.log(sensitiveData.username);
handleSuspectedHack();
// TypeError: Revoked
console.log(sensitiveData.username);
```

