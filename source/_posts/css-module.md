---
title: css可以抽离出来的模块
date: 2018-08-21 11:19:29
tags: css
---

## 为什么要抽离
- 可以将业务和组件分开，这样后面维护的时候会很清晰，这样也好抽离共用的组件
- 

## 规范命名
- bem
    - block（块）、 例如menu、auth、logo、search、head
    - element（元素）、 例如span、button
    - modify（修饰符）、 例如size、
    - 总的可以为 menu-span__small、search-form__input

## 抽离的变量
- 关于颜色
- 关于固定的大小
- 路径
    - icon路径
    - 图片路径