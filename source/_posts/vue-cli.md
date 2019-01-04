---
title: vue开发遇到的问题
date: 2018-12-24 10:35:30
tags: js
---

## 重新运行vue-cli3的项目会报错
- 装个全局的node-sass就好了

## vue-cli下，scss变量问题
- 向预处理Loader传递全局变量
- [方案](https://cli.vuejs.org/zh/guide/css.html#css-modules)

## ts下mixin不生效、$router等
- 使用全局变量需要在typings/vue-property.d.ts下声明全局方法
``` typeScript
    import Vue from "vue";
    declare module "vue/types/vue" {
        interface Vue {
            _proxy: any;
        }
    }
```

## elementUi中Autocomplete使用
- 加一个下拉菜单，例如筛选id和名字的（pm要我用代码识别???）
- 如何切换下拉菜单后可以直接对内容进行搜索并展示，刚开始直接调用对应的fetch-suggestions函数，但这样的话拿到的queryString和callback函数都是undefined
- 这时候我想到了添加一个函数记住原先存在的