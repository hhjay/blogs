---
title: 常见排序算法
date: 2018-07-09 14:03:36
tags: js
---

## 冒泡排序
- 思路
    - 比较相邻的元素，如果第一个比第二个大，则交换他们两个
    - 对每一个相邻的元素做同样的操作，从开始第一对到最后一对
    - 对所有元素（除了最后一个）重复以上步骤
    - 一直比较，越小的元素会经由交换慢慢浮到数列的顶端，慢慢的把大（小）的值冒泡到后面
- 效率
    - O(n^2)
- 代码
``` JavaScript
    function bubbleSort(oldArr) {
        let len = oldArr.length;
        // 除了最后一个
        for(let i = 0; i < (len - 1); i++) {
            // 从开始第一对到最后一对
            for(let j = 0; j < (len - 1 - i); j++) {
                // 相邻元素比较
                if( oldArr[j] > oldArr[j + 1] ) {
                    // 交换位置
                    let temp = oldArr[j];
                    oldArr[j] = oldArr[j + 1];
                    oldArr[j + 1] = temp;
                }
            }
        }

        console.log(oldArr);
    }
```

## 快速排序（划分交换排序）
- 思路
    - 分治法，把一个序列分割成两个子序列
    - 从数组挑出一个元素，作为“基准”（需要比较的值）
    - 对数组进行重新排序，所有比基准小的元素放在基准前面，大的放后面；通过这一步操作，基准位于数组的中间位置
    - 递归的把小于和大于基准元素的子数组进行排序
    - 将数组进行分割成n*log n块进行比较
    - 通常要进行n * log n次排序，最坏情况下则需要n^2次
- 代码
``` JavaScript
    function quickSort(arr, start = 0, end = arr.length - 1) {
        // 开始位置比结束位置大 则终止
        if( start >= end ) return

        let mid = arr[parseInt((start + end) / 2)]; // 正常使用第一个作为基准
        let left = start + 1, right = end;
        while(left < right) {
            while( mid > arr[left] ) {
                left++;
            }

            while( mid < arr[right] ) {
                right--;
            }

            if( left <= right ) {
                let temp = arr[left];
                arr[left] = arr[right];
                arr[right] = arr[left];

                left++;
                right--;
            }
        }

        if( start < left ) {
            quickSort(arr, start, right);
        }
        if( left < end ) {
            quickSort(arr, left, end);
        }
    }
```

## 选择排序

## 插入排序

## 桶排序

## 