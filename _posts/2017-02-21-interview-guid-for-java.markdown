---
title: Java面试准备向导
layout: post
category: Java 实习
tags: 面试 指南
---

### Java笔试算法题OJ

[LeetCode OJ 平台](https://leetcode.com/ "LeetCode")

> 根据平台说明，先将easy level的算法题做一做。

### Java面试中常问的问题

#### JVM内存模型

* Java堆
* 方法区
* Java虚拟机栈
* 本地方法栈
* 程序计数器(Program Counter)

##### Java虚拟机栈

Java虚拟机栈是Java方法执行的内存模型，每一个方法在执行的时候都会创建一个栈帧，栈帧当中存放着局部变量表、操作数栈、动态链接、返回地址等。

Java虚拟机栈在编译的时候就确定了内存的大小。如果线程请求的栈深度大于虚拟机所能够提供的深度，将会抛出`StackOverflowError`；如果虚拟机在动态扩展栈时无法申请到足够的内存空间将会抛出`OutofMemoryError`。

局部变量表中存放的是方法参数和方法内部定义的局部变量、各种基本的数据类型、对象引用(reference)和ReturnAddress类型。

操作数栈用于保存中间变量。

动态链接指向方法区中的运行时常量池。

##### 堆

Java堆是用来存放

#### Java并发
