---
layout: post
category: 计算机系统 计算机语言
tags: 计算机基础 计算机底层 汇编语言
title: 底层编程(汇编语言)
---

---

### Introduction

**What is kernel?**

The kernel is the core part of an operating system keeps track of everything.

The kernel is both and an fence and gate. 

As a gate, it allows programs to access hardware in uniform way. Without the kernel, you would have to write programs to deal with every device model ever made. The kernel handles all device-specific interacitons so you don't have to. It also handles file access and intraction between process. 

As a fence, the kernel prevents programs from accidentally overwriting each other's data and from accessing files and devices that they don't have permission to. It limits the amout of damage a poorly-written program can do to other running programs.

**计算机语言**

*机器语言(Machine Language)*

This is what computer actually sees and deals with. Every command the computer sees is given as a number or sequence of number.

*汇编语言(Assembly Language)*

This is the same as machine language, except the command numbers have been replaced by letter sequences which are easier to memorize. Other small things are done to make it easier as well.

*高级语言(High-Level Language)*

High-Level language are there to make programming easier. Assembly language requiers you to work with the machine itself. High-Level Language allow you to describe the program in a more natural language. A single command in a high-level language usually is equivalent to sevel commands in an assembly language.

---

### 计算机组成(Computer Architecture)

Modern computer architecture is based off of an architecture called the Von Neumann architecture. The Von Neumann architecture divides the computer up into two main parts - the CPU(for Central Processing Unit) and the memory.

**Data Accessing Methods(Addressing Modes)**

*immediate mode*

The data to access is embedded in the instruction itself.

*register addressing mode*

The instruction contains a register to access, rather than a memory location.

*direct addressing mode*

The instruction contains the memory address to access.

*index addressing mode*

The insturction contains a memory address to access, and also specific and index register to offset that address.

*indirect addressing mode*

The instruction contains a pointer to where the data should be accessed.

*base pointer addressing mode*

This is similar to indirect addressing, but you also include a number called offset to add to the register's value before using it to look up.

---

### Your first programs

     .section .data #follow the data

     .section .text #follow the code

     .globl _start #mark the location of the start of the program

    _start: #the program entrance function
     movl $1, %eax #the linux kernel command number(system call) for exiting a program
     movl $0, %ebx #the parameter of the exit command(exit status)
     int $0x80 #wake up the kernel to run the exit command, the int stands for interrupt

> 上面的程序是汇编源码，后缀为`.s`，源码要经过编译器编译为目标文件(object file)，后缀为`.o`，编译的命令为：`as -o exit.o eixt.s`；An objce file is code that is in the machine language, but has not been completely put together；目标文件要经过链接(link)，链接器将目标文件组合在一起，并加入一些信息让kernel知道怎么加载和运行，链接的命令为：`ld -o exit exit.o`。

> Anything start with a period isn't directly translated into machine instruction. Instead, it's an instruction to the assembler itself. These are called assembler directives or pseudo-operations because they are handled by the assembler and are not actually run by the computer.

**Addressing Model**

The general form of memory address references is like:

```
ADDRESS_OR_OFFSET(%BASE_OR_OFFSET, %INDEX, MULTIPLIER)

FINAL ADDRESS = ADDRESS_OR_OFFSET + %BASE_OR_OFFSET + MULTIPLIER * %INDEX
```

> ADDRESS_OR_OFFSET and MULTIPLIER must be contants, while %BASE_OR_OFFSET and %INDEX must be register

*direct addressing mode*

This is done by only using the ADDRESS_OR_OFFSET portion. e.g., `movl ADDRESS, %eax`

*index addressing mode*

This is done by using The ADDRESS_OR_OFFSET and the %INDEX protion.

*indirect addressing mode*

Indirect addressing mode loads value from address indicated by a register. e.g., `movl (%eax), %ebx`

*base pointer addressing mode*

This is similar to indirect addressing mode, except that adds a constant value to the address in the register. e.g., `movl 4($eax), %ebx`

*immediate mode*

Immediate mode is used to load direct values into registers or memory location. e.g., `movl $12, %eax`

*register addressing mode*

Register addressing mode simply moves data in or out of a register.

---

### All about functions

Programming can either be viewed as breaking a large program down into smaller pieces until you get to the primitive functions, or incrementally building functions on top of primitives until you get the large pitcure in focus.

> Functions are perhaps the most fundamental language feature for abstraction and code reuse.

**Inorder to understand function calls, you need to understand the stack!**

when a program starts executing, a certain contiguous section of memory is set aside for the program called stack.

**When calling function, how stack works?**

Before executing a function, a program pushes all of parameters for the function onto the stack in the reverse order that the are documented. Then the program issue a `call` instruction indicating which function it wishes to start. The call instruction does two things:

First, it pushes the address of the next indtruction, which is the return address, onto the stack;

Then, it modifies the instruction pointer(%eip) to point the start of the function. So, at the time the function starts;

```
Parameter #N
...
Parameter 2
Parameter 1
Return Address <-- (%esp)
```

Now the function itself has some work to do:

First, save the current base pointer register %ebp, by doing `pushl %ebp`;

Next, it copy the stack pointer to %ebp by doing `movl %esp, %ebp`, this allows you to be able to access the function parameter(and local variables too) as fixed indexes from the base pointer.

```
Parameter N*4+4(%ebp)
...
Parameter 12(%ebp)
Parameter 8(%ebp)
Return Address <-- 4(%ebp)
old %ebp <-- (%ebp) and (%esp)
```

Next, the function reserves space on the stack for any local variable it needs by simply moving the stack pointer out of the way. e.g., we are going to need two words(remember, a word is four byte long) of memory to run a function:`subl $8, %esp`


```
Parameter N*4+4(%ebp)
...
Parameter 12(%ebp)
Parameter 8(%ebp)
Return Address <-- 4(%ebp)
old %ebp <-- (%esp) and (%ebp)
Local Variable 1 <-- -4(%ebp)
Local Variable 2 <-- -8(%ebp) and (%esp)
```

When the function is done executing, it does three things:

1. It stores its return value in %eax
2. It resets the stack to what it was when it was called(it gets rid of the current stack frame and puts the stack frame of the calling code back into effect)
3. It returns control back to wherever it was called from. This is done using the `ret` instruction, which pops whatever value is at the top of the stack, and sets the instruction pointer, %eip, to the value.

```
movl %ebp, %esp
popl %ebp
ret
```
