---
layout: post
title: 秋季校园招聘笔试题目集
category: 校园招聘
tags: 校招 笔试
---

### 2016-08-01

* 数据库表设计:一个公司生产产品,每个产品由很多配件组成，配件由厂商生产,根据此设计数据库表

* 三次握手和四次挥手

* 语言实现链表倒序

* 数组中存储很多整数,求两个数和等于N的数组下标,找到两个即可停止.(尽量优化算法)

* 数据库的优化语句,如何实现查询效率尽可能高(索引)

* 三个数组均存储整数,三个数组分别从大到小已经排好序,如何求前k个最大值(堆)

* 三个线程,并发进行,如何统计三个文件中关键词的个数(竞争锁,HashMap)

### 2016-08-24

* 每个线程有个looper,它管理messageQueue,他是如何做到各个looper独立运行的

* java的内存结构,堆栈的介绍,堆栈中的方法和变量是线程共享的吗

* 设计模式,单例模式介绍,懒汉式饿汉式加载模式,如何保证懒汉式加载线程安全

* hashMap如何保证线程安全

* string是不可变(immutable/final)的,如何理解?比较stringbuffer  stringBuiler他们之间区别

```
String is immutable/final generally for two reasons:

1. String objct are cached in String pool. Since cached String literals are shared between multiple clients there is always a risk, where one client's action would affect another client; Caching of String objects is important for performance reason.

2. String has been widely used as parameter for many java classes, e.g. for opening network connection, you can pass hostname and port number as String; you can pass database URL as a String for opening database connection; you can open any file by passing the name of the file as arguement to File I/O classes.

3. String are very popular as HashMap key, it is important for them to be immutable so that they can be retrieve the value object which is stored in hashmap. HashMap works in the principle of hashing, which requires same value to function properly. Mutable String would product two different hashcodes at the time of insertion and retrieval if contents of String was modified after insertion, potentially losing the value object in the map.

4. The absolutely most important reason that String is immutable is that it is used by the class loader mechanism, and thus have profound and fundamental security aspects.

5. String is immutable, it can safely share between many threads which is very important for multithreaded programming and to avoid any synchronization issue in java. Immutablity also makes String instance thread-safe in java, means you don't need to synchronized String operation externally. 


Difference between String StringBuffer and StringBuilder:

1. Mutability Difference: String is immutable, if you want to change its value, another object will be created, whereas StringBuffer and StringBuilder is multable, so you can change its values.

2. Thread-Safety Difference: StringBuffer is thread-safe, whereas not for StringBuilder, and StringBuilder is more efficient.

So the solutions:

1) If String is not gong to change, use String. 

2) If String is going to change and always for single thread, use StringBuiler for performance.

3) If String is going to change and will be accessed from multiple threads, use a StringBuffer for the thread-safety synchronization
```

* An immutable class for example?

```
public final class Student{
    private String name;// this is immutable(private)

    public Student(String name){
        this.name = name;
    }
    
    public String getName(){
        return name;
    }
}
```

* 做过的项目比较有特色的介绍一下

* ==和equals和hashcode有什么区别,分别介绍

* linkedList和arraylist区别,从数据存储,查询,删除方面分析,他们的效率

* 进程和线程的区别,安卓如何实现多进程和多线程,安卓如何新建线程

### 2016-08-25

* http状态码(blabla)和缓存相关的头(cache－control expires etag Last-Modified)

* 简介tcp ip?(...说的不太好) tcp怎么实现可靠性?(数据分块,重传,滑动窗口)无状态的http怎么实现一个状态?(cookie session,长连接,websocket?最后一个是胡说的...)

* 输入url到页面现实的过程...(大概对了,说的不太好)遇到link script标签怎么处理?(同步执行?不太确定)

* 手写个归并吧(写出来了，但是不流利)

### 2016-09-06

* 什么是多线程，为什么要使用多线程，多线程与多进程的区别

```
What is thread?

1. A thread is an independent set of values of the processor registers(for a single core). Since this includes the Instruction Pointer(aka Program Counter), which controls what executes in what order. It also includes the Stack Pointer, which had better point to a unique area of memory for each thread or else they will interfere with each other.

2. Threads are the software unit affected by control flow(function call, loop, switch), because those instructions operate on the Instruction Pointer, and that belongs to a paritcular thread. Threads are often scheduled arrording to some prioritization scheme(although it is possible to design a system with one thread per processor core, in which case every thread is always running and no shcheduling is needed).

3. In fact the value of the Instruction Pointer and the instruction stored at that location is sufficient to determine a new value for Instruction Pointer. For most instructions, this simply advances the IP by the size of the instruction, but control flow instructions change the IP in other, predicatable ways. The sequence of values the IP takes on forms a path of execution weaving through the program code, giving rise to the name "thread".

ps: The exact list of CPU registers depends on the architecture, but instruction pointer and stack pointer are pretty much universal. They define a thread insofar as when this thread(set of register values) is loaded in the processor core, the thread is running. The processor is fetching instructions demanded by the thread and updateing the thread registers. When a contex switch is needed, the processor saves this set of register values into memeory and loads a set belonging to defferent thread, typically as part of the interrupt servicing logic.

Why we need multi therad?

1. The main reason, in many applications, multiple activities are going on at once. Some of these may block from time to time. By decomposing such an application into multiple sequential threads that run in quasi-parallel, the programming model becomes simpler.

2. Thread is lighter weight than process, they are easier to creat and destroy than processes, which is about 10-100 times faster than create a process.

3. About performance, threads yield no performance gain when all of them are CPU bound, but when there is a substantial
computing and substantial I/O, having threads allows these activities to overlap, thus speeding up the application. 
```
