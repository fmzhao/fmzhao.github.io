---
title: Python Essential Reference
layout: post
category: 技术 笔记
tags: python 实习
---

### pthon语言特性


Python是动态类型语言(dynamically typed language)，在程序的执行过程中，变量的名字可以与不同类型的值进行绑定, 这种绑定是发生在变量的声明的时候。这种语言的特性和c语言有很大的不同，c语言中一个变量名是代表固定的类型、大小、内存地址。

在一个动态类型的语言中，每一个变量名，通过变量声明(declaration)在编译时，绑定一个声明类型或者一个对象。对象的绑定是可选的，如果没有绑定一个对象，则这个变量名为null。一旦变量名绑定一个类型之后，这个变量名只能绑定相同类型的对象，不能绑定不同类型的对象。如果试图绑定其他类型的对象则会一起类型异常(tpye error)。

在一个静态类型的语言中，非null的变量名仅仅绑定一个对象。在执行的过程中，通过赋值(assignment)，这个变量名可能绑定不同类型的对象。

在一个弱类型的语言中，变量可以隐含(implicitly)转化为其他非相关的类型。

在一个强类型的语言中，变量不能够隐含转化为非相关的类型，如果要转化，显示的转换的必须的。

> java and c language are static typed language, python and php are dynamic typed language; java and python are strong typed language, c and php is weaked typed language. 

    #!/usr/bin python

    principal = 1000
    rate = 0.05
    numyears = 10
    year = 1
    while year <= numyears:
        principal = principal * (1 + rate)
    #    print year, principal
    #    print "%3d %0.2f" % (year, principal)
    #    print format(year, "2d"), format(principal, "0.2f")
        print "{0:2d} {1:0.2f}".format(year, principal)
        year += 1

> 代码中的变量principal最开始bound是integer(principal = 1000)，执行过程中bound float(principal = principal * (1 + rate))。

Python换行符表示新的statement开始，也可用用`;`将多个statement放在同一行中

Python用缩进(indentation)解释body关系，没有规定缩进的大小，只要保持一致性即可，但是通常用四个空格的缩进表示一个缩进的级别。

`%d %s %f`是special formatting-character，用来定义特定类型数据的格式，例如整数、字符串和浮点数，special formatting-character可以包含修饰符(modifiers)用来修饰宽度(width)和precision(精度)，例如`%3d %0.2f`。默认对其的方式是左对齐，修饰符的width表示向右对其width个字符。

Python没有特殊的switch语句，用来测试value，为了处理多种测试用例，使用`elif`

#### 文件相关操作

打开文件并读取:

    #!/usr/bin python

    f = open("open_file.py")
    line = f.readline()
    while line: 
        print line, #trailing ',' omits newline character
    #    print(line, end='') #use in Python 3
        line = f.readline()

    for line in open("open_file.py"):
        print line,
    f.close()

写入文件并写入：

    #!/usr/bin python

    principal = 1000
    rate = 0.05
    numberyears = 15
    year = 1

    f = open("out", "w")
    while year <= numberyears:
        principal = principal * (1 + rate)
        print >> f, "%3d %0.3f" % (year, principal)
        year += 1
    f.close()

标准输入与输出读写
    #!/usr/bin python

    import sys
    #print "Enter your name:", 
    #name = sys.stdin.readline()
    name = raw_input("Enter your name:")
    print "Welcome",name,"!"

#### Strings

```
a = "Hello World"
b = 'Python is groovy'
c = """Computer says 'NO'"""
```

> Triple-quoted strings are useful when the contents of a string literal span multiple lines of text.

```
x = 3.4
s = "The value of x is" + str(x)
s = "The value of x is" + repr(x)
s = "The value of x is" + format(x, "0.4f")
```

> str() 和 repr() 都可以产生字符串，但两者的结果略有不同，前者是输出结果的样子，而后者是在计算机中的实际表示。

#### Lists

Lists  are sequences of arbitrary objects.

把文件中内容读入list

    #!/usr/bin python

    import sys

    if len(sys.argv) != 2:
        print "Please supply a filename"
        raise SystemExit(1)
    f = open(sys.argv[1])
    lines = f.readlines()
    f.close()

    fvalues = [float(line) for line in lines]

    print "The minimum value is ", min(fvalues)
    print "The maximum value is ", max(fvalues)
    print sys.argv[0]

> `fvalues = [float(line) for line in lines]`可以简写成`fvalues = [float(line) for line in open(sys.argv[1])]`，这个表达式通过遍历list中的所有Strings构造了一个新的list，同时对所有的item应用了函数`float()`，这种强有力重构list的方法称为*list comprehension*。

#### Tuples

To create simple data structures, you can pack a collection of values together into a single object using a tuple.

Note: the contents of a tuple cannot be modified after creation. This reflects the fact that a tuple is best viewed as a single object consisting of several parts, not as a collection of distinct objects to which you might insert or remove items. Tuples are immutable.

Tuple和List混合使用，读取csc文件中的数据并转化格式后构建Tuple

    #!/usr/bin python

    filename = "portfolio.csv"
    portfolio = []
    for line in open(filename):
        fields = line.split(",")
        name = fields[0]
        shares = int(fields[1])
        price = float(fields[2])
        stock = (name, shares, price)
        portfolio.append(stock)

    print portfolio[1]

#### Sets

A set is used to contain an unordered collection of objects.

与List和Tuple不同，sets是无序的，并且不能用数字进行索引。

Sets支持标准的集合运算：

```
a = t | s #并集 Union of t and s
b = t & s #交集 Intersection of t and s
c = t - s #补集 Set difference (items in t, but not in s)
d = t ^ s #异或 Symmetric difference(items in t or s, but not both)
```

#### Directories

A directory is an associate array or hash table that comntains indexed by keys.

例如：

```
stodk = {
    "name"   : "GOOG"
    "shares" : 100
    "price"  : 490.10
}
```

通常使用字符串作为directory的key，但是也可以使用其他Python对象，比如数字、Tuple，想List和directory对象不能被用作key，因为不是immutable。

空directory可以通过两种方式创建：

```
prices = {} # An empty dict
prices = dicr() # An enmty dict
```

#### Iteration and Looping

`range(i, j, [,stride])`函数创造了一个list对象，代表从i到j-1的value，如果i省略，则从0开始。

#### Functions

You can use the `def` statement to create a function

当有多个值返回的时候，可以用一个返回一个Tuple

可以对函数的参数设置默认值，当设置默认值调用的时候，默认值参数可以不写，也可以任意的顺序参数来调用函数，但是这样调用的时候必须写出来参数的名称。

#### Generators

函数不仅仅能产生一个或者几个值，还可以产生一个generator。

    #!/usr/bin python

    def countdown(n):
        print "Counting down!"
        while n > 0:
            yield n # thd statement create generator
            n -= 1

    c = countdown(9)

    #print c.next()

    for i in countdown(5):
        print i

> Specially, when you write a statement such as for item in s, s could represent a list of items, the lines of a file, the result of a generator function, or any number of other objects that support iteration.

#### Coroutines

Normally, functions operate on a sigle set of input arguements. However, a function can also be written to operate as a task that process a sequence of inputs send to it. This type of function is known as a coroutine and is created by using the yieled statement as an expression (yield).

    #!/usr/bin python

    def print_matches(matchtext):
        print "Looking for", matchtext
        while True:
            line = (yield)
            if matchtext in line:
                print line

    matcher = print_matches("python")
    matcher.next()

    matcher.send("Hello, world!")
    matcher.send("python is cool!")
    matcher.send("cool!")
    matcher.send("I love python!")
    matcher.close()

#### Modules 

```
import div
impourt div as foo
from div import divide
from div import *
```

---

### 惯例与语法

可以使用Python的命令提示符(prompt)进行计算功能，`_`表示一个特殊变量，用来保存上一次的计算结果。

`\` 是 line-continue character。但是，当遇到truple-quoted string，list，Tuple，directory跨越多行时，不需要line-contine符号。

Python的结构是由缩进来决定的，例如：方法体(bodies of functions)，条件语句，循环语句和类的定义，如果这些结构中只包含一个语句，可以将它们放在同一行中。

---

### Types and Objects
