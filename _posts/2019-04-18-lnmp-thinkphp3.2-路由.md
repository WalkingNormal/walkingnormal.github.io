---
title: lnmp 集成环境下thinkphp3.2路由不生效
date: 2019-03-28
categories:
tags: RabbitMQ
---

thinkphp3.2 程序采用路由规则后，放在 lnmp 服务器上，通过路由全部无法访问。

需要在 `/usr/local/php/etc/php.ini` 文件中 修改`cgi.fix_pathinfo=1` 

