---
title: vue1.x 与 vue2.x的区别
date: 2018-06-05 13:50:50
tags: js
---

## 为什么要升级到Vue2
- vue2新特性
    - 使用了基于snabbdom的virtual-dom对底层的渲染进行了重写
    - 对上层的编译做了优化处理，例如对重绘时减少了一些不必要的对比，即值重绘修改的部分子组件
    - 可手动写渲染函数，并提供jsx的babel
        - template + jsx都可以使用
    - 支持服务端渲染（ssr），流式+组件级的渲染
        - Vue 2.0 提供了内建的流式服务端渲染 - 在渲染组件时返回一个可读的 stream，然后直接 pipe 到 HTTP response
- vue-router新特性
    - 支持多命名的router-view
    - 可通过router-link进行导航功能
    - 自定义的滚动条行为
- vuex
    - 简化组件内的用法
    - 可聚合的异步action
- 饿了么也出了最新的elementUi组件库

## vue区别
- 父子组件双向响应变成单项数据传递
    - 可用$on / $emit
- 必须要有根元素
- compiled / ready使用mounted替代
    - ready 需要加nextTick
- v-for变化
    - v-for="(item, index) in Array"
    - v-for="(val, key, index) in Object"
    - track-by替换成key
    - 需要加key，否则会warning
- 添加computed 
- v-on / @ 在vue2.x下只会监听自定义事件，要监听原生的根元素事件，需要添加.native
    - @click
    - @click.native
- v-el / v-ref替换成ref
    - ref="testRef"
- v-show 后不能跟 v-else
- filter by / order by
    - filter by可用computed
    - sort排序
- slot
- keep-alive变成一个包裹组件，而不只是一个属性
- { { { html } } } 使用 v-html替换
- 在vue2中增加了虚拟dom（virtual DOM）
    - 当watcher被通知变动时，watcher会通知组件的render函数进行re-render操作，创建一个新的virtual DOM，跟旧的virtual DOM进行diff比较，得到一个最优的dom更新路径

## vuex
- $dispatch 和 $broadcast 替换
    - event bus
    - $emit / $on / $off 

## vue-router
- subRoutes 替换为 child
- redirect 从一个路由定义变成 url
    - router.redirect({ '/name': "/someurl" })
    - redirect: "some url"
- alias 也是从一个路由定义变成 string 或者 数组
- v-link指令 变换成 router-link组件
    - < a v-link="url"> => < router-link></ router-link>
- router.go 变换成 router.push()

## 参考链接
- [vue](https://cn.vuejs.org/v2/guide/migration.html)
- [vuex]()
- [vue-router](https://cn.vuejs.org/v2/guide/migration-vue-router.html)