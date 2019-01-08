---
title: Elasticsearch-PHP2.3 使用scroll 返回Unrecognized token错误
date: 2019-01-08 12:00
categories:
tags:
---

使用 必应国际版搜索 `Elasticsearch scroll  Unrecognized token`

找到这个链接 https://github.com/elastic/elasticsearch-php/issues/564

![FqdhoF.png](https://s2.ax1x.com/2019/01/08/FqdhoF.png)

跟手册说明不一样。[手册](https://www.elastic.co/guide/cn/elasticsearch/php/current/_search_operations.html)说明是这样操作

```php
$client = ClientBuilder::create()->build();
$params = [
    "scroll" => "30s",          // how long between scroll requests. should be small!
    "size" => 50,               // how many results *per shard* you want back
    "index" => "my_index",
    "body" => [
        "query" => [
            "match_all" => new \stdClass()
        ]
    ]
];

// Execute the search
// The response will contain the first batch of documents
// and a scroll_id
$response = $client->search($params);

// Now we loop until the scroll "cursors" are exhausted
while (isset($response['hits']['hits']) && count($response['hits']['hits']) > 0) {

    // **
    // Do your work here, on the $response['hits']['hits'] array
    // **

    // When done, get the new scroll_id
    // You must always refresh your _scroll_id!  It can change sometimes
    $scroll_id = $response['_scroll_id'];

    // Execute a Scroll request and repeat
    // <span style="color:red;">这里并没有说明还需设置 'body' => 'scroll_id'=>$scroll_id</span>
    $response = $client->scroll([
            "scroll_id" => $scroll_id,  //...using our previously obtained _scroll_id
            "scroll" => "30s"           // and the same timeout window
        ]
    );
}
```
