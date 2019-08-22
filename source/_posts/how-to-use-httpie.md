---
title: "Httpie超赞的http客户端"
description: "How to Use Httpie"
date: "2019-08-18T15:34:15+08:00"
thumbnail: ""
categories:
  - "开发工具"
tags:
  - "Linux"
  - "Tools"
---

`Httpie`是一个人性化的HTTP的命令行客户端，`httpie`之于`curl`，有点类似`requests`之于`urllib`，用起来更方便。

> HTTPie (pronounced aitch-tee-tee-pie) is a cURL-like, modern, user-friendly, and cross-platform command line HTTP client written in Python. 
It is designed to make CLI interaction with web services easy and as user-friendly as possible.

## 主要特性
- 格式化终端输出
- 内置 JSON 支持
- 支持上传表单和文件
- HTTPS、代理和认证
- 任意请求数据
- 自定义头部
- 持久性会话
- 类 Wget 下载
- 支持 Python 2.6, 2.7 和 3.x
- 支持 Linux, Mac OS X 和 Windows

## 安装和使用
```
brew reinstall httpie  # On Mac 
apt-get install httpie  # On Debian/Ubuntu
```

### 基本操作
```
usage: http [--json] [--form] [--pretty {all,colors,format,none}]
            [--style STYLE] [--print WHAT] [--headers] [--body] [--verbose]
            [--all] [--history-print WHAT] [--stream] [--output FILE]
            [--download] [--continue]
            [--session SESSION_NAME_OR_PATH | --session-read-only SESSION_NAME_OR_PATH]
            [--auth USER[:PASS]] [--auth-type {basic,digest}]
            [--proxy PROTOCOL:PROXY_URL] [--follow]
            [--max-redirects MAX_REDIRECTS] [--timeout SECONDS]
            [--check-status] [--verify VERIFY]
            [--ssl {ssl2.3,tls1,tls1.1,tls1.2}] [--cert CERT]
            [--cert-key CERT_KEY] [--ignore-stdin] [--help] [--version]
            [--traceback] [--default-scheme DEFAULT_SCHEME] [--debug]
            [METHOD] URL [REQUEST_ITEM [REQUEST_ITEM ...]]
```

### GET访问
```
 http http://baidu.com 
```

```             
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: max-age=86400
Connection: Keep-Alive
Content-Length: 81
Content-Type: text/html
Date: Sun, 18 Aug 2019 07:41:11 GMT
ETag: "51-47cf7e6ee8400"
Expires: Mon, 19 Aug 2019 07:41:11 GMT
Last-Modified: Tue, 12 Jan 2010 13:48:00 GMT
Server: Apache

<html>
<meta http-equiv="refresh" content="0;url=http://www.baidu.com/">
</html>
```

### 上传文件
```
http https://lockshell.com < file.txt
```

### 下载文件
```
http --download https://lockhell.com/file.txt < file.txt
```

### 提交表单
```
http --form POST lockshell.com date='Hello World'
```

### 认证
```
http -a username:password http://lockshell.com/admin/
```

### 设置Headers
```
http GET https://httpbin.org/headers User-Agent:'TEST 1.0'
```

### 使用http代理
```
http --proxy=http:http://192.168.0.1:8081 proxy.lockshell.com
```
