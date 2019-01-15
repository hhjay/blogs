---
title: git-commitizen的规范
date: 2018-08-23 14:19:53
tags: git
---

## 很多commit不知道写什么好
- 时间紧
- 不知道写什么好、懒得写，但是这样的后果会导致后面的人不知道提交的内容都有哪些
- 

## git cz
- 对提交信息进行格式化，避免"test"、"aaa"、"..."等无效信息
- 方便后期查看，例如看fix就知道是单纯的bugfix、feat是功能开发、test是测试相关
- 可自定义输入
``` bash
    # npm
    npm install -g commitizen
    # yarn
    yarn global add commitizen
```

## [cz-conventional-changelog](https://github.com/conventional-changelog/conventional-changelog)
- 对输入的内容进行校验

## [cz-customizable](https://github.com/leonardoanalista/cz-customizable)
- 自定义cz选项及校验函数
- 添加cz-customizable
```bash 
    # 添加cz-customizable
    yarn add cz-customizable
 ```
- 添加（.cz-config.js）文件
- 修改package文件
``` json
    {
        "config": {
            "commitizen": {
                "path": "node_modules/cz-customizable"
            }
        }
    }
```
- 最后git cz就ok了

## 工程化

## 更多命令工具
``` bash
    # 迁移到新的路径1
    git remote set-url origin
    git push origin master

    # 迁移到新的路径2
    git remote remove origin
    git remote add origin [新路径]
    git push origin master
    #
```

## 参考链接
- [ruanyifeng](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)