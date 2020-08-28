# ts父子组件传值

### 父向子传值

在父组件向子组件进行传值时，在父组件中向子组件便签中添加属性。

```tsx
//父组件中，向子组件便签中添加变量属性
<propDemo data = {this.name} on-father = {this.change}></propDemo>
```

在子组件中使用`@Prop() readonly 属性名 !: string|number`

### 子向父传值

在子组件向父组件传值时，用Emit定义方法

```tsx
//ts
itemChange(val:any) {
  this.$emit("事件名", val)
}
//ts使用装饰器
@Emit('事件名'){
    itemChange(val:any){
        return val
    }
}
@Emit()     //注意：若不定义触发事件名称，父组件绑定的名称必须小写当前事件名称
itemchange(val:any){
  return val
}
```

在父组件中，在子组件便签中使用`on-事件名 = {父组件中的方法对传回的值进行处理}`