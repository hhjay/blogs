---
title: vue1.x 与 vue2.x的区别
date: 2018-06-05 13:50:50
tags: js
---

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
- 在vue2中增加了虚拟dom

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