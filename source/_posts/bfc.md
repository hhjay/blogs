---
title: bfc
date: 2018-03-21 17:41:37
tags: html
---

## BFC(Block Formatting Context)块级上下文

## 概念
- 是页面中的一块渲染区域，并且有一套渲染规则，决定了其子元素将如何定位，以及和其他元素的关系和相互关系。
- 盒模型: 一个页面由很多盒子构成构成，盒子和盒子之间会有各种相互关系，盒子里面的元素能否影响其他盒子呢
- 具有BFC特征的元素可以看作是隔离了的容器，容器里面的元素不会在布局上影响到外部布局，即可以把他比喻成一个盒子，盒子里面的元素无论怎么变化都不会影响到外部。

## 触发BFC的条件
- 浮动元素，float除none外
- 绝对定位元素，position: absolute || fixed
- display: inline-block || table-cells || table-captions
- overflow: hidden || scroll || auto

## 作用及原理
- 两栏布局
    - a、b会错位，解决办法：给b加overflow:hidden，触发BFC
    ```html
        <style>
            .a {
                float: left;
                width: 50px;
                height: 50px;
                border: 1px solid #4ec584;
            }
            .b {
                height: 100px;
                width: 100px;
                border: 1px solid #e14545;
                /*fix*/
                overflow: hidden;
            }
        </style>
        <div class="a"></div>
        <div class="b"></div>
    ```
    - a、b浮动，父元素高度塌陷；
    - 解决办法1：给父级元素添加overflow: hidden;触发BFC
    - 解决办法2：给父级元素after添加clear:both;display:table;
    ```html
        <style>
            .per {
                border: 1px solid #ccc;
                /*fix*/
                overflow: hidden;
            }
            .a {
                float: left;
                width: 50px;
                height: 50px;
                border: 1px solid #4ec584;
            }
        </style>
        <div class="per">
            <div class="a"></div>
            <div class="a"></div>
        </div>
    ```
    - margin重叠，会发现margin只有30px，少了20px；解决办法: 给b添加一个父级元素，并使该元素触发BFC，这样这两个div就不属于同一个BFC也就不会发生重叠了
    ```html
        <style>
            .a {
                width: 50px;
                height: 50px;
                border: 1px solid #4ec584;
                margin-bottom: 20px;
            }
            .b {
                height: 100px;
                width: 100px;
                border: 1px solid #e14545;
                margin-top: 30px;
            }
            /* 修改后 */
            .b1 {
                overflow: hidden;
            }
        </style>
        <div class="a"></div>
        <div class="b"></div>
        <!-- 修改后 -->
        <div class="a"></div>
        <div class="b"></div>
        <div class="b1">
            <div class="b"></div>
        </div>
    ```
## 参考链接
- [知乎专栏 . 有酒](https://zhuanlan.zhihu.com/p/25321647)
- [博客园](http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)