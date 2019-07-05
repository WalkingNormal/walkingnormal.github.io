---
title: Nginx 转发到 Apache 服务器跨域
date: 2019-07-05
categories:
tags: 
- PHP 
- 跨域
---

按我以前遇到的跨域处理，都是在 `PHP` 程序这边，输出信息的时候加上跨域 `Header`.

```php
header("Access-Control-Allow-Origin:*");
header("Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept, Connection, User-Agent, Cookie,Authorization,HTTP_AUTHORIZATION");
header('Access-Control-Allow-Methods', 'OPTIONS, GET, PUT, POST, DELETE');
```
但是这次因为是 `Nginx` 转发过来，程序这边设置后，前端还是提示跨域，并且 `PUT`、`DELETE` 方法不支持。
前端提示这样的错误：`Method PUT is not allowed by Access-Control-Allow-Methods in preflight response`

这样的情况，**都需要在 `Nginx` 上增加跨域配置**。

```
location / {  
    add_header Access-Control-Allow-Origin *;
    add_header Access-Control-Allow-Methods 'GET, POST, PUT, DELETE, OPTIONS';
    add_header Access-Control-Allow-Headers 'DNT,X-Mx-ReqToken,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization';

    if ($request_method = 'OPTIONS') {
        return 204;
    }
} 
```
