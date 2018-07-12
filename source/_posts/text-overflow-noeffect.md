---
title: text-overflow不生效、注意事项
date: 2018-06-30 15:31:16
tags: css
---

## 默认用法
- text-overflow: clip | ellipsis
    - clip当对象内文本溢出时，直接将溢出的部分裁切掉
    - ellipsis当对象内文本溢出时，显示省略标记...

## 开始经常在使用text-overflow: ellipsis;不生效，没有出现...
- overflow: hidden;了解一下
    - 未使用该属性会全部显示
- 一行
    - 可以使用white-space: nowrap;强制不换行让其显示
- 多行
    - 设置n行，让对最后一行进行省略标记
    - box-orient规定框内的子元素被水平（horizontal）或垂直（vertical）排序
    - line-clamp限制多行文本
    - display: -webkit-box
    ``` html
        text-overflow: ellipsis;
        -webkit-line-clamp: 3;
        display: -webkit-box;
        line-height: 25px;
        -webkit-box-orient: vertical;
    ```