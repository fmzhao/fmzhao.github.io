---
layout: post
title: 设计模式
category: Java 设计模式
tags: 设计模式 
---

**模式是什么?**

人们在自己环境中不断的发现问题和寻找问题解决方案的时候,发现有一些问题及其解决方案不断变换面孔重复出现,但这些不同面孔后面有着共同的本质,这些共同的本质就是模式.

模式化的过程就是把问题抽象化，在忽略不重要的细节后，发现问题的一般性本质，并找出普遍适用的解决方案的过程.

*学而时习之,不亦乐乎?*

模仿+实践是一种学习新事物的模式.

*知行合一.*

知行合一是一种提高自身修养的模式.

---

**设计模式原则**

一. 开-闭原则(OCP)(Open-Closed Principle)

**开-闭原则讲的是：一个软件实体应该对扩展开放，对修改关闭(Software entries should be open for extension, but closed for modification)**

> - 对元素的修改关闭(不允许修改的是系统的抽象层)
- 对体系结构的修改开放(允许扩展的是系统的实现层)

![Simple Factory Pattern UML](../image/simple_factory.png "简单工厂模式")

> 如果要新增加一种新的Product,只需要新增加一个Product类继承或者实现Product,完成了对体系结构的修改开放;而不必要去修改Product接口,完成了对元素的修改关闭.

二. 单例原则/模式(Singleton Principle)

参考设计模式方法中的单例模式.

三. 里氏替换原则(LSP)

**定义:** 如果对每一个类型为T1的对象o1,都有类型为T2的对象o2,使得以T1定义的所有程序P在所有的对象o1都替换成o2时，程序P的行为没有发生改变，那么类型T2是类型T1的子类型。换言之，一个软件实体如果使用的是一个基类的话，那么也一定适用其子类，而且它根本不能察觉出基类对象和子类对象的区别.

> 里氏替换原则是继承复用的基石。只有当衍生类可以替换掉基类，软件的单位功不能受到影响时，基类才能真正被复用，而衍生类才能够在基类基础上增加新的行为

一般而言，如果有两个具体类A和B有继承关系，那么一个最简单的符合里氏替换原则的方案应该是：建立一个抽象类C，然后让类A和类B成为抽象类C的子类.

> 里氏替换原则的理解:

>> - “白马，马也；乘白马，乘马也。骊马，马也；乘骊马，乘马也”
- “妹，美人也，爱妹，非爱美人也”

四. 接口隔离原则(Interface Segregation Principle)

接口隔离原则讲的是: 使用多个专门的接口比使用单一的总借口要好.

从一个客户端的角度来讲,一个类对另一个类的依赖性要建立在最小的接口之上.客户端不应该依赖它不需要的接口.

![臃肿的接口](../image/isp-1.jpg "接口隔离原则")

![隔离的接口](../image/isp-2.jpg "接口隔离原则")

五. 依赖倒转原则(Dependece Inversion Priciple)

依赖倒转原则讲的是: 要依赖于抽象,不要依赖于具体.

抽象不应该依赖于细节;细节应当依赖抽象.(Abstraction should not depend upon details. Details should depend upon abstractions)

[依赖接口而不是具体实现](https://fmzhao.github.io/thinking-in-java/#9)

---

**设计模式方法**

一、单例模式(Singleton Pattern, creational)

![Singleton Pattern UML](../image/singleton.png "单例模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/singleton)

二、简单工厂模式(Simple Factory Pattern, creational)

![Simple Factory Pattern UML](../image/simple_factory.png "简单工厂模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/simple_factory)

三、工厂方法模式(Factory Method Pattern, creational)

![Factory Method Pattern UML](../image/factory_method.png "工厂方法模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/factory_method)

四、抽象工厂模式(Abstract Factory Pattern, creational)

![Abstract Factory Pattern UML](../image/abstract_factory.png "抽象工厂模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/abstract_factory)

五、适配器模式(Adapter Pattern，structural)

![Adapter Pattern UML](../image/adapter.png "适配器模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/adapter)

六、装饰器模式(Decorator Pattern, structrual)

![Decorator Pattern UML](../image/decorator.png "装饰器模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/decorator)

七、代理模式(Proxy Pattern, structural)

![Proxy Pattern UML](../image/proxy.png "代理模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/proxy)

八、合成模式(Composite Pattern, structural)

![Composite Pattern UML](../image/composite.png "合成模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/composite)

九、桥梁模式(Bridge Pattern, structural)

![Bridge Pattern UML](../image/bridge.png "桥梁模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/bridge)

十、模板模式(Template Pattern, structural)

![Template Pattern UML](../image/template.png "模板模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/template)

十一、策略模式(Strategy Pattern, behavioral)

![Strategy pattern UML](../image/strategy.png "策略模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/strategy)

十二、迭代子模式(Iterator Pattern, behavioral)

![Iterator Pattern UML](../image/iterator.png "迭代子模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/iterator)

十三、观察者模式(Observer Pattern, behavioral)

![Observer Pattern UML](../image/observer.png "观察者模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/observer)

十四、责任链模式(Chain of Responsibility Pattern, behavioral)

![Chain of Responsibility Pattern UML](../image/chain_of_responsibility.png "责任链模式")

[示例代码](https://github.com/FengMengZhao/language_learn/tree/master/thinking_in_java/design_pattern/chain_of_responsibility)

---
