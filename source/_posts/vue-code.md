---
title: vue源码解读
date: 2018-06-13 10:37:18
tags: js
---

## vue生命周期
- new Vue()
    - 创建Vue实例
- 创建前后
    - 在实例创建之后，数据观测（data observe）和事件配置（events/watcher）之前被调用beforeCreate
        - beforeCreate阶段，vue的挂载元素el和数据对象data都是undefined，未初始化
    - 实例创建后立即调用created
        - Vue实例的数据对象data有了，但el还没有
- 载入前后（在服务端渲染都不会被调用）
    - 挂载实例之前调用beforeMount，相关的render函数首次被调用beforeMount
        - Vue实例的$el和data都初始化了，但挂载之前还是虚拟dom节点，相关的data下的数据未替换
    - $el被新创建的vm.$el替换，并挂载到实例上去之后调用mounted
        - Vue实例挂载完成，相关的数据会被替换渲染
- 更新前后
    - 数据更新时调用beforeUpdate，发生在虚拟dom打补丁之前
        - 这里适合更新之前访问的dom，比如手动移除已添加的事件监听器
    - 数据更新导致的虚拟dom重新渲染和打补丁，之后调用updated
- 销毁前后
    - 实例销毁之前调用beforeUpdate，在这一步，实例仍然完全可用
    - Vue实例销毁之后调用
        - 实例的所有东西都会被解绑，所有的事件监听器都会被移除，所有的子实例都会被销毁
- code
    ``` JavaScript
        // 例子 ~/backup_code/learn/example/js-pro/vue-code.html
        new Vue()
        beforeCreate()
        created()
        beforeMount()
        ...compile...
        mounted()
        beforeUpdate()
        updated()
        beforeDestroy()
        destroyed()
    ```

## 双向数据绑定原理
- [definePrototype和proxy的区别](https://juejin.im/post/5acd0c8a6fb9a028da7cdfaf)
- 数据劫持结合发布者 - 订阅者的方式，通过defineProperty来劫持各个属性的setter、getter，在数据变动时发布消息给订阅者，触发相关的监听回调
- defineProperty
    - 1、对observe的数据对象进行遍历，包括子属性对象的属性，都加上setter和getter。这样给该对象赋值的时候就会触发setter，就可以监听到数据变化了
    - 2、compile时解析模板指令，将模板中的变量替换成数据，初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，则更新视图
    - 3、Watcher订阅者是observe和compile之间通信的桥梁
        - 在自身实例化时往订阅器dep里面添加自己
        - 自身有一个update方法
        - 待属性变动，触发dep.notice通知时，调用自身的update函数，并触发compile绑定的回调
    - 4、mvvm作为数据绑定的入口，整合observe、compile和watcher三者，通过observe来监听自己的module数据变化，通过compile来解析编译模板指令
        - 最终利用watcher搭起observe和compile的桥梁，达到数据变化->视图更新、视图交互变化->数据module变更的双向绑定效果
- Vue不允许在已经创建的实例上动态添加新的跟级响应式属性
    - 但它可以使用Vue.set方法将响应式属性添加到嵌套的对象上
    - 还可以用vm.$set实例方法
- 向已有对象上添加一些属性，例如使用Object.assign或_.extend方法来添加属性
    - 添加到对象上的新属性不会触发更新
    - 在这种情况下，可以创建一个新的对象让他包含原对象的属性和新的属性
    ``` JavaScript
        this.obj = Object.assign({}, this.obj, { a: 1, b: 2 });
    ```
- [为什么data是返回函数而非对象](https://cn.vuejs.org/v2/guide/components.html#data-%E5%BF%85%E9%A1%BB%E6%98%AF%E4%B8%80%E4%B8%AA%E5%87%BD%E6%95%B0)
    - 函数作用域
    - 组件是通过Vue.component全局注册的，可以用在其注册之后的任何新创建的Vue根实例
        - 若data是对象，则会有数据之间的命名冲突等问题
        - data是一个函数后，每个组件实例有自己的作用域，实例之间相互独立互不影响

## 虚拟dom
- 虚拟dom是js对象，操作更高效
    - vue的diff算法(基于snabbdom改造)是在同级vNode间比较，递归的进行同级vNode的diff，最终实现整个dom树的更新
    - 判断同一节点：key相同、tag相同、data(当前节点的对象，包含具体的数据信息)一致、标签是input时type相同
- [参考1](https://cn.vuejs.org/v2/guide/render-function.html#%E8%8A%82%E7%82%B9%E3%80%81%E6%A0%91%E4%BB%A5%E5%8F%8A%E8%99%9A%E6%8B%9F-DOM)
- [参考2](https://github.com/answershuto/learnVue/blob/master/docs/VirtualDOM%E4%B8%8Ediff(Vue%E5%AE%9E%E7%8E%B0).MarkDown)

## vue的template编译的原理
- 先把模板转化成AST树，之后render函数返回VNode(Vue-virtual Node)
- 首先，通过compile编译器把template编译成AST(Abstract Syntax Tree抽象语法树)
- compile是createElement的返回值，createElement是用于创建编译器
- 然后AST通过generate得到render函数，render的返回值是vNode

## event & v-model 实现原理
- v-model原理
- 传入原先的props，使用临时变量标记this，然后监听input的输入事件，并将输入值返回传给原先的值并修改
- 通过绑定原先值的value，并监听
- code
    ``` JavaScript
        props: ["v-model"],
        render: function(h) {
            let self = this;
            return h('input', {
                domProps: {// 初始化值
                    value: self['v-model']
                },
                on: {
                    input: function(evt) {// 此处为event
                        self.emit('input', event.target.value); // 自定义回调函数
                    }
                }
            })
        }
    ```

## slot & keep-alive 实现原理

## transition 过渡的实现原理

## vue-router 路由的实现原理

## vuex 状态管理的实现原理

## 参考
- [juejin.vue面试](https://juejin.im/post/5b19e81de51d454e907bd1c5)