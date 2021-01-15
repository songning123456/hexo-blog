---
title: 什么时候使用CallableStatement？用来准备CallableStatement的方法是什么？
date: 2021-01-15 17:17:43
tags: [面试, SSM]
category: [面试, SSM]
---

CallableStatement用来执行存储过程。存储过程是由数据库存储和提供的。存储过程可以接受输入参数，也可以有返回结果。非常鼓励使用存储过程，因为它提供了安全性和模块化。准备一个CallableStatement的方法是：CallableStament.prepareCall()。

