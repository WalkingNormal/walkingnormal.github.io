---
title: PHP basename 获取中文文件名
date: 2019-05-29
categories:
tags: Elasticsearch
---

获取中文文件名需要设置好时区 [`setlocale()`](https://www.php.net/manual/zh/function.basename.php)。
```php
setlocale(LC_ALL, 'zh_CN.GBK');
```

不然获取不到正确的文件名。
