---
title: localStorage、session和cookie的区别？
date: 2018-03-22 11:02:30
tags: js
---

## http
- Cookie是由HTTP服务器设置的，保存在浏览器中，但HTTP协议是一种无状态协议，在数据交换完毕后，服务器端和客户端的链接就会关闭，每次交换数据都需要建立新的链接。
- HTTP协议是一种无状态协议，在数据交换完毕后，服务器端和客户端的链接就会关闭，每次交换数据都需要建立新的链接。此时，服务器无法从链接上跟踪会话。cookie可以跟踪会话，弥补HTTP无状态协议的不足。

## session
- 定义
    - 会话控制，session是一次浏览器和服务器的交互的会话
    - 由服务器创建，以cookie的形式将sessionId传到客户端，并存在服务器的文本文件，设置了只能系统读写权限控制
- 用途
    - Session可以记录用户的登录与行为数据，即记录下用户目前访问服务器上的那些内容
    - 在用户执行刷新操作时，即再次访问服务器时，可以直接根据Session，打开用户上次访问时网页的状态
    - 它记录了用户在进入页面、查看结果、点击结果以及后继的操作（比如翻页、加购物车等）
- 运行过程
    - http请求一个页面时，如果用到session，会去读cookie中的sessionId是否有，如果没有则生成一个新的session
    ```php
        session_start();
        // 创建的session会保留这个sessionId，并将其以cookie的形式和客户端会话交流
        echo session_id();
        /**
        * 会根据session的相关配置将这些值存到文件里面，一般会包含这有sessionId的文件名
        * 内容: user|i:hhj
        */
        $_SESSION['user'] = 'hhj';
    ```
- cookie被禁用后怎么实现session
    - 若用户禁用cookie，可使用url参数形式传给后端验证
    - 表单隐藏字段，服务器自动修改字段，在提交的时候也把这个隐藏字段提交回服务端
- [参考](https://www.zhihu.com/question/19786827/answer/151015728)

## cookie
- Cookie就是由服务器发给客户端的特殊信息，而这些信息以文本文件的方式存放在客户端，然后客户端每次向服务器发送请求的时候都会带上这些特殊的信息。
- Cookie是由服务器发送出来以存贮在网络浏览器上，使得下次该访客再次回到服务器时，可以浏览验证该信息；是由Web服务器保存在用户浏览器（客户端）上的小文本文件，运行时存储在内存中
- 一个浏览器可创建的cookie数量最多为300多个，且每个不能超过4kb，每个站点能设置的cookie总数不能超过20个
- [防止Xss攻击](./safe-xss) 、 [参考](https://baike.baidu.com/item/cookie/1119?fr=aladdin#8)

## localStorage
- Web Storage API 提供了存储机制，通过该机制，浏览器可以安全地存储键值对，比使用 cookie 更加直观

## sessionStorage
- ...

## cookie / session 区别
- 都可以和服务端交互
- session是存在服务端的文本文件，cookie是存在客户端
- session依赖sessionId，而sessionId是存在cookie的，若客户端禁用了cookie，则session也会收到影响，不过可以通过url的方式传递sessionId

## cookie / localStorage 区别
- cookie可以与服务端交互、localStorage仅能在客户端进行交互
- cookie存储大小约为4k、localStorage可以存大约10M

## localStorage / sessionStorage 区别
- localStorage可以存永久数据、sessionStorage仅当会话结束就销毁数据

## 参考链接
- [csdn.cookie](http://blog.csdn.net/u014753892/article/details/52821268)
- [csdn.session](http://blog.csdn.net/hjc1984117/article/details/53995816)
- [知乎.cookie&session区别](https://www.zhihu.com/question/19786827)
- [百度百科.cookie](https://baike.baidu.com/item/cookie/1119?fr=aladdin)
- [博客园.cookie](https://www.cnblogs.com/andy-zhou/p/5360107.html#_caption_1)
- [mdn.localStorage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/localStorage)