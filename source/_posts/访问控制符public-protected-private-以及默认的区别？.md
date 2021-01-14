---
title: 访问控制符public,protected,private,以及默认(default)的区别？
date: 2021-01-14 16:15:12
tags: [面试, Java]
category: [面试, Java, 基础]
---

| 修饰符 | 当前类 | 同包 | 子类 | 其他包 | 
| :----- | :----- | :----- | :----- | :----- | 
| public | √ | √ | √ | √ | 
| protected | √ | √ | √ | × |  
| default | √ | √ | × | × | 
| private | √ | × | × | × |   

类的成员不写访问修饰时默认为default。默认对于同一个包中的其他类相当于公开(public)，对于不是同一个包中的其他类相当于私有(private)。受保护(protected)对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。Java中，外部类的修饰符只能是public或默认，类的成员(包括内部类)的修饰符可以是以上四种。
