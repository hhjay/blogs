---
title: js继承
date: 2018-05-08 14:28:13
tags: js
---

## 对象
- 一切事物皆对象
- 对象具有封装和继承特性

## 原型链继承
- 对象（object）依赖类（class）来产生，而基于原型链的面向对象方向中，对象依赖构造器（constructor）利用原型链（prototype）构造出来的
- 被继承的属性和方法都放在prototype中
- 子继承者自己的属性和方法也放在自己的prototype
- 子继承者的prototype对象的__proto__属性指向被继承的prototype
```JavaScript
    class: { prototype: {} }
    |                   ^
    |                   |
    V                   |
    new class: {        |
        prototype: {    |
            __proto__: { }
        }
    }
    // 实例
    function Person(name, sex) {
        this.name = name;
        this.sex = sex;
    }
    Person.prototype.say = function() {
        return `my name is ${this.name}, and I am a ${this.sex}`;
    }
    var p1 = new Person("hhj", "man");
    p1.say();
```

## class继承

## 原型链和class继承的转换

## 链接
- [segmentfault](https://segmentfault.com/a/1190000008533435)
- [ruanyifeng](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001458267339633fd3a83c597d04b5fb59f7d1f6792efb3000)
- [github.norfish](https://github.com/norfish/blog/wiki/%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3JavaScrip%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E5%92%8C%E5%8E%9F%E5%9E%8B%E7%BB%A7%E6%89%BF)