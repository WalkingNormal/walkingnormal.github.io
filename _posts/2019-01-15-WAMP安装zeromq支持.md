---
title: WAMP 增加 zeromq(php-zmq)支持
date: 2019-01-15 13:48
categories:
tags:
---

## 安装 zmq 程序
下载地址： http://zeromq.org/distro:microsoft-windows

## 安装 php-zmq 模块
下载地址: http://pecl.php.net/package/zmq

这里我的是 `windowns` 系统，下载 `DLL` 文件。下载好的文件里，把 `libzmq.dll` 放在 `PHP` 目录下，例如 `E:\wamp\bin\php\php7.2.10\`, 把 `php_zmq.dll` 放在 `PHP` 的 `ext` 目录下，例如: `E:\wamp\bin\php\php7.2.10\ext\`

## 重启 wamp

---

刚开始以为本地环境，只要安装下 `php-zmq` 模块就行了，总是出现 ` Unable to load dynamic library 'zmq'`这样的错误，谷歌百度出来的答案，都是第二步操作的事，没有说明还要安装 **`zmq` 程序**。
