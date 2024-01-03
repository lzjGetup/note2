# 表达式
`{{ [内容] }}`

>![[Pasted image 20231226143343.png]]

>![[Pasted image 20231226143409.png]]


# 属性绑定

`:`或者`v-bind`
```html
<template>
    <h4>入门</h4>
    <p>{{ msg }}</p>
    <p v-html="rawHtml"></p>
    <div :id="appId">属性绑定</div>
    <button type="button" :disabled="isUsed">按钮</button>
    <button type="button" v-bind="styObj">用对象绑定html属性</button>
</template>

<script>
export default{
  data(){
    return{
      msg: "hello lingzj!",
      rawHtml: "<h4>案例</h4>",
      appId: "head",
      isUsed: false,
      styObj:
        {
          id: "head",
          class: "abc"
        }
      
    }
  }
}
</script>
<style>
#head{
  color: red;
  font-size: 30px;
}
.abc{
  margin: 0px;
}
</style>
```

**styObj:{} 表明可以用一个对象将大量属性绑定,节省代码量,注意属性名需要一致**


# 条件绑定

```html
<template>
    <div>条件渲染</div>
    <p v-if="flag">here</p>
    <p v-else>there</p>
</template>

<script>
export default{
    data(){
        return{
            flag: false
        }
    }
    
}
</script>
```

`v-if` `v-else` `x-else-if`  `v-show`均可以实现条件判断是否渲染

>![[Pasted image 20231226153315.png]]

# 列表渲染

```html
<template>
    <p v-for="(item,index) in names" :key="index">{{ item }}</p>
</template>
<script>
    export default{
        data(){
            return{
                names: ["ling","zj","ganzhou"]
            }
        }
    }
</script>
```

>![[Pasted image 20231226162245.png]]

**其中names对应数据名,`in`可以替换成为`of`**

在Vue中，当你使用v-for指令来渲染一个列表时，每个渲染的元素都需要有一个唯一的key属性。这个key属性的作用是帮助Vue识别每个列表项的身份，以便在数据发生变化时，能够高效地更新DOM。

当列表数据发生变化时，Vue会尽可能地复用已经存在的元素，而不是销毁并重新创建。key属性就是用来帮助Vue识别每个列表项的身份，确保它们能够正确地被复用或者重新渲染。==推荐使用数据id作为key==


# 事件监听

>![[Pasted image 20231226165243.png]]

```html
<button type="button" @click="add">增加</button>
    <p>{{ count }}</p>

    methods:{
        add(){
            this.count++;
        }
    }
```

==注意分辨格式==


# 事件传参

```html
<p @click="strHandle(str,$event)" v-for="(str,index) in names" :key="index">{{ str }}</p>

    methods:{
        strHandle(str){
            console.log(str);
        }
    }
```

==注意此处传递的event对象应该放在传递的参数之后==


# 事件修饰符

以阻止a标签默认事件-跳转页面为例,原生JS采用`e.preventDefault();`
vue提供了事件修饰符,`<a @click.prevent="Handler" href=""></a>`
**e.prevent**,即可完成功能.


# 响应式方法,非响应式方法

1. 响应式方法：
    - push(): 向数组末尾添加新元素。
    - pop(): 从数组末尾移除元素。
    - shift(): 从数组开头移除元素。
    - unshift(): 向数组开头添加新元素。
    - splice(): 可以删除现有元素、添加新元素或者同时进行这两个操作。
2. 非响应式方法：
    - concat(): 用于连接两个或多个数组，并返回一个新数组。
    - slice(): 返回数组的选定部分。
    - sort(): 对数组的元素进行排序。
    - reverse(): 颠倒数组中元素的顺序。

**响应式方法会触发Vue的响应式系统，从而引起数据的变化，而非响应式方法则不会触发数据的更新。在Vue 3中，使用响应式方法可以更方便地处理数组的变化，并确保数据能够及时地反映这些变化。**


# 计算属性
`  methods: {},computed:{}`

在Vue 3中，计算属性和方法（methods）之间有几个重要的区别：

1. **缓存机制**：
    - **计算属性**：计算属性具有缓存机制，只有在它的相关依赖发生改变时才会重新计算。这意味着只要计算属性依赖的响应式数据没有发生变化，多次访问计算属性会直接返回缓存的结果，而不会重新计算。
    - **方法**：方法在每次被访问时都会执行其中的代码，不具有缓存机制。每次调用方法都会重新执行其中的逻辑。
2. **用法**：
    - **计算属性**：适合用于基于响应式数据进行计算，并且希望缓存计算结果的场景，比如对数据进行筛选、排序或格式化。
    - **方法**：适合用于需要进行一些操作或者逻辑判断的场景，比如处理用户输入、触发异步操作等。
3. **调用方式**：
    - **计算属性**：在模板中以属性的形式调用，类似于访问普通的数据属性。
    - **方法**：在模板中以方法的形式调用，需要在模板中使用函数调用的方式来触发执行。

总的来说，计算属性适合用于基于响应式数据的计算，并且希望缓存计算结果的场景，而方法适合用于执行一些操作或者逻辑判断的场景。


# Class属性绑定

>![[Pasted image 20231226203055.png]]


在Vue 3中，使用class属性绑定有一些特别之处：
1. **对象语法**：你可以使用对象语法来动态地绑定多个class。这意味着你可以根据数据的变化来动态地添加或移除class。例如：
```html
<div :class="{ active: isActive, 'text-danger': hasError }"></div>
```
上面的例子中，active和text-danger的class会根据isActive和hasError的值动态地添加或移除。
2. **数组语法**：你也可以使用数组语法来绑定多个class。这在你需要根据条件组合多个class时非常有用。例如：

```html
<div :class="[activeClass, errorClass]"></div>
```
在这个例子中，activeClass和errorClass都是根据某些条件动态确定的class。
3. **内联样式和class的混合**：在Vue 3中，你可以同时使用:class和:style来动态地绑定class和内联样式，这使得你可以非常灵活地控制元素的外观和行为。


==具体实现==

```html
<template>
<p :class="{'sty1':usedsty1,'sty2':usedcol1}">class样式绑定方法一</p>
<p :class="classObj">class样式绑定方法二</p>
<p :class="[arrsty1]">class样式绑定方法三</p>
<p :class="[usedcol4 ? 'sty2' : '']">class样式绑定方法四</p>
</template>
<script>
export default {
  data() {
    return {
        usedsty1: true,
        usedcol1: true,
        classObj: {
            'sty1':true,
            'sty2':false
        },
        arrsty1:'sty1',
        usedcol4: true
    };
  }
};
</script>
<style>
.sty1{
    font-size: 15px;
}
.sty2{
    color: aqua;
}
</style>
```

>![[Pasted image 20231226211826.png]]



==方法一==
在 :class中添加对应样式的选择器,在data中给出控制字即可.
==方法二==
类似方法一
在 :class中添加对应样式的对象,在data中给出对象即可.
==方法三==
在 数组中添加需要显示的样式
==方法四==
在 数组中添加三元运算符,用于逻辑渲染

*注意*
*css选择器必须是字符,如'sty1',而不是sty1*
*数组可以嵌套对象使用,但是不能反过来使用*











