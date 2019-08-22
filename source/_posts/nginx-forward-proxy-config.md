---
title: "Nginx正向代理配置"
description: "Nginx Forward Proxy Config"
date: "2018-08-17T11:20:19+08:00"
thumbnail: ""
categories:
  - "Nginx"
tags:
  - "CS"
  - "Nginx"
---

Nginx不仅可以做反向代理，实现负载均衡。还能用作正向代理来进行上网等功能。

正向代理：如果把局域网外的Internet想象成一个巨大的资源库，局域网中的客户端要访问Internet，则需要通过代理服务器来访问，这种代理服务就称为正向代理。
<!--more-->

## 配置代理
```

server {  
    resolver 114.114.114.114;       #指定DNS服务器IP地址  
    listen 80;
    location / {  
        proxy_pass http://$http_host$request_uri;     #设定代理服务器的协议和地址  
                proxy_set_header HOST $http_host;
                proxy_buffers 256 4k;
                proxy_max_temp_file_size 0k; 
                proxy_connect_timeout 30;
                proxy_send_timeout 60;
                proxy_read_timeout 60;
                proxy_next_upstream error timeout invalid_header http_502;
    }  
}

server {  
    resolver 114.114.114.114;       #指定DNS服务器IP地址  
    listen 443;  
    location / {  
       proxy_pass https://$host$request_uri;    #设定代理服务器的协议和地址  
             proxy_buffers 256 4k;
             proxy_max_temp_file_size 0k; 
       proxy_connect_timeout 30;
       proxy_send_timeout 60;
       proxy_read_timeout 60;
       proxy_next_upstream error timeout invalid_header http_502;
    }  
}  
```
配置两个SERVER节点，一个处理HTTP转发，另一个处理HTTPS转发，而客户端都通过HTTP来访问代理，通过访问代理不同的端口，来区分HTTP和HTTPS请求。

## 加载配置
```
nginx -s reload
```

## 测试访问
```
server {   
    resolver 114.114.114.114;       #指定DNS服务器IP地址  
    listen 8000;  
    location / {
        proxy_pass http://$http_host$request_uri;     #设定代理服务器的协议和地址  
    }   
} 
```
在本地的Nginx设置了一个通过8000端口的http代理。用代理访问淘宝，不过被重定向了。
```
➜  curl -l --proxy 127.0.0.1:8000 http://www.taobao.com/   
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html>
<head><title>302 Found</title></head>
<body bgcolor="white">
<h1>302 Found</h1>
<p>The requested resource resides temporarily under a different URI.</p>
<hr/>Powered by Tengine</body>
</html>
```

试试访问百度，可以的呐。
```
➜ curl -l --proxy 127.0.0.1:8000 "www.baidu.com"
<!DOCTYPE html>
<!--STATUS OK--><html> <head><meta http-equiv=content-type content=text/html;charset=utf-8><meta http-equiv=X-UA-Compatible content=IE=Edge><meta content=always name=referrer><link rel=stylesheet type=text/css href=http://s1.bdstatic.com/r/www/cache/bdorz/baidu.min.css><title>百度一下，你就知道</title></head> <body link=#0000cc> <div id=wrapper> <div id=head> <div class=head_wrapper> <div class=s_form> <div class=s_form_wrapper> <div id=lg> <img hidefocus=true src=//www.baidu.com/img/bd_logo1.png width=270 height=129> </div> <form id=form name=f action=//www.baidu.com/s class=fm> <input type=hidden name=bdorz_come value=1> <input type=hidden name=ie value=utf-8> <input type=hidden name=f value=8> <input type=hidden name=rsv_bp value=1> <input type=hidden name=rsv_idx value=1> <input type=hidden name=tn value=baidu><span class="bg s_ipt_wr"><input id=kw name=wd class=s_ipt value maxlength=255 autocomplete=off autofocus></span><span class="bg s_btn_wr"><input type=submit id=su value=百度一下 class="bg s_btn"></span> </form> </div> </div> <div id=u1> <a href=http://news.baidu.com name=tj_trnews class=mnav>新闻</a> <a href=http://www.hao123.com name=tj_trhao123 class=mnav>hao123</a> <a href=http://map.baidu.com name=tj_trmap class=mnav>地图</a> <a href=http://v.baidu.com name=tj_trvideo class=mnav>视频</a> <a href=http://tieba.baidu.com name=tj_trtieba class=mnav>贴吧</a> <noscript> <a href=http://www.baidu.com/bdorz/login.gif?login&amp;tpl=mn&amp;u=http%3A%2F%2Fwww.baidu.com%2f%3fbdorz_come%3d1 name=tj_login class=lb>登录</a> </noscript> <script>document.write('<a href="http://www.baidu.com/bdorz/login.gif?login&tpl=mn&u='+ encodeURIComponent(window.location.href+ (window.location.search === "" ? "?" : "&")+ "bdorz_come=1")+ '" name="tj_login" class="lb">登录</a>');</script> <a href=//www.baidu.com/more/ name=tj_briicon class=bri style="display: block;">更多产品</a> </div> </div> </div> <div id=ftCon> <div id=ftConw> <p id=lh> <a href=http://home.baidu.com>关于百度</a> <a href=http://ir.baidu.com>About Baidu</a> </p> <p id=cp>&copy;2017&nbsp;Baidu&nbsp;<a href=http://www.baidu.com/duty/>使用百度前必读</a>&nbsp; <a href=http://jianyi.baidu.com/ class=cp-feedback>意见反馈</a>&nbsp;京ICP证030173号&nbsp; <img src=//www.baidu.com/img/gs.gif> </p> </div> </div> </div> </body> </html>
```

## 参考
- [深入理解Nginx](http://lockshell.com)

