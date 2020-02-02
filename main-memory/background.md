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


In Runtime Linking, 

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}



