---
title: 基于translog和commit point如何进行数据恢复？
date: 2021-01-16 09:34:18
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

fsync+清空translog，就是flush，默认每隔30分钟flush一次，或者当translog过大的时候，也会flush。POST /my_index/_flush，一般来说别手动flush，让它自动执行就可以了。translog每隔5秒被fsync一次到磁盘上。在一次增删改操作之后，当fsync在primary shard和replica shard都成功之后，那次增删改操作才会成功。但是这种在一次增删改时强行fsync translog可能会导致部分操作比较耗时，也可以允许部分数据丢失，设置异步fsync translog。

```
PUT /my_index/_settings
{
    "index.translog.durability": "async",
    "index.translog.sync_interval": "5s"
}
```
