# Vue学习笔记

## Vue的引用

1. 第一种引用方法可以直接用<script>引入，Vue会被注册为一个全局变量

   - 对于制作原型或者学习，可以用

     ```js
     <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
     ```

   - 对于生产环境，推荐使用明确的版本号和构建文件，例如

     ```javascript
     <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
     ```

2. 第二种方式使用NPM进行安装

   ```
   # 最新稳定版
   $ npm install vue
   ```

   

## Vue的核心知识

### 基本使用

#### 插值 表达式 动态属性

Vue.js的核心是一个允许采用简洁模板语法来声明式地将数据渲染进DOM的系统

```javascript
<div id='app'>
	{{message}}
</div>
```

```javascript
var vm = new Vue({
    el:'#app',
    data:{
        message:'Hello Vue！'
    }
})
```

> Hello Vue!

vue在背后进行了大量的工作。现在数据和DOM已经被建立了关联，所有的东西都是**响应式的**。我们在浏览器的javascript控制台修改`vm.message`的值后，在页面会有相应的更新。

在插值中，我们只能在其中写入**表达式**，而不能写入语句

