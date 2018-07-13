---
title: hexo写blog
date: 2018-07-10 16:14:07
tags: js
---

## why hexo
- jekyll还要安装ruby
- hexo
    - 可以有建站工具hexo-cli

## 开始搭建
- 配置文件
    - _config.yml
- 选择主题
    - _config.yml=> theme: cactus-white # landscape
    - 下载对应主题文件
- 跑起来
    - hexo g -w
    - hexo s
- 只显示一部分文章，但是已经打包成功
    - show_all_posts: false

## 打包上线
- git
    - 怎么进行发布，设置各种属性
        - hexo clean
        - hexo d
        - 设置
        ``` JavaScript
            type: git
            repo: git@github.com:hhjay/hhjay.github.io.git
            branch: deploy # 部署分支
            message: # 上传文案
        ```
    - 发布和主分支冲突
        - 利用发布分支
        - 还在寻找更好的解决方案，怎样把发布分支切到对应的发布分支呢
