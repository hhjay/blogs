---
title: vue开发遇到的问题
date: 2018-12-24 10:35:30
tags: js
---

## vue-cli下，scss变量问题
- 向预处理Loader传递全局变量
- [方案](https://cli.vuejs.org/zh/guide/css.html#css-modules)

## elementUi中Autocomplete使用
- 加一个下拉菜单，例如筛选id和名字的（pm要我用代码识别???）
- 如何切换下拉菜单后可以直接对内容进行搜索并展示，刚开始直接调用对应的fetch-suggestions函数，但这样的话拿到的queryString和callback函数都是undefined
- 这时候我想到了添加一个函数记住原先存在的