---
title: 边框渐变和圆角不兼容的解决办法
date: 2018-05-31 14:03:01
tags: css
---

## 概要
- border-radius
    - 是用来设置边框圆角的
    - 即使元素没有边框，具体效果受 background-clip 影响
- linear-gradient()
    - 该函数用于创建一个表示两种或多种颜色（线性）渐变的图片，其结果属于< gradient>数据结构，一种特别的< image>数据结构
    - 属性
        - linear-gradient(
            angel(角度) | to left/right/top/bottom起始点位置,
            color start, color stop(渲染的颜色)
            )
        - 渐变线的起始点位置
        - 渐变的方向
        - 渐变的颜色渲染
    - test
    ``` css
        // 起始位置 起止位置
        background: linear-gradient(to right, red, orange);
        // 渐变角度 起止位置
        background: linear-gradient(135deg, red, blue);
        // 渐变角度 起止位置(10%代表red占10%的大小)
        background: linear-gradient(135deg, red 10%, blue);
    ```
- border-image
    - 允许在元素的边框下绘制图像
    - 使用该属性时，将会替换掉border-style属性所设置的边框样式
    - 属性
        - source
        - slice
        - img height
        - img width
        - outse
        - repeat

## 外部添加border-radius
- border-image添加渐变
``` css
.border {
    width: 100px;
    height: 38px;
    background: #6CF;
    border: 3px solid #F33;
    border-image: linear-gradient(to top, red, orange, yellow) 6;
}
```

## 外部背景添加渐变
- background添加渐变
``` css
    .test-box {
        position: relative;
        border: 1px solid transparent;
        border-radius: 5px;
        background: linear-gradient(white, white);
        background-clip: padding-box;
        padding: 10px;
        box-shadow: 0 3px 9px black, inset 0 0 9px white;
        &::before {
            position: absolute;
            top: -1px;
            bottom: -2px;
            left: -1px;
            right: -1px;
            background: linear-gradient(#34acb6, #34acb6);
            content: '';
            z-index: -1;
            border-radius: 5px;
        }
    }
```