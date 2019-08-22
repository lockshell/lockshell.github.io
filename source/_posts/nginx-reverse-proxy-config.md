---
title: "Nginx反向代理配置"
description: "Nginx Reverse Proxy Config"
date: "2018-02-12T11:03:42+08:00"
thumbnail: ""
categories:
  - "Nginx"
tags:
  - "CS"
  - "Nginx"
---

## Nginx反向代理
Nginx是一个轻量级的、高性能的WebServer，主要可以干下面两件事：作为http服务器（和apache的功能一样）；作为反向代理服务器实现负载均衡。
<!--more-->

### 安装Nginx
Mac上执行
```
brew install nginx
```
Ubuntu上执行：
```
sudo apt-get install nginx 
```

### Nginx基本操作
```
1) 启动Nginx：start nginx
2) 停止Nginx：nginx -s stop
3) 修改配置后重启：nginx -s reload
```

## 关于代理
### 正向代理
正向代理，作为一个媒介将互联网上获取的资源返回给相关联的客户端。代理和客户端在一个局域网，对于服务端是透明的

### 反向代理
反向代理，根据客户端的请求，从后端的服务器上获取资源，然后再将这些资源返回给客户端。代理和服务器在一个局域网，对客户端是透明的。

### 反向代理的作用
- 提高动态语言的I/O处理能力，Python、PHP、Java这样的动态服务的I/O处理能力不高，反向代理可以缓冲请求，交给后端一个完整的HTTP请求，同样，Nginx也可以缓冲响应，也达到了减轻后端的压力。   
- 加密和SSL加速。   
- 安全。它保护和隐藏了原始资源服务器，还可以用作应用防火墙防御一些网络攻击，比如DDoS。   
- 负载均衡。它帮应用服务器分配请求，以达到资源使用率最佳、吞吐率最大、响应时间最小的目的。 
- 缓存静态内容。代理缓存通常可以满足相当数量的网站请求，大大降低应用服务器上的负载。   
- 支持压缩。通过压缩优化可以提高网站访问速度，还能大大减少带宽的消耗。

在生产环境中，通常会在多个服务器启动多个tornado进程实例，使用Nginx在前端作为反向代理服务器来分发web请求，同时负载均衡。

## 反向代理实例
### tornado服务`demo.py`
```
# coding: utf-8
import tornado.ioloop
import tornado.web
from multiprocessing import Pool
import sys
import os


class MainHandler(tornado.web.RequestHandler):
    def get(self):
        self.write("Hello, world! PID: %s" % os.getpid())

application = tornado.web.Application([
    (r"/", MainHandler),
])

if __name__ == "__main__":
    def run(port):
        print 'Start Process on port: %s' % port
        sys.stdout.flush()
        application.listen(port)
        tornado.ioloop.IOLoop.instance().start()

    pool = Pool(3)
    pool.map(run, [8001, 8002, 8003])
```
我们运行`demo.py`，tornado会启动三个进程，分别侦听8001, 8002, 8003三个端口。

### 调整Nginx配置
负载均衡的目的是为了解决单个节点压力过大，造成Web服务响应过慢，严重的情况下导致服务瘫痪，无法正常提供服务的问题。
Nginx负载均衡是通过upstream模块来实现的，内置实现了多种负载策略。Mac上Nginx的配置文件位于`/usr/local/etc/nginx`，用vim打开进行编辑。

#### 负载均衡配置
```
upstream tornado.server {
   server 127.0.0.1:8001;
   server 127.0.0.1:8002;
   server 127.0.0.1:8003;
}
```
upstream指令主要用于负载均衡，设置一系列的后端服务器。nginx 的 upstream默认是以轮询的方式实现负载均衡，这种方式中，每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。此外还有ip_hash、weight、url_hash、fair等负载均衡策略。
upstream命名和服务器地址根据实际情况修改。我这里是本地起的三个tornado服务，所以server IP地址都配的是127.0.0.1，默认轮询的负载均衡。

#### 反向代理配置
```
location / {
       proxy_pass_header Server;
       proxy_set_header Host $http_host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Scheme $scheme;
       proxy_pass http://tornado.server;
    }
```
location部分用于匹配反向代理的网页位置。反向代理（Reverse Proxy）方式是指以代理服务器来接受internet上的连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个反向代理服务器。

### 完整配置示例
```

worker_processes  1;

events {
    worker_connections  1024;
    use kqueue;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    # 负载均衡配置
    upstream tornado.server {
        server 127.0.0.1:8001;
        server 127.0.0.1:8002;
        server 127.0.0.1:8003;
    }

    sendfile        on;
    keepalive_timeout  65;

    server {
        listen       80;
        server_name  localhost;
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # 反向代理配置
        location / {
            proxy_pass_header Server;
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Scheme $scheme;
            proxy_pass http://tornado.server;
        }
    }
}

```
代理地址根据实际情况修改，其他缺省配置项采用默认值就可以。

### 重新加载ginx.conf
如果已经启动了Nginx，执行`sudo nginx -s reload`重新加载配置。

### 访问结果
直接在浏览器中访问`http://127.0.0.1/`，就可以访问demo应用了。每次刷新都返回了`Hello, world! PID：18854`，后面跟的pid是交替出现，说明负载均衡生效了。

## 参考
- [Python Web开发实战 董伟明](http://lockshell.com)
- [深入理解Nginx](http://lockshell.com)

