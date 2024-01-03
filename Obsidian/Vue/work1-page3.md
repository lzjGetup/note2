# 组件生命周期

Vue 3 的组件生命周期包括创建、挂载、更新和销毁等阶段。下面是 Vue 3 组件的生命周期钩子函数：

1. **beforeCreate**: 在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
2. **created**: 实例已经创建完成之后被调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
3. **beforeMount**: 在挂载开始之前被调用：相关的 render 函数首次被调用。
4. **mounted**: el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。
5. **beforeUpdate**: 数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。
6. **updated**: 由于数据更改导致的虚拟 DOM 重新渲染和打补丁后调用。
7. **beforeUnmount**: 在实例销毁之前调用。在这一步，实例仍然完全可用。
8. **unmounted**: 在实例销毁之后调用。

在 Vue 3 中，获取 DOM 元素通常应该在组件的 mounted 生命周期钩子函数中进行。在这个阶段，组件已经被挂载到 DOM 中，所以可以安全地访问和操作 DOM 元素。



# 动态组件及组件保持存活

动态组件是 Vue 中一种非常有用的特性，它允许你根据当前的数据来动态地切换不同的组件。在 Vue 中，你可以使用 <component/> 元素并通过动态绑定 is 属性来实现动态组件的切换.

>![[Pasted image 20231229154841.png]]

`  <keep-alive></keep-alive>`
包裹组件即可

# 异步加载组件

```vue
//同步加载
import conB from './components/conBDmo.vue';
//异步加载
import { defineAsyncComponent } from 'vue';
const conB = defineAsyncComponent(
  () => import("./components/conBDmo.vue")
)
```


# 依赖注入

依赖注入是一种软件设计模式，它允许你将一个对象的依赖关系传递给另一个对象，而不是在对象内部直接创建这些依赖关系。在 Vue 中，依赖注入通常通过 `provide` 和` inject `这对特殊的选项来实现,注意只能由上到下传递。

==例如==
高层:
  provide:{
    msg: "祖先的遗产"
  }
子类:
  inject: ["msg"]
 















