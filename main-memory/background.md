# Background

## Basic Hardware

**Main memory** and **Registers** are **the only storage CPU directly access.**  
That is, every operators and datas executed have to be in main memory or registers.  
If not, data have to be moved to memory before executed.

**Registers** **in CPU** are accessible in **one cycle in CPU clock**.  
**Datas in Main memory** consumes **many cycles**.  
To reduce this gap, there is **Cache buffer between them**.

To protect each process from one another, there are some hardware supports.  
First, **each process has own independent memory space**.  
there are **base register** and **limit register** to mark space range. E.g. if base register == 300040, limit register == 120900, process can access memory from 300040 to 420940.  


// TODO

## Logical Versus Physical Address Space

**Logical Address** : address created by **CPU**  
**Physical Address** : address managed by **Memory**

**Compile Time linking :** Logical Address **==** Physical Address  
**Load Time Linking** : Logical Address **==** Physical Address  
**RunTime Linking** : Logical Address **!=** Physical Address

In Runtime Linking, we call **logical address as virtual address**. 

Mapping between **virtual address** &lt;-&gt; **physical address** is managed by **MMU** \(Memory Management Unit\)

## Dynamic Loading

To utilize memory space, we have to use dynamic loading.  
**In dynamic loading, each routine waits in disk until it actually called.**

First, main routine is loaded into memory and executed. Once it calls another routine, system examines whether it is loaded to memory.  
If not,  **Relocatable Linking Loader** is called and loads routine into memory, and program continues.

## Dynamic Linking & Shared Libraries

**In dynamic linking, linked routine is not linked until it actually called.**  
If system does not use dynamic linking, each program should have system libraries' copy or linked libraries' copy. It might waste disk space and main memory.

When program calls library, **Stub** is created.  
**Stub is small piece of code which indicates how to find or load library.**  
First it examines memory whether library routine is already in memory. If not, it loads routine to memory.  
For example, if printf\(\) is used in 10 process, one printf\(\) code is necessary.

Unlike dynamic loading, dynamic linking should be supported by os, because, only os can figure out which routine locates in memory as each processes are saved from one another.

## Swapping

If necessary, process can be swapped to sub-memory and swapped back to main memory again.

Considering round-robin scheduling multiprogramming environment.  
If one 

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}



