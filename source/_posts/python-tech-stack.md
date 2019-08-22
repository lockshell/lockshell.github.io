---
title: "Python技术栈整理"
description: "Python tech stack and dev tools"
date: "2018-12-10T23:07:04+08:00"
thumbnail: ""
toc: false
categories:
  - "Python"
tags:
  - "Python"
  - "Tools"
---

## 开发环境

### 开发工具
- `Vim`/`SublimeText2`/`PyCharm`/`VS Code`<br>
用着顺手就好，我是由vim转PyCharm的。集成开发环境自动补全、单步调试等功能好很多，有利于提高工作效率。
- `iTerm`：Mac下必备，谁用谁知道
- `Tmux`：分屏工具，可以复用session，这点很赞
- `XShell`：远程登录
- `Sequel`：数据库登录
- `Postman`：HTTP接口调试工具

### 开发环境
- pip/easy_install 包管理
- viertualenv + virtualenvwrapper 库/版本管理，环境隔离
- ipython
- pydev


## 项目开发
### 代码管理
- `Git`：版本管理，SVN基本已经被淘汰
- `Gitlab`：大部分互联网公司都是搭建自己的Gitlab
- `Source Tree`：Git客户端，方便diff代码 管理分支
- `Jenkins`：持续集成

### Web框架
- `Django`：有些重，配置和约定众多，即可作为成熟的web框架，有可快速开发一些"管理"性质的后台
- `Flask`：轻量! 可以灵活组合各类组件进行开发(第三方组件很丰富)，简单高效，便于快速开发和维护
- `Tornado`：异步，高性能。<br>
Python Web框架也是超多，目前主流的就是这三个了；目前工作中用过的Django和Tornado。

### ORM
- `SQLAlchemy`：标配MySql ORM
- `PyMongo`：MongoDB ORM
- `peewe`：一个更轻量的ORM，简单了解，没在生产环境用过

### 数据库
- `MySql`：标配，关系型数据库
- `MongoDB`：NoSql数据库，不久前好像不开源最新版本了。
- `TiDB`：高拓展性，后起之秀

### 缓存Cache
- `Redis`：缓存/持久化/特殊需求(计数-排行榜-时间线等)，用`codis`做集群来访问
- `Memcached`：数据结构没有Redis丰富<br>
目前业务中这2个都有用到，感觉Redis有逐渐取代memcached的趋势

### 分布式存储
- `HDFS`：大数据分布式存储
- `Hive`：分析数据
- `HBase`：列数据库，可以存储海量数据，上10亿条不在话下，跟关系型数据库区别较大

### 消息队列
- `RabbitMQ`：Python中`pika`操作
- `celery`：分布式的异步任务处理器，配合`RabbitMQ`或`Redis`使用

## 项目测试
- 软件测试：单元测试，集成测试，压力测试等等；很多开发瞧不起测试，但是考虑周全的、高效的测试不容易
- 测试工具：请参考我整理的[Python 测试工具](https://lockshell.com/posts/python-test-tools/)<br>


## 项目运维
### 服务部署
- `Nginx`：主要用于负载均衡，反向代理，使用极为广泛
- `uWSGI`：用来部署Django项目
- `Gunicorn`：a Python WSGI HTTP Server，用来运行Django/Flask项目

### 日志&监控
- `Kibana`：`ElasticSearch`可视化平台，方便查log
- `Falcon`：小米开源的监控系统
- `grafana`：可视化的监控平台

### 运维管理
- `SaltStack`：别名，盐栈。自动化运维工具
- `Fabric`：用于自动化部署
- `Supervisor`：A Process Control System，配置管理各种程序，进程监控，自动重启等
- `Ansible`: [Ansible](http://www.ansibleworks.com/)是一个集成IT系统的配置管理，应用部署，执行特定任务的开源平台


## 其他
### Python学习资源
- 请参考我整理的[Python免费学习资源](https://lockshell.com/posts/python-free-resources/)

### 常用三方库
- 请参考我整理的[Python常用三方库](https://lockshell.com/posts/python-third-party-libs/)

### 前端基础
- html，css，JavaScript，jQuery，BootStrap，AngularJS，React，vue.js <br>
作为一个后端工程师，了解一些基本的前端知识也是必要的，关注下业界动态，按需学习即可。<br>
目前工作中用到`jQuery` + `BootStrap` + `AngularJS`来开发后台管理系统。

### 软件工程
- 设计模式<br>
Python是动态语言，许多Java复杂的设计模式用Python实现很简单，基本的设计模式也会用到。<br>
常用的有组合模式，单例模式、装饰器模式、工厂模式。
- REST接口 vs RPC接口<br>
软件工程说起来可能比较务虚，有比较才有差距，多看别人代码，借鉴提高。
