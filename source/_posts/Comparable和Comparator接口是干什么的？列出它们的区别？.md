---
title: Comparable和Comparator接口是干什么的？列出它们的区别？
date: 2021-01-14 19:07:56
tags: [面试, Java]
category: [面试, Java, 集合]
---

# Comparable

Comparable是排序接口。若一个类实现了Comparable接口，就意味着“该类支持排序”。此外，“实现Comparable接口的类的对象”可以用作“有序映射(如TreeMap)”中的键或“有序集合(TreeSet)”中的元素，而不需要指定比较器。接口中通过x.compareTo(y)来比较x和y的大小。若返回负数，意味着x<y；返回零，意味着x=y；返回正数，意味着x>y。

```java
// Person对象
public class Person implements Comparable<Person> {
    private String name;
    private int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @Override
    public int compareTo(Person person) {
        // this.age - person.age升序，person.age - this.age降序
        return this.age - person.age;
    }
    @Override
    public String toString() {
        return this.name + "-" + this.age;
    }
}

// Comparable实现
public class ComparableMain {
    public static void main(String[] args) {
        ArrayList<Person> list = new ArrayList<>();
        list.add(new Person("ccc", 20));
        list.add(new Person("AAA", 30));
        list.add(new Person("bbb", 10));
        list.add(new Person("ddd", 40));
        System.out.println("Comparable-before: " + list);
        Collections.sort(list);
        System.out.println("Comparable-after: " + list);
    }
}

// 结果
// Comparable-before: [ccc-20, AAA-30, bbb-10, ddd-40]
// Comparable-after: [bbb-10, ccc-20, AAA-30, ddd-40]
```

# Comparator

Comparator是比较器接口。我们若需要控制某个类的次序，而该类本身不支持排序(即没有实现Comparable接口)；那么，我们可以建立一个“该类的比较器”来进行排序。这个“比较器”只需要实现Comparator接口即可。也就是说，我们可以通过“实现Comparator类来新建一个比较器”，然后通过该比较器对类进行排序。int compare(T o1, T o2)和上面的x.compareTo(y)类似，定义排序规则后返回。正数，零和负数分别代表大于，等于和小于。

```java
// Person略，去掉implements Comparable<Person>

// 升序
public class AscComparator implements Comparator<Person> {
    @Override
    public int compare(Person person1, Person person2) {
        return person1.getAge() - person2.getAge();
    }
}

// 降序
public class DescComparator implements Comparator<Person> {
    @Override
    public int compare(Person person1, Person person2) {
        return person2.getAge() - person1.getAge();
    }
}

// Comparator实现
public class ComparatorMain {
    public static void main(String[] args) {
        ArrayList<Person> list = new ArrayList<>();
        list.add(new Person("ccc", 20));
        list.add(new Person("AAA", 30));
        list.add(new Person("bbb", 10));
        list.add(new Person("ddd", 40));
        System.out.println("Comparator-before: " + list);
        AscComparator ascComparator = new AscComparator();
        list.sort(ascComparator);
        System.out.println("Comparator-asc: " + list);
        DescComparator descComparator = new DescComparator();
        list.sort(descComparator);
        System.out.println("Comparator-desc: " + list);
    }
}

// 结果
// Comparator-before: [ccc-20, AAA-30, bbb-10, ddd-40]
// Comparator-asc: [bbb-10, ccc-20, AAA-30, ddd-40]
// Comparator-desc: [ddd-40, AAA-30, ccc-20, bbb-10]
```
