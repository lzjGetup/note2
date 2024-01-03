# Style绑定

在Vue 3中，可以使用v-bind指令或者简写的:来绑定style属性。你可以直接将一个对象传递给style属性

```html
<template>
    <p :style="{color: activeColor, fontSize: activeSize+'px'}">Style 样式渲染1</p>
    <p :style="styObj">Style 样式渲染2</p>
</template>

<script>
export default{
    data(){
        return{
            activeColor: "green",
            activeSize: "30",
            styObj: {
                color: "red",
                fontSize: "30px"
            }
        }
    }
}
</script>
```


# 侦听器
在Vue 3中，`watch`选项可以用来监听数据的变化并执行相应的操作。你可以在组件的选项中使用watch来监视一个特定的数据，并在数据变化时执行回调函数。

# 模板引用

![[Pasted image 20231228193541.png]]



# 表单输入绑定

在Vue 3中，`v-model`指令用于在表单元素和组件上创建双向数据绑定。

- .lazy 修饰符：默认情况下，v-model会在 input 事件中同步输入框的值到数据，使用.lazy修饰符可以让它改为在 change 事件中同步。

- .trim 修饰符：在用户输入前移除首尾空白字符。

- .number 修饰符：将用户的输入转为数值类型。


```html
<template>
    <p>v-model绑定</p>
    <p>文本框</p>
    <input v-model="msg" type="text">
    <p>{{ msg }}</p>
    <p>复选框</p>
    <input type="checkbox" name="cb" id="" v-model="c1">
    <label for="cb">{{ c1 }}</label>
</template>
<script>
export default{
    data(){
        return{
            msg: "",
            c1: false
        }
    }
}
</script>
```

# 组件

在Vue 3中，一个组件通常由以下几个部分组成：
1. 模板（Template）：定义了组件的结构和布局。
2. 脚本（Script）：包含了组件的行为逻辑，可以包括数据、计算属性、方法等。
3. 样式（Style）：定义了组件的样式，可以使用CSS、SCSS、LESS等来描述组件的外观。

```html
<template>
  <mycomp/>
</template>
<script>
  import mycomp from './components/Mycomp.vue'
  export default{
    components:{
      mycomp
    }
  }
</script>
```

==其中被引用的组件可以只存在template部分,在style部分,可以添加scope属性,让css样式只在当前组件中展示==


# 父子组件消息传递

==父组件==
其中Funame用于绑定数组元素, `<ZiDmoe :names=""/>`用于声明连接到子组件的names属性,同理,`props:["names"]`用于在子组件中声明.不止是数组,对象,字符串,数字,都可以传递.`props`传递数据只读.

>![[Pasted image 20231229101153.png]]

==子组件==

>![[Pasted image 20231229101213.png]]

在子组件中`type`可以针对传递过来的类型进行校验,`default`可以提供默认值,数组和对象默认值需要工厂函数,`require: true`用于表明该传递必须提供,否则发出警告.
*例如*

    props:{
        ziname:{
            type: String,
	         default:"null",
	         require: true
	         /**
	         type: Arrays
	         default(){
		         return []
	         }
	         **/
        }
    }


# 组件事件处理
用于处理父组件对子组件的事件处理,在子事件处理式,使用`this.$emit()`,括号中填写名称与父组件的`@+事件名称`一致.其中,括号里面也可传递参数

zi:
<button @click="clickHandle" type="button">传递数据
        clickHandle(){
            this.$emit("sonEvent")
        }
fu:
<ZiDmo @sonEvent="FuHandler"/>

[组件事件与v-model绑定](https://www.bilibili.com/video/BV1Rs4y127j8/?p=28&spm_id_from=pageDriver&vd_source=c9f01c4138ffca623361215fe6c00336)


# 插槽slot
  
Vue 3 中的插槽（slot）是一种非常强大的功能，它允许你在父组件中将子组件的内容插入到特定的位置。在 Vue 3 中，插槽有两种类型：具名插槽和作用域插槽。

==具体实现==
把原来的`template`中引用组件单标签改为双标签,在双标签内添加内容,在被引用组件加入插槽出口`slot`即可.

对于动态数据,其定义内容应该在的父组件中进行定义.

# 具名插槽

同一个组件中需要多个插槽入口时,可以根据`v-slot`用以区分.`v-slot`可以用`#`号代替

    <template v-slot="header">
    </template>

    <slot  name="header"></slot>



























