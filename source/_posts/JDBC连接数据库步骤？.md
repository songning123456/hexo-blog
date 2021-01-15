---
title: JDBC连接数据库步骤？
date: 2021-01-15 17:18:59
tags: [面试, SSM]
category: [面试, SSM]
---

# 加载JDBC驱动程序

通过Class类的forName方法实现，并将驱动地址放进去成功加载后，会将Driver类的实例注册到DriverManager类中。


# 提供JDBC连接的URL、创建数据库的连接

要连接数据库，需要向java.sql.DriverManager请求并获得Connection对象，该对象就代表一个数据库的连接。使用DriverManager的getConnection()方法传入指定的欲连接的数据库的路径、数据库的用户名和密码。

```java
 Connection con = DriverManager.getConnection(url,username,password);
 "jdbc:mysql://localhost:3306/test?user=root&password=123&useUnicode=true&characterEncoding=utf-8"
```


# 创建一个Statement

要执行SQL语句，必须获得java.sql.Statement实例；执行静态SQL语句，通常通过Statement实例实现；执行动态SQL语句，通常通过PreparedStatement实例实现。

```java
String sql = "";
Statement st = con.createStatement();  
PreparedStatement pst = con.prepareStatement(sql);
```


# 执行SQL语句

Statement接口提供了executeQuery、executeUpdate、execute三种方法。executeQuery执行select语句，返回ResultSet结果集；executeUpdate执行insert、update、delete语句。

```java
ResultSet rst = pst.executeQuery();
```


# 关闭JDBC对象

操作完成以后要把所有使用的JDBC对象全都关闭，以释放JDBC资源。
