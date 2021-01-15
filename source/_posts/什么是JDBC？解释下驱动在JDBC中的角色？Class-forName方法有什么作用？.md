---
title: 什么是JDBC？解释下驱动在JDBC中的角色？Class.forName方法有什么作用？
date: 2021-01-15 17:14:34
tags: [面试, SSM]
category: [面试, SSM]
---

{% asset_img JDBC.jpg %}

* JDBC是允许用户在不同数据库之间做选择的一个抽象层。JDBC允许开发者用JAVA写数据库应用程序，而不需要关心底层特定数据库的细节。
* JDBC驱动提供了特定厂商对JDBC API接口类的实现，驱动必须要提供java.sql包下面这些类的实现：Connection, Statement, PreparedStatement,CallableStatement, ResultSet和Driver。
* Class.forName()用来载入跟数据库建立连接的驱动。