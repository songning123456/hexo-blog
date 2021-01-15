---
title: PreparedStatement比Statement有什么优势？
date: 2021-01-15 17:16:19
tags: [面试, SSM]
category: [面试, SSM]
---

# Statement

* 每次执行sql语句，相关数据库都要执行sql语句的编译。
* 在对数据库只执行一次性存取的时侯，用Statement对象进行处理。
* 是'+'字符串拼接，安全性较低。

# PreparedStatement

* PreparedStatement是预编译的，对于批量处理可以大大提高效率，也叫JDBC存储过程。
* 对象的开销比Statement大，对于一次性操作并不会带来额外的好处。
* 用'?'传参,可以防止sql注入，具有安全性。
