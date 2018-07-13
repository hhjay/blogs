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
    - 函数形式
        ``` JavaScript
            function quickSort(arr, start = 0, end = arr.length - 1) {
                // 开始位置比结束位置大 则终止
                if( start >= end ) return;

                let mid = arr[parseInt((start + end) / 2)]; // 正常使用第一个作为基准
                let left = start, right = end;
                while(left < right) {// 左右两端扫描
                    while( mid > arr[left] ) {// 找到比基准大的值（左边切换位置）
                        left++;
                    }

                    while( mid < arr[right] ) {// 寻找比基准小的值（右边切换位置）
                        right--;
                    }

                    // 找到左边比基准大的数、右边比基准小的数。进行交换
                    if( left <= right ) {
                        let temp = arr[left];
                        arr[left] = arr[right];
                        arr[right] = arr[left];

                        left++;
                        right--;
                    }
                }
                // 左边再排序
                if( start < left ) {
                    quickSort(arr, start, right);
                }
                // 右边再排序
                if( left < end ) {
                    quickSort(arr, left, end);
                }
                console.log(arr);
            }

            quickSort([1, 2, 1, 3, 7, 8, 4, 6, 5]);
        ```
    - 原型链
        ``` JavaScript
            Array.prototype.quickSort = function() {
                let len = this.length;
                if( len <= 1 ) return this.slice(0); // 长度不可分割的时候直接返回自身

                let left = [], right = [], mid = this[0]; // 分割为左右数组
                for(let i = 1; i < len; i++) {// 从基准值的下一个开始
                    if( this[i] < mid ) {
                        left.push(this[i]);
                    }else {
                        right.push(this[i]);
                    }
                }
                // 对左右数组递归的进行排序
                return left.quickSort().concat([mid].concat(right.quickSort()))
            }
        ```

## 选择排序
- 在未排序数组中找到最小（大）的元素，存放到排序序列的起始位置
- 重复上述操作
- 复杂度
    - 比较操作 O(n * (n - 1)  / 2)
    - 赋值操作 0 < < O(3 * (n -1))
- 代码
    - 函数
        ``` JavaScript
            function selectSort(arr) {
                let len = arr.length;
                for(let i = 0; i < len -1; i++) {
                    let max = i;
                    for(let j = i + 1; j <len; j++) {
                        if( arr[max] < arr[j] ) {
                            max = j;
                        }
                    }
                    let temp =arr[max];
                    arr[max] = arr[i];
                    arr[i] = temp;
                }

                console.log(arr)
            }
        ```
    - 原型链
        ``` JavaScript
            Array.prototype.selectSort = function() {
                let len = this.length;
                for(let i = 0; i < len; i++) {
                    let max = i;// 默认第一个为最大值
                    for(let j = i + 1; j < len; j++) {// 都跟未排序的数组相比较
                        if( this[max] < this[j] ) {
                            max = j;
                        }
                    }

                    let temp = this[max];
                    this[max] = this[i];
                    this[i] = temp;
                }
            }

        ```

## 插入排序
- 一种直观的排序算法
- 思路
    - 从第一个元素开始，并认定为已经被排序
    - 取出下一个元素，在已经排序的数组中从后向前扫描
    - 若该元素大于新元素，将元素移至下一位置
    - 重复上一步骤
    - 将新元素插入到该位置后
    - 重复判断
- 代码
    - 函数
        ``` JavaScript
            function insertSort(arr) {
                let len = arr.length;
                for(let i = 1; i < len; i++) {
                    let max = arr[i];
                    for(let j = i - 1; j >= 0 && max > arr[j]; j--) {
                        arr[j + 1] = arr[j];
                        arr[j] = max;
                    }
                }
                console.log(arr);
            }
        ```
    - 原型链
        ``` JavaScript
            Array.prototype.insertSort = function() {
                let len = this.length;
                for(let i = 0; i < len; i++) {
                    let max = this[i];
                    for(let j = i - 1; j >= 0 && max > this[j]; j--) {
                        this[j + 1] = this[j];
                        this[j] = max;
                    }
                }
            }
        ```

## 桶排序