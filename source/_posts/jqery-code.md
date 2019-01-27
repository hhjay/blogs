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
- 原生ajax是什么
    - Async Javascript And Xml (异步js和xml)
    - 是用于创建快速动态网页的技术，可以再不重新加载整个网页的情况下，对网页的某部分进行更新
    - XmlHttpRequest & ActiveXObject( Ie5/6 )
        - xml.open("GET | POST", url, true | false) 
        ``` JavaScript
            // true异步请求，执行到这一步之后会继续往下执行，并不需要等待返回结果 
            // false同步请求，执行到这一步之后会等待返回结果再往下执行
        ```
        - setRequestHeader(header, value) ``` setRequestHeader("Content-type", "application/x-www-form-urlencoded") ```
        - xml.send() ，将请求发送至服务器
    - POST 与 GET 区别： POST无法使用缓存
    - onreadystatechange | readyState | status
        - readyState
            - 0 : 请求未初始化
            - 1 : 请求连接已建立
            - 2 : 请求已接收
            - 3 : 请求处理中
            - 4 : 请求已完成，且响应已就绪
- xhr
- script
- jsonp
- load

## offset

## exports
- amd
- global