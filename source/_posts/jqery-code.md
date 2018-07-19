---
title: jqery-code
date: 2018-07-19 10:12:48
tags: js
---

## 主模块core
- ready
- 基础函数
    - var变量模块
``` JavaScript
    // isFunction
    typeof obj === "function" && typeof obj.nodeType !== "number";
    // isWindow
    obj != null && obj === obj.window;
```
    - jquery.extend
    - ready
``` JavaScript
    // onload和readystate === "complete"区别
    // DOMContentLoaded IE9+
    // onreadystatechange IE6+
    // doscroll IE8-
    if ( document.readyState === "complete" ||
	    ( document.readyState !== "loading" && !document.documentElement.doScroll ) ){
            // 异步处理 准备脚本就绪
            window.setTimeout( jQuery.ready );
    } else {
        document.addEventListener( "DOMContentLoaded", completed );
        window.addEventListener( "load", completed );
    }
```
    - 

## 选择器selector

## deferred

## event

## css
- hiddenVisibleSelectors

## ajax
- xhr
- script
- jsonp
- load

## offset

## exports
- amd
- global