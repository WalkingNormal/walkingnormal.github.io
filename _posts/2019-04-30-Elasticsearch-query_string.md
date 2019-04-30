---
title: Elasticsearch 的 query_string 语法
date: 2019-04-30
categories:
tags: Elasticsearch
---

Elasticsearch 中存储如下日志信息，
```
[2019-04-30 13:42:42] AMQP02-IOTSVR1006 9636 [INFO] appLog - 21004507 tocloud message: {"msgid":"20190430134241","devid":"21004507","cmd":"42","data":"S0120398701020328","data_base":"210045074220190430134241S012039870102032831B9","sender":"client","user_id":"15","server_id":"1005","ctime_stamp":1556602962,"ctime":"2019-04-30 13:42:42","docType":"tocloud"}
[2019-04-30 13:42:42] AMQP02-IOTSVR1006 9636 [INFO] appLog - 61000341 tortu message: {"msgid":"20190430134235","devid":"61000341","cmd":"42","data":"","data_base":"##610003414220190430134235FFFF@\r\n","sender":"server","user_id":"15","server_id":"1005","ctime_stamp":1556602962,"ctime":"2019-04-30 13:42:42","docType":"tortu"}
```
需要排除 `"data":""` 这种空数据，通过数据分析，可以通过 `"sender server" AND "cmd 42"` 查询限制。查询语法示例

```
"must_not" => array(
                [
                    "query_string" => [
                        "query"            => "\"sender server\" AND \"cmd 42\"",
                        "analyze_wildcard" => true,
                        "default_field"    => "message",
                    ],
                ],
            ),
```

