---
title: left join、inner join和right join的区别？
date: 2021-01-15 15:20:04
tags: [面试, 数据库]
category: [面试, 数据库]
---

{% asset_img join-method.jpg %}

{% asset_img test-join.PNG %}

# left join 

返回包括左表中的所有记录和右表中联结字段相等的记录。 

```sql
select user.id as user_id, user.user_name, class.id as class_id, class.class_name from user left join class on user.id = class.id
```

{% asset_img left-join.PNG %}

# inner join 

返回包括右表中的所有记录和左表中联结字段相等的记录。 

```sql
select user.id as user_id, user.user_name, class.id as class_id, class.class_name from user inner join class on user.id = class.id
```

{% asset_img inner-join.PNG %}

# right join

只返回两个表中联结字段相等的行。

```sql
select user.id as user_id, user.user_name, class.id as class_id, class.class_name from user right join class on user.id = class.id
```

{% asset_img right-join.PNG %}

