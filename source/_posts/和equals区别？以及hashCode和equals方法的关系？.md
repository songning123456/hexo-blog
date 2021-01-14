---
title: '==和equals区别？以及hashCode和equals方法的关系？'
date: 2021-01-14 14:31:50
tags: [面试, Java]
category: [面试, Java, 基础]
---

# 功能不同

==判断两个变量或实例是不是指向同一个内存空间。equals判断两个变量或实例所指向的内存空间的值是不是相同。

# 定义不同

==在JAVA中只是一个运算符合。equals在JAVA中是一个方法。

# 运行速度不同

==快，equals慢。


**总结：equals相等，hashcode必相等；hashcode相等，equals可能不相等。**
