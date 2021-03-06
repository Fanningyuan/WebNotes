# Vue生命周期

[简书](https://www.jianshu.com/p/5cd198945d41)

![](https://pics3.baidu.com/feed/d0c8a786c9177f3e668177cd4bfcf9c19e3d5676.png?token=e1704b12a0e009ba1c294d959ebcaa3e)

### 先罗列一下，稍后一次了解

- beforeCreate()  创建前
- created()  创建
- beforeMount() 挂载前
- mouted() 挂载
- befordUpdate() 更改前
- updated() 更改
- beforeDestroy() 销毁前
- destroyed() 销毁

1. **beforeCreate()**

   该函数执行在组件创建、数据观测 (data observer) 和 event/watcher 事件配置之前，实例初始化之后被调用。
   
   在该阶段组件未创建，不能访问数据，组件中的 data，ref 均为 undefined。
   
   

2. **created()**

   该函数在组件创建完成后被立即调用，在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。

   但是还未渲染成HTML模板，组件中的data对象已经存在，可以对data进行操作了，即可以访问数据，发请求，ref依旧是undefined，挂载阶段还没开始，$el 属性目前尚不可用。

   一般我们可以将对数据的初始化和初始化页面的请求放到里面，结束loading。

3. **beforeMount()**

   该函数在组件挂载之前，在该阶段页面上还没渲染出 HTML 元素，data 初始化完成，ref 依旧不可以操作，相关的 render 函数首次被调用。

   可以访问数据，编译模板结束，虚拟 dom 已经存在。

   该钩子在服务器端渲染期间不被调用。

4. **Mounted()**

   该函数是页面完成挂载之后执行的，这时 el 被新创建的 vm.$el 替换了，就可以操作 ref 了，一般会用于将组件初始时请求数据的方法放到这里面，filter 也是在这里生效。

   如果根实例挂载到了一个文档内的元素上，当 mounted 被调用时 vm.$el 也在文档内。

   可以拿到数据和节点，实例被挂载后调用。

5. **BeforeUpdate()**

   该函数在数据更新时调用，发生在虚拟 DOM 打补丁之前，在有特殊需求的情况下，可以将更新之前的数据存起来，放到后面去使用。

   这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

   该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。

6. **Update()**

   由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子，在数据更新之后做一些处理，即监控数据的变化。

   当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用计算属性或 watcher 取而代之。

7. **BeforeDestroy**

   该函数在实例销毁之前调用，这里的 ref 依旧可以操作，实例仍然完全可用，可以在这里做清除定时器的操作，防止内存泄漏。

   该钩子在服务器端渲染期间不被调用。

8. **Destroyed**

   该函数在组件销毁的时候执行，即实例销毁后调用，这里的 ref 不存在。

   该钩子被调用后，对应 Vue 实例的所有指令都被解绑，所有的事件监听器被移除，所有的子实例也都被销毁。

   该钩子在服务器端渲染期间不被调用。

