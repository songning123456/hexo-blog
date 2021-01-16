---
title: partial update(部分更新)实现原理？
date: 2021-01-16 09:36:07
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

```
post /index/type/id/_update
{
   "doc": {
      "要修改的少数几个field即可，不需要全量的数据"
   }
}

eg：

PUT /test_index/test_type/10
{
  "test_field1": "test1",
  "test_field2": "test2"
}

POST /test_index/test_type/10/_update
{
  "doc": {
    "test_field2": "updated test2"
  }
}
```

* 内部先获取document；
* 在内存中封装用户提交的新document，发送PUT请求到ES内部；
* 将老的document标记为deleted；
* 将新的document存入索引中。

比全量替换的优点：所有查询、修改和写回操作都发生在ES的一个shard内部，避免网络开销(减少2次网络请求)提升性能。

