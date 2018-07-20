---
title: requireJs源码
date: 2018-07-18 11:12:30
tags: js
---

## 原来
- 通过< script>标签来加载对应的js文件，用全局变量来区分不同的功能代码，文件之间的依赖关系就需要通过文件的加载顺序来指定
- 监听readyState事件，动态的插入到head中script脚本
- 优点
    - 写法简单，不需要引入什么加载代码，小功能的开发快
- 存在问题
    - 变量命名之间会有冲突
    - 前端模块很多的时候，管理起来困难
    - 难以保证加载顺序、依赖关系难以处理
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
- 查找顺序（bar、bar.js、bar.json、bar.node、bar/package.json、bar/index.js、bar/index.json、bar/index.node）
- 找到对应的依赖文件（有些用模块id，但这样的话每次更新模块都要更新对应的id）
- 每个模块实例都有一个require方法，其实内部会调用module._load方法
    - 是否有缓存，有缓存取出缓存
    - 是否为内置模块
        - 如果是内置模块，直接返回模块（可避免重复加载）
    - 生成模块实例，存入缓存
    - 加载模块
    - 去除模块的export

## AMD规范和commonJs规范比较
- commonJs是服务端的规范，Nodejs采用了这个规范
    - 一个单独的文件就是一个模块
    - 加载文件使用require方法，该方法读取一个文件并执行，最后返回文件内部的export
    - 加载完成，才能执行后面的操作
- AMD则是非同步加载模块，允许指定回调函数

## 经典解读
``` JavaScript
    // 判断浏览器
    var isBrowser = !!(typeof window !== 'undefined' && typeof navigator !== 'undefined' && window.document);
    // 判断是否加载完成
    var readyRegExp = isBrowser && navigator.platform === 'PLAYSTATION 3' ?
                      /^complete$/ : /^(complete|loaded)$/;
    
    // 判断script是否加载完成
    onScriptLoad: function (evt) {
        // firefox 2.0需要currentTarget，旧浏览器srcElement
        if (evt.type === 'load' || (readyRegExp.test((evt.currentTarget || evt.srcElement).readyState))) {
            // 重置脚本，保证脚本不会保存太久
            interactiveScript = null;

            // 导出模块的名称和上下文
            var data = getScriptData(evt);
            context.completeLoad(data.id);
        }
    }

    // 创建对应的js script
    req.createNode = function (config, moduleName, url) {
        var node = config.xhtml ?
                document.createElementNS('http://www.w3.org/1999/xhtml', 'html:script') :
                document.createElement('script');
        node.type = config.scriptType || 'text/javascript';
        node.charset = 'utf-8';
        node.async = true;
        return node;
    };
```

## 参考
- [ibm.developer](https://www.ibm.com/developerworks/cn/web/1209_shiwei_requirejs/index.html)
- [github.HRFE](https://github.com/HRFE/blog/issues/10)