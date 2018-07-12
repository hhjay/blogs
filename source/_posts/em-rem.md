---
title: em与rem的区别及各种长度单位的关系
date: 2018-03-29 13:40:53
tags: css
---

## px(pixel像素)
- 现代浏览器都支持
- 相对于显示器屏幕分辨率确定
- 屏幕放大缩小的时候不会随着屏幕一起变化

## em(font size of the element)
- 现代浏览器都支持
- 相对于当前对象内文本的字体大小，如当前相对字体大小未设置，则相对于浏览器的默认字体大小
- em值是不确定的
- 会继承父级元素的字体大小
- 浏览器默认的字体高都是16px，若未手动设置则1em = 16px

## rem(font size of the root element)
- 兼容ie9+
- 相对于根节点的大小
- root em，相对于根节点< html>的字体大小，若根节点未手动设置大小，则是浏览器的默认大小，一般为1rem = 16px
- 使用该单位在媒体查询时可以只设置根节点的大小来控制页面，适用于网格布局
- 可通过设置viewport进行缩放
    ```html
    <!-- 可实现在320的时候以1.3倍，416的时候刚好1 -->
    <meta name="viewport" content="width=320,maximum-scale=1.3,user-scalable=no">
    ```
- 若设置了绝对的大小，则该rem会失效(不支持rem的，支持的会按照css正常规则即优先级原则)
    ```css
    p {
        font-size: 12px;
        font-size: .8rem;
    }
    ```

## em与px区别
- px大小确定，em可以随着屏幕放大缩小变化

## em与rem区别
- em继承至父级元素，rem是继承至根节点

## vw / vh
- Viewport units（视口单位）
- 响应式页面布局技术很大程度依赖于比例规则，该单位相对于视图窗口的大小
- 1vh = 1/100 vierport height; 1vw = 1/100 vierport width，这里面的高度和宽度指的是可视区域的大小，即window.innerHeight及window.innerWidth
- vmin / vmax
    - vmin和vmax取决于高度和宽度的最大最小值
    - 例如浏览器高度1023px、宽度960px，则vmin是960px、vmax是1024px
    - 例如浏览器高度860px、宽度960px，则vmin是860px、vmax是960px

## pt

## ex / ch

## 参考链接
- [caibaojian.rem是如何实现自适应布局的](http://caibaojian.com/web-app-rem.html)
- [caibaojian.rem与em的使用和区别详解](http://caibaojian.com/rem-vs-em.html)
- [runoob.px、em、rem区别介绍](http://www.runoob.com/w3cnote/px-em-rem-different.html)