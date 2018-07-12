---
title: undefined-null的区别
date: 2018-03-28 11:09:32
tags: js
---

## undefined
- Undefined是一个数据结构
- 继承至Null
- 表示一个“无”的原始值（初始值）
- 产生undefined值的
    ```js
        var x;              // 声明变量未赋值
        function f(x) {     // 调用函数时参数未提供
            console.log(x);
        }
        var x = new Object(); console.log(x.p); // 对象未赋值的属性
        var x = f();        // 函数无返回值
    ```

## null
- 表示一个没有任何引用的空对象（空对象指针） .

## NaN
- Not a Number
- NaN与所有的值都不相等，包括它自己
- 可用isNaN函数来判断

## undefined和null的区别
- 类型不同
    ```js
        typeof null;      // object
        typeof undefined; // undefined
        null == undefined;  // true
        null === undefined; // false
    ```
- undefined不是有效的JSON值，null是
    ```js
        JSON.stringify({a: undefined, b: 1}); // "{"b":1}"
        JSON.stringify({a: null, b: 1})       // "{"a":null,"b":1}"
    ```

## 参考链接
- [阮一峰](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null)
- [css88](http://www.css88.com/archives/6236)
