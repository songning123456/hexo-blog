---
title: ES相关度评分算法？
date: 2021-01-16 09:30:54
tags: [面试, Elasticsearch]
category: [面试, Elasticsearch]
---

# term frequency/inverse document frequency

简称为TF/IDF算法

# Term frequency

搜索文本中的各个词条在field文本中出现了多少次，出现次数越多就越相关。

# Inverse document frequency

搜索文本中的各个词条在整个索引的所有文档中出现了多少次，出现的次数越多就越不相关。

