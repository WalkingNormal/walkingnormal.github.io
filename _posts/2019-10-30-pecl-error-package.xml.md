---
title: pecl 安装模块下载出错
date: 2019-10-30 10:32
categories:
- PHP
- PECL
---

```shell
sudo pecl install uploadprogress
```
执行命令后，提示如下

```shell
could not extract the package.xml file from "/build/buildd/php5-5.5.9+dfsg/pear-build-download/uploadprogress-1.0.3.1.tgz"
Download of "pecl/uploadprogress" succeeded, but it is not a valid package archive
Error: cannot download "pecl/uploadprogress"
Download failed
install failed
```

采用这样的方式处理
```shell
sudo pecl install -Z uploadprogress
```

- 参考链接：https://www.antojose.com/solved-php-pear-install-pecl-uploadprogress-on-ubuntu-14-04-fix-workaround-error-could-not-extract-package-xml-download-succeeded-but-not-valid-package-archive
