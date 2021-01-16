---
title: 什么是迭代器(Iterator)？Iterator和ListIterator的区别是什么？
date: 2021-01-14 18:52:56
tags: [面试, Java]
category: [面试, Java, 集合]
---

Iterator接口提供了很多对集合元素进行迭代的方法。每一个集合类都包含了可以返回迭代器实例的迭代方法。迭代器可以在迭代的过程中删除底层集合的元素。克隆(cloning)或者是序列化(serialization)的语义和含义是跟具体的实现相关的。因此，应该由集合类的具体实现来决定如何被克隆或者是序列化。

# Iterator

* 可用来遍历Set和List集合。
* 对集合只能是前向遍历。
* 实现了Iterator接口，并包含其他的功能。比如增加元素，替换元素，获取前一个和后一个元素的索引等等。

# ListIterator

* 只能用来遍历List。
* 既可以前向也可以后向。

