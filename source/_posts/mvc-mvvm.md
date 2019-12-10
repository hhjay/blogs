---
title: mvc 和 mvvm的区别
date: 2019-06-24 15:50:38
tags: css
---

## MVC
- Model：数据层，负责存储数据
- View：视图层，展示用户看到的界面
- Control：控制器，协调层，负责协调Model和View，根据用户在View层的动作做出的对应的更改反馈给Model层，同时将修改的信息返回到View层

## MVVM
- Model：数据层，负责跟数据相关的更改
- View：视图层，负责从ViewModel层获取数据，然后显示
- ViewModel：视图模型，封装业务逻辑、数据缓存，将原先ViewControl层的业务逻辑等剖离出来放到ViewModel层

## 参考
- [https://zhuanlan.zhihu.com/p/60832562](知乎)