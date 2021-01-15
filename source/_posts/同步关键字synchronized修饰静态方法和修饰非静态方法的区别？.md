---
title: 同步关键字(synchronized)修饰静态方法和修饰非静态方法的区别？
date: 2021-01-15 11:05:17
tags: [面试, Java]
category: [面试, Java, 并发]
---

# 修饰非静态方法

```java
class Demo {
    private int i;
    Demo(int i) {
        this.i = i;
    }
    public synchronized void getI(String s) {
        for (int j = 0; j < 10000; j++) {
            System.out.println(i + "---------" + s);
        }
    }
}

public class ObjectLock implements Runnable {
    Demo demo;
    public ObjectLock(Demo demo) {
        this.demo = demo;
    }
    @Override
    public void run() {
        demo.getI(Thread.currentThread().getName());
    }
    public static void main(String[] args) {
        Demo demo = new Demo(1);
        Thread thread = new Thread(new ObjectLock(demo), "thread0");
        Thread thread1 = new Thread(new ObjectLock(demo), "thread1");
        Thread thread2 = new Thread(new ObjectLock(new Demo(2)), "thread2");
        thread.start();
        thread1.start();
        thread2.start();
    }
}
```

```
// 非静态方法结果
...
1---------thread0
1---------thread0
2---------thread2
1---------thread0
2---------thread2
1---------thread0
1---------thread1
1---------thread1
2---------thread2
1---------thread1
1---------thread1
...
```

可以看到Thread0和Thread2交替出现，Thread1和Thread2交替出现，但Thread0和Thread1不会交替出现。因为对非静态方法加锁，实际上是对调用该方法的对象加锁。Thread0和Thread1用的是同一个对象，所以互斥，但是Thread2则不受影响。

# 修饰静态方法

```java
class Demo {
    static int i;
    Demo(int i) {
        Demo.i = i;
    }
    public static synchronized void staticGetI(String s) {
        for (int j = 0; j < 10000; j++) {
            System.out.println(i + "---------" + s);
        }
    }
}

// ObjectLock重复部分略
...
    @Override
    public void run() {
        Demo.staticGetI(Thread.currentThread().getName());
    }
...
```

```
// 静态方法结果
...
2---------thread0
2---------thread0
2---------thread2
2---------thread2
2---------thread1
2---------thread1
...
```

三个线程均互斥。当synchronized修饰一个static方法时，多线程下，获取的是类锁(即Class本身，注意：不是实例)，作用范围是整个静态方法，作用的对象是这个类的所有对象。

# 一个对象在两个线程中分别调用一个静态同步方法和一个非静态同步方法

```java
public void run() {
    if (Thread.currentThread().getName().equals("thread0")){
        demo.staticGetI(Thread.currentThread().getName());
    }else if (Thread.currentThread().getName().equals("thread1")){
        demo.getI(Thread.currentThread().getName());
    }
} 
```

不会产生互斥。因为虽然是一个对象调用，但是两个方法的锁类型不同，调用的静态方法实际上是类对象在调用，即这两个方法产生的并不是同一个对象锁，因此不会互斥，会并发执行。

