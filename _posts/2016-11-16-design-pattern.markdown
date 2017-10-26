---
layout: post
title: 设计模式
category: Java 设计模式
tags: 设计模式 
---

### 目录

- [1 模式是什么](#1)
- [2 设计模式原则](#2)
    - [2.1 单一职责原则](#2.1)
    - [2.2 开-闭原则](#2.2)
    - [2.3 里氏替换原则](#2.3)
    - [2.4 接口隔离原则](#2.4)
    - [2.5 依赖倒转原则](#2.5)
    - [2.6 迪米特法则](#2.6)
- [3 设计模式方法](#3)
    - [3.1 单例模式](#3.1)
    - [3.2 简单工厂模式](#3.2)
    - [3.3 工厂方法模式](#3.3)
    - [3.4 抽象工厂模式](#3.4)
    - [3.5 适配器模式](#3.5)
    - [3.6 装饰器模式](#3.6)
    - [3.7 代理模式](#3.7)
    - [3.8 合成模式](#3.8)
    - [3.9 桥梁模式](#3.9)
    - [3.10 模板模式](#3.10)
    - [3.11 策略模式](#3.11)
    - [3.12 迭代子模式](#3.12)
    - [3.13 观察者模式](#3.13)
    - [3.14 责任链模式](#3.14)

<h3 id='1'>模式是什么?</h3>

人们在自己环境中不断的发现问题和寻找问题解决方案的时候,发现有一些问题及其解决方案不断变换面孔重复出现,但这些不同面孔后面有着共同的本质,这些共同的本质就是模式.

模式化的过程就是把问题抽象化，在忽略不重要的细节后，发现问题的一般性本质，并找出普遍适用的解决方案的过程.

*学而时习之,不亦乐乎?*

模仿+实践是一种学习新事物的模式.

*知行合一.*

知行合一是王阳明心学这追求的模式.

---

<h3 id='2'>设计模式原则</h3>

<h4 id='2.1'>开-闭原则(OCP)(Open-Closed Principle)</h4>

开-闭原则讲的是：一个软件实体应该对扩展开放，对修改关闭(Software entries should be open for extension, but closed for modification)

> - 对元素的修改关闭(不允许修改的是系统的抽象层)
- 对体系结构的修改开放(允许扩展的是系统的实现层)

![Simple Factory Pattern UML](../image/simple_factory.png "简单工厂模式")

> 如果要新增加一种新的Product,只需要新增加一个Product类继承或者实现Product,完成了对体系结构的修改开放;而不必要去修改Product接口,完成了对元素的修改关闭.

<h4 id='2.2'>单一职责原则(Singleton Responsibility Principle, SRP)</h4>

不要存在多于一个导致类变更的原因，也就是说：一个类只做一件事。

类T负责两个不同的职责：职责P1，职责P2。当由于职责P1需求发生改变而需要修改类T时，有可能会导致原本运行正常的职责P2功能发生故障。另外，如果另外一个类需要复用职责P2，往往采用复制粘贴的办法，无法达到优雅的复用。

![单一职责原则示例](../image/srp.png)

> 违背单一职责原则的开发之所以容易发生，是因为职责扩散。所谓职责扩散，就是因为某种原因，职责P被分化为粒度更细的职责P1和P2。

<h4 id='2.3'>里氏替换原则(Liskov Substitution Principle, LSP)</h4>

**定义:** 如果对每一个类型为T1的对象o1,都有类型为T2的对象o2,使得以T1定义的所有程序P在所有的对象o1都替换成o2时，程序P的行为没有发生改变，那么类型T2是类型T1的子类型。换言之，一个软件实体如果使用的是一个基类的话，那么也一定适用其子类，而且它根本不能察觉出基类对象和子类对象的区别.

> 里氏替换原则是继承复用的基石。只有当衍生类可以替换掉基类，软件的单位功不能受到影响时，基类才能真正被复用，而衍生类才能够在基类基础上增加新的行为

一般而言，如果有两个具体类A和B有继承关系，那么一个最简单的符合里氏替换原则的方案应该是：建立一个抽象类C，然后让类A和类B成为抽象类C的子类.

> - “白马，马也；乘白马，乘马也。骊马，马也；乘骊马，乘马也”
- “妹，美人也，爱妹，非爱美人也”

<h4 id='2.4'>接口隔离原则(Interface Segregation Principle)</h4>

接口隔离原则讲的是: 使用多个专门的接口比使用单一的总借口要好.

从一个客户端的角度来讲,一个类对另一个类的依赖性要建立在最小的接口之上.客户端不应该依赖它不需要的接口.

![臃肿的接口](../image/isp-1.jpg "接口隔离原则")

![隔离的接口](../image/isp-2.jpg "接口隔离原则")

<h4 id='2.5'>依赖倒转原则(Dependece Inversion Priciple)</h4>

依赖倒转原则讲的是: 要依赖于抽象,不要依赖于具体.

抽象不应该依赖于细节;细节应当依赖抽象.(Abstraction should not depend upon details. Details should depend upon abstractions)

[参考: 依赖接口而不是具体实现](https://fmzhao.github.io/thinking-in-java/#9)

---

<h3 id='3'>设计模式方法</h3>

<h4 id='3.1'>单例模式(Singleton Pattern, creational)</h4>

![Singleton Pattern UML](../image/singleton.png "单例模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/singleton)

<h4 id='3.2'>简单工厂模式(Simple Factory Pattern, creational)</h4>

![Simple Factory Pattern UML](../image/simple_factory.png "简单工厂模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/simple_factory)

<h4 id='3.3'>工厂方法模式(Factory Method Pattern, creational)</h4>

![Factory Method Pattern UML](../image/factory_method.png "工厂方法模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/factory_method)

<h4 id='3.4'>抽象工厂模式(Abstract Factory Pattern, creational)</h4>

![Abstract Factory Pattern UML](../image/abstract_factory.png "抽象工厂模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/abstract_factory)

<h4 id='3.5'>适配器模式(Adapter Pattern，structural)</h4>

![Adapter Pattern UML](../image/adapter.png "适配器模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/adapter)

<h4 id='3.6'>装饰器模式(Decorator Pattern, structrual)</h4>

![Decorator Pattern UML](../image/decorator.png "装饰器模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/decorator)

<h4 id='3.7'>代理模式(Proxy Pattern, structural)</h4>

![Proxy Pattern UML](../image/proxy.png "代理模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/proxy)

<h4 id='3.8'>合成模式(Composite Pattern, structural)</h4>

![Composite Pattern UML](../image/composite.png "合成模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/composite)

<h4 id='3.9'>桥梁模式(Bridge Pattern, structural)</h4>

![Bridge Pattern UML](../image/bridge.png "桥梁模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/bridge)

<h4 id='3.10'>模板模式(Template Pattern, structural)</h4>

![Template Pattern UML](../image/template.png "模板模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/template)

<h4 id='3.11'>策略模式(Strategy Pattern, behavioral)</h4>

![Strategy pattern UML](../image/strategy.png "策略模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/strategy)

<h4 id='3.12'>迭代子模式(Iterator Pattern, behavioral)</h4>

![Iterator Pattern UML](../image/iterator.png "迭代子模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/iterator)

<h4 id='3.13'>观察者模式(Observer Pattern, behavioral)</h4>

![Observer Pattern UML](../image/observer.png "观察者模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/observer)

<h4 id='3.14'>责任链模式(Chain of Responsibility Pattern, behavioral)</h4>

![Chain of Responsibility Pattern UML](../image/chain_of_responsibility.png "责任链模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/chain_of_responsibility)

---
