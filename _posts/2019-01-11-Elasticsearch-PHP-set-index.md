---
title: Elasticsearch-PHP 动态修改索引配置
date: 2019-01-11 22:42
categories:
tags:
---

大数据分页，需要修改 elasticsearch 默认 `1w` 数据的限制。

```php
$paramsa = [
    'index'  => $indexResult,
    'body'   => [
        'settings' => [
            'max_result_window' => '100000000',
        ],
    ],
    'client' => [
        'curl' => [
            CURLOPT_HTTPHEADER => [  // 这里可以修复 header 报错。我的版本是 elasticsearch-php 2.3
                'Content-type: application/json',  
                'Authorization: foobarbaz',
            ],
        ],
    ],
];

$client->indices()->putSettings($paramsa);
```

手册地址: https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/_index_management_operations.html
