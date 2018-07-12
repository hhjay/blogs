---
title: python-crawler
date: 2018-05-10 16:38:25
tags: python
---

## python
- py2
- py3

## 爬虫
- urllib.request

## 中文乱码
- urllib2报错
    - python3把urllib2和urllib合并
    - 引入urllib.request
- gbk乱码报错
``` Python
    # UnicodeEncodeError: 'gbk' codec can't encode character '\u2003' in position 4763: illegal multibyte sequence
    # 解决办法：引入输出模块，改变标准输出的默认编码
    import io
    import sys
    sys.stdout = io.TextIOWrapper(sys.stdout.buffer,encoding='utf8')
```

## 参考链接
- [csdn.乱码解决](https://blog.csdn.net/jim7424994/article/details/22675759)
- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html)