---
title: 什么是mapping？mapping的核心数据类型？dynamic mapping时数据类型转换？如何查看mapping？
date: 2021-01-16 09:27:50
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

自动或手动为index中type建立的一种数据结构和相关配置，简称mapping。dynamic mapping自动为我们建立index、创建type以及type对应的mapping。mapping中包含了每个field对应的数据类型，以及如何分词等设置，包括自动设置数据类型，也可以提前手动创建index和type的mapping，自己对各field进行设置，包括数据类型、索引行为、分词器等等。

mapping核心数据类型string、byte、short、integer、long、float、double、boolean、date。

dynamic mapping时true or false转boolean、123转long、123.45转double、2017-01-01转date、"hello world"转string/text。

查询mapping：GET /index/_mapping/type。

