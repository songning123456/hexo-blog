---
title: 单node环境下如何创建index？
date: 2021-01-16 09:14:35
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

```html
PUT /test_index
{
   "settings" : {
      "number_of_shards" : 3,
      "number_of_replicas" : 1
   }
}
```

* 单node环境下，创建一个index，有3个primary shard，3个replica shard；
* 集群status是yellow；
* 这个时候，只会将3个primary shard分配到仅有的一个node上去，另外3个replica shard是无法分配的；
* 集群可以正常工作，但是一旦出现节点宕机，数据全部丢失，而且集群不可用，无法承接任何请求。

