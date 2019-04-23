---
title: axios 在发送非简单请求时，会发送预检请求
date: 2019-04-23
categories:
tags: axios 预检 请求两次
---

在跟前端通过接口交互的时候，前端总报告后端`PHP`跨域问题。监控前端请求时，发现前端发送 `PUT` 请求时，会先发送 `OPTIONS` 预检请求。

[跨域资源共享 CORS 详解---阮一峰的博客](http://www.ruanyifeng.com/blog/2016/04/cors.html)

遇到类似问题的问答参考，对方使用的是 `Laravel` 框架，我这边还是 `Thinkphp3.2`，只能望洋兴叹。
https://learnku.com/laravel/t/6321/the-problem-of-sending-post-requests-to-options-when-axios-cross-domain-is-solved

