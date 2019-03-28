---
title: 使用php-amqplib/php-amqplib提示 bcadd() 错误
date: 2019-03-28
categories:
tags: elastic
---
提示如下错误
> PHP Fatal error:  Call to undefined function PhpAmqpLib\Wire\bcadd()

需要给 PHP 增加 bcmath 扩展

centos 系统增加扩展，参考如下链接
https://github.com/shavitush/bhoptimer/issues/20#issuecomment-196512329
