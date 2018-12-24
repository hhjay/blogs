---
title: flex和grid布局的特效及区别
date: 2018-12-20 09:34:57
tags: css
---

## flex

## flex遇到的问题
### flex布局中设置子元素的宽度无效
- 
``` css
    .pr {
        display: flex;
        flex-flow: row;
    }
    .chi {
        width: 200px;/* 此处无效 */
        flex: 0 0 200px;/* 解决方案 */
    }
```

## frid

## flex及grid的区别