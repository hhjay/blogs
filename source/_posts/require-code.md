---
title: requireJs源码
date: 2018-07-18 11:12:30
tags: js
---

## 原来
- 通过< script>标签来加载对应的js文件，用全局变量来区分不同的功能代码，文件之间的依赖关系就需要通过文件的加载顺序来指定
- 优点
    - 写法简单，不需要引入什么加载代码，小功能的开发快
- 存在问题
    - 变量命名之间会有冲突
    - 前端模块很多的时候，管理起来困难
    - 依赖关系难以处理
    - 功能复用比较难

## require是什么
- requireJs是一个工具库，主要用于客户端的模块管理
- 让客户端的代码分成一个一个模块，实现异步或者同步加载，从而提高代码的性能和可维护性
- 通过define方法，将js代码封装进一个个模块，对全局对象的依赖变成对其他模块的依赖，避免一些命名冲突
- 通过延迟和按需加载来解决各个模块之间的依赖关系
- 优点
    - 解决全局变量命名冲突
    - 提高代码的复用性、可维护性
    - 非阻塞并发式加载js代码，使其不依赖页面的ui元素，图片、css及dom节点，得到更好的用户体验

## 怎么用
- 独立模块：直接define定义
``` JavaScript
    // 函数返回值即输出的模块
    define(function() {
        return {
            fn1: function() {
                // code
            },
            fn2: function() {
                // code
            }
        }
    })
    define(function() {
        fn1: function() {
            // code
        },
        fn2: function() {
            // code
        }
    })
```
- 非独立模块：define定义，有依赖关系
``` JavaScript
    // 依赖于jquery和head js文件
    define(["jquery.js", "js/head.js"], function($, head){
        return {
            fn1: function(idName) {
                return $("#"+ idName);
            },
            fn2: function(className) {
                return $("."+ className)
            }
        }
    }) 
```

## 源码基本结构

## 运行原理

## 参考
- [ibm.developer](https://www.ibm.com/developerworks/cn/web/1209_shiwei_requirejs/index.html)