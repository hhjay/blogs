---
title: 闭包
date: 2018-04-19 10:14:23
tags: js
---

## 闭包（词法闭包、函数闭包）
- 是引用了自由变量的函数
- 闭包是有权访问另一作用域中变量的函数
- 从实践角度来看
    - 即使创建它的上下文已经销毁，它依然存在（eg内部函数从父函数中返回）
    - 在代码中引用了自由变量
- 自由变量：指在函数中使用的，但既不是函数参数也不是函数的局部变量
```JavaScript
    var gl = "global var"; // 全局上下文
    function csA() {
        var gl = "local var"; // 函数内的上下文
        function csB() {
            return gl;
        }

        return csB;
    }

    var foo = csA(); // 函数上下文已销毁，理论上此时内部的gl变量也被销毁了
    foo(); // local var
```
- 用途
    - 读取函数内部的变量
    - 让这些变量值始终保持在内存中，记录变量
    ``` JavaScript
        function add(x) {
            var sum = x;
            var tmp = function(y) {
                return sum + y;
            }
            return tmp;
        }

        add(2)(5);
    ```
    - 私有变量，访问控制
    ```JavaScript
        var o = (function() {
            var a = 111, b = 222;
            return {
                foo: function() {
                    console.log(a + b);
                    return b;
                }
            }
        })()
        
        o.foo() = 333;
        console.log(o.foo()) // 可以读取b的值，但是不能修改，达到了私有访问的目的
    ```
- 常见
    - 例子1
    ```JavaScript
        var a = [];
        for(var i = 0; i < 3; i++) {
            a[i] = function() {
                console.log(i);
            }
        }
        a[0](); // 3
        a[1](); // 3
        a[2](); // 3 在a[i] = ..时定义函数，未执行，最后在这里执行产生环境变量，故a[n]()指向的是i最后的值
    ```
    - 例子2
    ```JavaScript
        function A() {
            var i = 1;
            return function () {
                i++
                console.log(i);
            }
        }
        var a = A(); // a生成环境变量
        a(); // 2 未释放变量，一直加下去
        a(); // 3
        var b = A();
        b(); // 2
        b(); // 3
        a(); // 4
    ```

## 参考链接
- [wiki]<https://zh.wikipedia.org/wiki/%E9%97%AD%E5%8C%85_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)>
- [github](https://github.com/mqyqingfeng/Blog/issues/9)
- [知乎](https://www.zhihu.com/question/31840939)