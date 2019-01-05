---
title: Elasticsearch-PHP Content-Type header is not supported
date: 2019-01-05 14:17
categories:
tags:
---

> 在查找问题的时候，需要把问题关键字写多一点，这样才能尽可能快地找到答案。

PHP5.4 环境中使用 `Elasticsearch-PHP v2.3.2` 的 `search()` 方法遇到 `Content-Type header [] is not supported`

在必应 国际版 搜索 `Elasticsearch-PHP 2.* search Content-Type header [] is not supported`

找到了这条链接 https://github.com/elastic/elasticsearch-php/issues/205

发现 `polyfractal` 的回答

![F7A9E9.png](https://s2.ax1x.com/2019/01/05/F7A9E9.png)

代码如下
```php
$client = Elasticsearch\ClientBuilder::create()->build();
$params = [
    'index' => 'test',
    'type' => 'test',
    'body' => [
        'query' => [
            'match_all' => []
        ]
    ],
    'client' => [
        'curl' => [
            CURLOPT_HTTPHEADER => [
                'Content-type: application/json',
                'Authorization: foobarbaz'
            ]
        ]
    ]
];
$client->search($params);
```

在我的 `$params` 中增加 `client` 设置后，一切工作正常。

