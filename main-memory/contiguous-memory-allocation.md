# Contiguous Memory Allocation

Usually memory is separated into **1. os** \(which always stays\) **2. user processes**  
Os process usually allocated nearby Interrupt vector **\(interrupt vector usually has address 0\).**

## Memory Protection

![](../.gitbook/assets/image%20%2814%29.png)

**Memory protection** can be done with **reallocation register** and **limit register**.

1.**Reallocation Register** saves **minimum physical address**  
2. **Limit Register** saves **range of logical address. Every logical address should be smaller than limit register.**

MMU converts addresses with adding reallocation register to logical address.

When CPU chooses next process, dispatcher loads reallocation register / limit register.  
Every addresses created by CPU is refer to this registers. That is, it protects one process from another processes or os.

## Memory Allocation

Simplest way of memory allocation is that separate memory into partitions with same and fixed size. This is not used for modern os.

Alternative approach is to keep // TODO

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}





