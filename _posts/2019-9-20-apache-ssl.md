---
title: Apache 增加 https 访问
date: 2019-09-20
categories:
tags: 
- PHP
- https
- ssl
---


在阿里云上申请免费的证书。[点击查看](https://common-buy.aliyun.com/?spm=5176.2020520163.cas.3.305156a7Dw5Reb&commodityCode=cas#/buy)

知道 cert 的存放目录。 从 /etc/httpd/conf.d/ssl.conf 查找。
把下载的证书放到相应的目录。例如新建一个跟域名相同的目录。
> /etc/ssl/certs/your.domain

找到 Apache 的配置目录 /etc/httpd/conf.d 
新建一个跟域名同名的配置文件 your.domain.conf
配置文件里填写如下配置

```shell
NameVirtualHost *:443

<VirtualHost *:443>
ServerName your.domain
DocumentRoot /var/www/your.dir
SSLEngine on
SSLCertificateFile /etc/ssl/certs/your.domain/your.domain-public.crt 
SSLCertificateKeyFile /etc/ssl/certs/your.domain/your.domain.key 
SSLCertificateChainFile /etc/ssl/certs/your.domain/your.domain-chain.crt
ErrorLog logs/microbed_error_log
TransferLog logs/microbed_access_log
LogLevel warn
</VirtualHost>
```

重启 Apache
> /etc/init.d/httpd reload
