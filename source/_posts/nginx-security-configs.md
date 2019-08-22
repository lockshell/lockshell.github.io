---
title: "Nginx安全相关配置"
description: "Nginx Security Configurations"
date: "2019-08-12T15:35:37+08:00"
thumbnail: ""
categories:
  - "Nginx"
tags:
  - "Nginx"
---

A summary of Nginx security configuration.
<!--more-->

### Limit connections
```
http {
    limit_conn_zone $binary_remote_addr zone=zclient:10m;
    limit_conn_zone $server_name zone=zserver:10m;

    server {
        listen       80;
        server_name  lockshell.com;

        root /home/project/webapp;
        index index.html;

        location / {
            limit_conn zclient 20; # 
            limit_conn zserver 1000; # 
        }

        access_log  /tmp/nginx_access.log  main;
    }
}
```
The ngx_http_limit_conn_module module can limit a IP's connections.

According to the config above, an IP can have 20 connections. 

The maximum connections number of the client is 20. 
Meanwhile, the maximum connections number of the server is 1000.


### Add user&passwd auth
```
server {
    location / {
        auth_basic "please input user&passwd";
        auth_basic_user_file key/auth.key;
    }
}
```


### Add blacklist or whitelist
```
location /admin/ {
    allow   192.168.1.0/24;
    deny    all;
}
```
Allow clients from 192.168.1.0/24 subnet to access.


### Limit request type
```
if ($request_method !~ ^(GET|POST)$ ) {
    return 405;
}
```
`$request_method` can get the method of requests to Nginx, the configuration only allows the GET/POST methods' access, other methods would return 405.


### Open Https
```
server {
    listen 443;
    server_name ops-coffee.cn;

    ssl on;
    ssl_certificate /etc/nginx/server.crt;
    ssl_certificate_key /etc/nginx/server.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         HIGH:!aNULL:!MD5;
}
```


### Hide version info
```
http {
    server_tokens off;
}
```
When there is security vulnerability in a version of the Nginx , hiding the nginx version info is one of the main security optimization ways, of course, the most important is to timely upgrade the vulnerability.


### Deny user-agent
```
if ($http_user_agent ~* LWP::Simple|BBBike|wget|curl) {
    return 444;
}
```
Somebody may use `curl` or `wget` to scan our website, We can simply prevent it by denying the corresponding user-agent.

Nginx's 444 state is special. If you return 444, the client will not receive the information returned by the server, just like the website can't connect.


### Picture anti-theft link
```
location /images/ {
    valid_referers none blocked www.lockshell.com lockshell.com;
    if ($invalid_referer) {
        return  403;
    }
}
```

### Set buffer size and timeout
```
client_body_buffer_size  1K;
client_header_buffer_size 1k;
client_max_body_size 1k;
large_client_header_buffers 2 1k;

client_body_timeout   10;
client_header_timeout 10;
keepalive_timeout     5 5;
send_timeout          10;
```


### Set Strict-Transport-Security
```
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";
```
It will tell the browser to use HTTPS instead of HTTP to access the target site.


### Set Content-Security-Policy
```
add_header Content-Security-Policy "default-src 'self'";
```
It defines what resources can be loaded on the page.


### Prevent XSS attack
```
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
add_header X-Content-Type-Options "nosniff";
```
