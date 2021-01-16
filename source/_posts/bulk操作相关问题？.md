---
title: bulk操作相关问题？
date: 2021-01-16 09:37:12
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

每一个操作要两个json串，语法如下：

```
{"action": {"metadata"}}
{"data"}
eg：
{"index": {"_index": "test_index", "_type", "test_type", "_id": "1"}}
{"test_field1": "test1", "test_field2": "test2"}
```

有哪些类型的操作可以执行呢？

* **delete**：删除一个文档，只要1个json串就可以了；
* **create**：PUT /index/type/id/_create，强制创建；
* **index**：普通的put操作，可以是创建文档，也可以是全量替换文档；
* **update**：执行的partial update操作。

bulk request会加载到内存里，如果太大的话，性能反而会下降，因此需要反复尝试一个最佳的bulk size。一般从1000~5000条数据开始，尝试逐渐增加。另外，如果看大小的话，最好是在5~15MB之间。

