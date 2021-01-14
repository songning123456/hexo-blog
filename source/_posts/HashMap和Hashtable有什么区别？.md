---
title: HashMap和Hashtable有什么区别？
date: 2021-01-14 18:56:18
tags: [面试, Java]
category: [面试, Java, 集合]
---

# HashMap

* 允许键和值是null。
* 非同步，适合于单线程环境。
* 可供应用迭代的键的集合，因此，HashMap是快速失败的。

# Hashtable

* 不允许键或者值是null。
* 同步，适合于多线程环境。
* 对键的列举(Enumeration)。
