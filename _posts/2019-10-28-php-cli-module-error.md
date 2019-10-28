---
title: php 命令行运行提示缺少模块 zip
date: 2019-10-28
categories:
tags: 
- PHP
---

报错如下
> Module 'zip' already loaded in Unknown on line 0

在采用CLI方式运行PHP的时候，每次都报标题上的错误。

原因：php.exe本身已经编译了zip扩展，而配置文件php.ini又开启了该扩展。

解决方法：在配置文件php.ini中，找到zip这个dll扩展，在前面加上英文的分号。重启Apache或者IIS等web服务器，再次测试，发现已经不报错了。
