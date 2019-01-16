---
title: lazada电-面
date: 2019-01-08 15:03:21
tags: interview
---

## Es6中的static、public、super关键字
- static
    - 类(class)使用static定义静态方法
    - 调用静态方法不需要实例化该类，不能通过类实例调用静态方法（1、父级返回的this也不能调用；2、继承的也不能调用）
    - 用于创建工具函数
    ``` javaScript
        // 例子 ./_example/es-class.html
        class Animal {
            constructor(color, name) {
                this.color = color;
                this.name = name;

                console.log(`这是一只${ color }的${ name }`);
            }
            self() {// 返回自身，看看是否在此使用static
                return this;
            }
            static Run(a, b) {
                return `${ a.color }的${ a.name }在追 => ${ b.color }的${ b.name }`;
            }
        }
        const dog = new Animal('黄色', '狗');
        const pig = new Animal('黑色', '猪');
        const cat = new Animal('白猫', '猫');
        console.log( Animal.Run(dog, pig) );
        console.log(cat.Run(dog, pig)); // 会报错，因为静态方法不会被实例化，且不能被实例调用
        /*  不能调用的情况1 */
        let self = dog.self();
        console.log(self.Run); // undefind
        /* 不能调用的情况2 */
        class Dog1 extends Animal {};
        const _dog1 = new Dog1();
        console.log(_dog1.Run); // undefind
    ```

- super
    - 超类，用于调用对象的父对象上的函数（可以调用父对象上的静态函数）
    - 如果子类中存在构造函数，则需要在使用“this”之前首先调用 super()
    ``` javaScript
        
    ```

- extends
    - 请注意，类不能继承常规（非可构造）对象。如果要继承常规对象，可以改用Object.setPrototypeOf

## 箭头函数和普通函数区别

## 为什么升级Vue1 -> Vue2
- Vue2支持es6的语法
- Vue2的生态更好，可使用的
- Vue2减去了一些不常用的Api
- Vue2改动了一些底层的东西Virtual-Dom
- [更多](./vue1-vue2.md)

## 数组去重
- 1, '1'怎么去重

## 怎么设计一个Dialog组件
- 弹框分类
    - 信息提示：区分为有无关闭按钮，自动关闭
    - 信息确认：提示用户，给关闭按钮
    - 对话框：关闭和确认或者其他按钮
    - 自定义对话框：自定义弹框里面的内容
- 创建一个模态框遮罩层，会先对页面上是否有弹框进行检验，一般是基于body
- 定义一个fixed的结构，再子元素定义弹框的基本结构，并默认居中于刚刚的相对于浏览器窗口的父元素
    - 弹框头部内容：标题、关闭icon
    - 弹框主题内容：自定义内容、样式
    - 弹框底部按钮：确认、关闭按钮或者其他
- 接收传进来的消息、弹框样式以及其他自定义内容
- 弹框变化给予响应的回调函数

## 跨域方法
- jsonp怎么来
- cors

## 双向绑定原理
- 怎么实现一个双向绑定

## 拖拽事件怎么来，对一个dom元素[js高级程序设计22章5.1]
- 基本概念：创建一个绝对定位的元素，使其可以用鼠标移动（鼠标拖尾）
- 鼠标按下，计算鼠标在当前元素的位置
- 设置一个onmousemove事件处理程序，将指定元素移动到鼠标指针的位置
- 并在鼠标释放的时候删除该元素

## 页面优化方法

## 事件委托
- 子元素和父元素都绑定了一个点击函数，点击子元素会怎么触发
- [example](./_example/dom-bubbling.html)

## csrs怎么来，防御

## node怎么寻找到对应的模块