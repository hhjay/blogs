---
title: iyunxiao面试历程
date: 2018-07-11 17:18:17
tags: job
---

## 笔试
- 找到100以内的素数
    ``` JavaScript
        // 输入最大值
        function findPrimeN(max = 100) {
            let ret = [];
            for(let i = 2; i <= max; i++) {
                let isPrime = true;
                // 开方可少一半运算
                for(let j = 2; j <= Math.sqrt(i); j++) {
                    if( i % j == 0 ) {
                        isPrime = false;
                        break;
                    }
                }

                if( isPrime ) {
                    ret.push(i);
                }
            }
            
            console.log(ret);
        }
    ```
- 快速排序
- 找到二进制里面所有的1
    - 使用位元运算子 <<
        - a << b 将a的二进制形式向左移b bit位
        - a >> b 有符号右移，将a的二进制形式向右移，丢弃被移除的位
        - a >>> b 无符号右移，将a的二进制形式右移，丢弃被移除的位，并使用0在右侧填充
    ``` JavaScript
        function size_1(num) {
            let count = 0;
            while (num != 0) {
                let t = num << 1;
                if( t == 1 ) {
                    count++;
                }
            }
            console.log(count)
        }
        size_1(10010)
    ```
    - 字符化之后迭代查找

## 面试
- vue的双向绑定原理

## 感觉
- 面试十分钟，浪费时间