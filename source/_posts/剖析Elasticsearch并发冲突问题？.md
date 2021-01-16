---
title: 剖析Elasticsearch并发冲突问题？
date: 2021-01-16 09:15:53
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

# 悲观锁

常见关系型数据库，比如mysql，读取时加锁。

# 乐观锁

不加锁。写的时候判断当前version和ES的version是否一致。

