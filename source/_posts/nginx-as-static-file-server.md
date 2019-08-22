---
title: "Nginx as Static File Server"
description: "Nginx静态文件服务配置"
date: "2018-02-12T11:31:48+08:00"
thumbnail: ""
categories:
  - "Nginx"
tags:
  - "CS"
  - "Nginx"
---

Nginx一大经典使用场景就是用来提供静态文件服务，例如图片、html、脚本、样式文件等，这些文件没有必要交给 tomcat、jboss等应用服务器处理，使用 Nginx 直接处理将大大提高性能。
用 Nginx 来提供静态文件服务十分简单，只需要添加一个 server块指令即可。
<!--more-->

## 基本配置
假设我们的静态文件位于 `/Users/test` 目录下，文件服务基本配置如下：
```
    server {
        client_max_body_size 4G;
        listen  0.0.0.0:8888;  ## listen for ipv4; this line is default and implied
        server_name localhost;
        root /Users/test/;
        location / {
        }
    }
```
location指令用来映射请求到本地文件系统。
root 指令用来指定文件在服务器上的基路径。

## 配置索引
```
    server {
        client_max_body_size 4G;
        listen  8889;  ## listen for ipv4; this line is default and implied
        server_name localhost;
        root /Users/test;
        location / {
            autoindex on; 
            autoindex_exact_size on;
            autoindex_localtime on;
        } 
    }
```
执行`sudo nginx -s reload`重新加载配置。在浏览器中访问`http://127.0.0.1:8889/`，即可显示root指定的`/Users/test`目录下的内容。


## 设置密码
搭建文件服务器有时候不想让别人任意访问，想做成一个私有的该怎么办呢，这个时候我们可以用到nginx自带的认证模块。 需配置`auth_basic`和`auth_basic_user_file`字段。
```
    server {
        client_max_body_size 4G;
        listen  8890;  ## listen for ipv4; this line is default and implied
        server_name localhost;
        root /Users/test/;
        location / {
            auth_basic   "Restricted";
            auth_basic_user_file /usr/local/etc/nginx/pass_file;
            autoindex on;
            autoindex_exact_size on;
            autoindex_localtime on;
        }
    }
```

## 生成用户名和密码
```
htpasswd -c -d pass_file test
```
这样就在`/usr/local/etc/nginx/pass_file`文件中添加了一个用户。在访问`http://localhost:8890/`时，会弹窗提示输入用户名和密码进行验证，然后就可以正常访问了。

## 参考
- [深入理解Nginx](http://lockshell.com)
