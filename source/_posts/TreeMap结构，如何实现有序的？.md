---
title: TreeMap结构，如何实现有序的？
date: 2021-01-14 19:06:09
tags: [面试, Java]
category: [面试, Java, 集合]
---

TreeMap实现SortMap接口，能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器。当用Iterator遍历TreeMap时，得到的记录是排过序的。TreeMap取出来的是排序后的键值对。但如果您要按自然顺序或自定义顺序遍历键，那么TreeMap会更好。TreeMap基于红黑树实现。TreeMap没有调优选项，因为该树总处于平衡状态。


```java
// 测试用例
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("3", 3);
treeMap.put("2", 2);
treeMap.put("1", 1);
treeMap.put("4", 4);
for (Map.Entry<String, Integer> item : treeMap.entrySet()) {
    String key = item.getKey();
    Integer value = item.getValue();
    System.out.println("key -> " + key + "; value -> " + value);
}
```


```
// 运行结果
key -> 1; value -> 1
key -> 2; value -> 2
key -> 3; value -> 3
key -> 4; value -> 4
```
