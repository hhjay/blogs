---
title: 表头不滚动，表格内容滚动
date: 2018-05-16 11:25:59
tags: css
---

## 方法1
- 使用div将表格分开，先显示表头，在将表体放入div中，设置div的css
- 动态插入表体的html
- iscroll用的该方法

## 方法2
- 设置表体的display为block，然后就可以直接overflow了
- 将表头设置为fix
- 有问题：表格对不上，需要强制给宽度那些
``` css
    thead, tbody tr {
        display: table;
        width: 100%;
        table-layout: fixed;
    }
    tbody {
        display: block;
    }
```