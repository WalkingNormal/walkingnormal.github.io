---
title: FORBIDDEN/12/index read-only / allow delete (api)]
date: 2019-09-09
categories:
tags: 
- ElasticSearch
---

> ElasticSearch 查询出现 `FORBIDDEN/12/index read-only / allow delete (api)]` `403` 报错。 

1. 服务器空间满了。
2. 执行以下语句临时解决。
  > curl -XPUT -H "Content-Type: application/json" http://127.0.0.1:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'
  > 
  > _all 可以改成要解决的具体索引文件

