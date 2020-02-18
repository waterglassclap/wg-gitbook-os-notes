# Contiguous Memory Allocation

Usually memory is separated into **1. os** \(which always stays\) **2. user processes**  
Os process usually allocated nearby Interrupt vector **\(interrupt vector usually has address 0\).**

## Memory Protection

![](../.gitbook/assets/image%20%2821%29.png)

**Memory protection** can be done with **reallocation register** and **limit register**.

1.**Reallocation Register** saves **minimum physical address**  
2. **Limit Register** saves **range of logical address. Every logical address should be smaller than limit register.**

MMU converts addresses with adding reallocation register to logical address.

When CPU chooses next process, dispatcher loads reallocation register / limit register.  
Every addresses created by CPU is refer to this registers. That is, it protects one process from another processes or os.

## Memory Allocation

Simplest way of memory allocation is to separate memory into partitions with same fixed size. This is not used for modern os.

Alternative approach is to keep table which marks memory usage.

1. Initially, all memory space is considered as one big free space.
2. When process enters system, os put the process into input queue.
3. Then, os finds out which / how much free space exists and how much space process requires, and allocates memory to process.
4. Once process gets memory, it competes with another process to take up CPU.
5. Once process is over, it returns its memory space.

### Dynamic Storage Allocation Problem

Dynamic Storage Allocation problem is to optimize memory allocation with n-byte memory block request \(with arbitrary free space list\).

1. **First Fit** Allocate first space which have enough space for request.
2. **Best Fit** Allocate smallest space of spaces which have enough space for request.
3. **Worst Fit** Allocate biggest space of spaces which have enough space for request.

With simulation, it is identified that first fit or best fit is better than worst fit, both in time and space.  
First fit and best fit cannot compete on space efficiency, but in time efficiency, generally first fit is faster than best fit. 

## Fragmentation

### External Fragmentation

With repeating allocation / deallocation of memory, some fragments becomes too small.  
If some memory fragments are too small individually, but big enough in total, we call it as **External Fragmentation**.

In First Fit, statistically, when N blocks are allocated, 0.5N blocks is useless because of external fragmentation. This is called **50-percent rule.**

One of the ways to solve this problem is **compaction**. Another way is to allocate each process' address space far enough.

### **Internal Fragmentation**

In general, we divide memory with certain size of fragments, and allocates adequate number of fragments.  
In this strategy, some fragments have leftover space. We call it as **Internal Fragmentation**.

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}





