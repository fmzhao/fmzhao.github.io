---
layout: post
title: 秋季校园招聘笔试题目集
category: 校园招聘
tags: 校招 笔试
---

---

**string是不可变(immutable/final)的,如何理解?比较stringbuffer  stringBuiler他们之间区别**

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

---

**An immutable class for example?**

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

---

**什么是多线程，为什么要使用多线程，多线程与多进程的区别**

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

---

**How final keyword works**

```
import java.util.*;
public class TestFinal{
    static final List<Integer> ls1;
    final List<Integer> ls2; 
    public TestFinal(){
        ls1 = new ArrayList<>();// compile error, because static instance is visible to all objects
        ls2 = new ArrayList<>();// correct, because one object can only init once
        ls2.add(1);
        ls2.add(2);
    }

    // Not correct, because the method will be invoked multi times
    public void set(List<Integer> ls){
        ls2 = ls;
    }

    public void add(Integer I){
        ls1.add(I);// correct, because we change the content, not the reference object itself
        ls2.add(I);// same as above
    }
}

About consturctor: Constructor can be invoked only one time per object by useing new keyword. Programmer cann't invoke constructor many times because consturctor is design so.

About method: Method can be invoked as many times as programmer warnts and compiler knows programmer can invoke method multi times.

Final class cannot be subclass

Final method cannot be overridden(this is in baseclass)

Final method can be a override method(this is in subclass)

Final keyword can decorate: class, field(static field), local variable, parameter, method
```

---

**对设计模式的设计原则是如何理解的**

```
设计模式的主要原则有：

1. 开闭原则(OCP, Open-Close Principle)

1) Software entries should be open for extension, but close for modification

2) 通过扩展已有的软件系统，可以通过新的行为，以满足对软件的新需求，使变化中的的软件系统有一定的适应性和灵活性；已有的软件模块，特别是最终要抽象层模块不能再修改，这样使变化中的系统有一点的稳定性和延续性

3) 要做到开闭原则：抽象化是关键；对可变性的封装原则(EVP, Priciple Of Encapsulation of Variation)

2. 里氏替换原则(LSP, Liskov Substitution Priciple)

1) 如果对每一个类型T1的对象o1，都有类型为T2的对象o2，使得T1定义的所有程序P在所有对象o1都替换成o2时，程序P的行为没有发生改变，那么类型T2是类型T1的子类型。也即是说：一个软件实体如果使用的一个基类的话，那么一定适用其子类，而且他根本不能觉察出基类对象和子类对象的区别

2) 里氏替换原则是复用的基石，只有当衍生类可以替换掉基类，软件单位的功能不会受到影响时，基类才能真正的被复用，而衍生类也能够在基类的基础上增加新的行为

3. 依赖倒转原则(DIP, Dependence Inversion Principle)

1) 依赖倒转原则讲的是：要依赖于抽象，不要依赖于具体

2) 抽象层次包含的是应用系统的商务逻辑和宏观的、对整体系统来说重要的战略决定，是必然性的体现；而具体层次则是一些次要的与实现有关的算法和逻辑，以及战术性从决定，带有相当大的偶然性的选择。具体层次的代码使经常会变动的，不能避免出现错误。抽象层次依赖于具体层次使得许多具体层次的细节的算法立刻影响到抽象层次的的宏观商务逻辑，导致微观决定宏观，战术决定战略，这样使很荒唐的事情。依赖倒转原则就是将这种很荒唐的事情反过来

3) 依赖倒转原则的另外一种说法是：要针对接口编程，不要针对具体编程。针对接口编程的意思是：应当使用Java的接口和抽象Java类进行变量的类型声明、参量类型声明、方法的放回类型声明、以及数据的类型转换等

4) 要做到依赖倒转原则的关键是：抽象耦合

4. 接口隔离原则(ISP, Interface Segregation Principle)

1) 几口隔离原则讲的是：使用多个专门的接口，总比是用单一的总接口要好。换言之：一个类对另一个类的依赖性应当是建立在最小的接口上的

2) For example:

// When the robot extends the interface, it must implements eat method, but it can't eat
// We call such interface fat interface or pollute interface

// interface segregation principle - bad example
interface IWorker {
    void work();
    void eat();
}

class Worker implements IWorker{
    public void work(){...}
    public void eat(){...}
}

class SuperWorker implements IWorker{
    public void work(){...}
    public void eat(){...}
}

class Manager{
    IWorker worker;
    
    public void setWorker(IWorker w){
        worker = w;
    }

    public void manage(){
        worker.work();
    }
}

// interface segregation priciple - good example
interface IWorkerable {
    void eat();
}

interface IFeedable{
    public void eat();
}

class Worker implements IWorkable, IFeedable{
    public void work(){...}
    public void eat(){...}
}

class SuperWorker implements IWorkable, IFeedable{
    public void work(){...}
    public void eat(){...}
}

class Robot implements IWorkable{
    public void work(){...}
}

5. 合成/聚合复用原则(CARP, Composite/Aggregate Reuse Priciple)

1) 合成/聚合复用原则也经常叫做合成复用原则(CRP, Compsite Reuse Priciple)。是在一个新的对象里面使用已有的对象，使之成为新对象的一部分；新的对象通过委派达到复用已有功能的目的

2) 尽量使用合成/聚合，尽量不要使用继承

3) 合成(Composition)和聚合(Aggregation)均是关联(Association)的特殊种类。聚合是用来表示"拥有"关系或者整体与部分的关系；而合成则表示一种强的多的"拥有"关系。在一个合成关系里，部分和整体的声明周期是一样的。一个合成的很对象完全拥有对其组成部分的支配权，包括它的创建和泯灭等。程序语言来说：组合而成的新对象组成部分的内存分配、内存释放有绝对责任。合成通常是值的聚合(Aggregation by Value)，而通常所说的聚合是引用聚合(Aggregation by Reference)

4) 继承复用的优点：新的实现比较容易，因为超类中的大部分功能可以通过继承关系自动进入子类；修改或扩展继承而来的实现较为容易

5) 为什么建议使用组合/聚合复用而不建议使用继承：继承复用破坏包装，因为继承将超类中的细节暴露给了子类，这种复用称之为透明复用或者白箱复用；如果超类的实现发生了改变，那么子类的实现也不得不发生改变。因此当基类发生改变的时候，这种改变就像水中投入石子引起的水波，将一圈又一圈的传递给一个又一个的子类当中，使得设计者不得不改变子类以适应这种变化

6. 迪米特法则(LoD, Law of Demeter), 也称之为最少知识原则(LKP, Least Knowledge Principle)
```

---

**类在什么情况下会触发加载**

```
1) A new instance of a class is created(in bytecode, the execution of a new instruction. Alternatively, via implicit creation: reflection, cloning, or deserialization)

2) The invocation of a static method decleared by a class(int bytecode, the execution of an invokestatic instruction)

3) The use or assignment of a static field declared by a class or interface, except for static fields that are final and initialized by a compile-time constant expression(in byte code, the execution of a getstatic or putstatic instruction)

4) The invocation of certain reflective methods in Java API, such as methods in class Class or in classes in the java.lang.reflect package

5) The initialization of a subclass of a class(Initialization of a class requires prior initialization of its superclass)

6) The designation of a class as the initial class(with the main() method) when Java Virtual Machine starts up
```

---
