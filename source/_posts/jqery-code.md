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
        ``` JavaScript
            // 节选
            jQuery.extend = jQuery.prototype.extend = function() {
                // 深度拷贝 递归合并纯数组或对象
                if ( deep && copy && ( jQuery.isPlainObject( copy ) ||
                    ( copyIsArray = Array.isArray( copy ) ) ) ) {

                    if ( copyIsArray ) {
                        copyIsArray = false;
                        clone = src && Array.isArray( src ) ? src : [];

                    } else {
                        clone = src && jQuery.isPlainObject( src ) ? src : {};
                    }

                    // 不改变源对象的情况下克隆
                    target[ name ] = jQuery.extend( deep, clone, copy );

                // 清除未定义的属性
                } else if ( copy !== undefined ) {
                    target[ name ] = copy;
                }
            }
        ```
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

## 选择器selector

## deferred ( $.Deferred )
- 是一个延迟对象，延迟到某个点才执行，改变状态的方法有resolve和reject，分别对应done和fail
- 他实现的promise方法
    - tuples
        - 定义[行为、添加监听、回调函数]
    - state
        - 执行状态，默认pendding
    - promise
        - state
        - always
        - catch
        - pipe
        - then

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