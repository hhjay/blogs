---
title: 个人域名的搭建
date: 2018-07-05 10:22:30
tags: nginx
---

## 购买域名

## 购买服务器
- 阿里云、腾讯云.... 都是云
- ssh root@xx.xx.xx.xx
- winScp上传你的代码

## 域名解析
- 我在阿里云上面买的域名和主机，阿里云上面有DNS解析的，直接在[上面](https://dns.console.aliyun.com/#/dns/domainList)填写的解析域名
- 到这一步之后
    - bash
    ``` Bash
        ping xxxx.com
        
        来自 xx.xx.xx.xx 的回复: 字节=32 时间=45ms
        0%丢失
        // 所以是没有解析成功咯?
    ```

## 云服务安全组设置
- 需要在云服务 - 安全组 - 配置规则 - 添加安全组规则

## nginx配置
- 安装nginx
    - bash
    ``` Bash
        /* 更新apt-get 不然安装其他会报错
         * Unable to locate package nginx
         */
        apt-get update
        /* 安装nginx */
        apt-get install nginx
        /* 启动nginx */
        nginx
        /* 查看当前nginx是否启动 */
        ps -ef | grep nginx
        /* 平滑启动 */
        nginx -s reload
        /* 强制停止 */
        pkill -9 nginx
        /* 重启 */
        nginx -s reopen
        /* 停止 */
        nginx -s stop
        nginx -s quit
    ```
- 配置nginx
    - bash
    ``` Bash
        cd /etl/nginx/
        vi nginx.conf

        http {
            server {
                listen: 80;
                server_name h-aimee.com;
                root /home/homepage;
                location / {
                    index index.html index.php index.htm;
                }
            }
        }
    ```

## 紧张备案
- 填写各种信息
- 上传身份证
- 上传承诺书，在备案时可下载填写就好（尴尬，我上传自己手写的）
- 等待ing...