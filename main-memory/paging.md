# Paging

Paging removes constraints that logical address space should be gathered in one consecutive space.

## Basic Method

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2817%29.png)

Physical memory is divided into **Frame** with fixed size.  
Logical memory is divided into **Page,** which has **same size with frame**.

![](../.gitbook/assets/image%20%282%29.png)

Every Address comes from CPU is consist of 1. page number 2. page offset

1. **page number** for accessing page table. page table has base address of page in main memory.
2. **page offset** pageTable\[page number\] + page offset =&gt; physical address for memory device.

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%288%29.png)

Above picture is example of 4B size paging with 32B memory.

**With paging, there are no external fragmentation. But internal fragmentation can be happened.**  
In average, there are **half page size** of internal fragmentation per process.

**With reducing size of page size:  
internal fragmentation size is decreased, but page table space is increased.**

In general,

1. page size**: 2~8KB**
2. each item in page table : **4B**

OS should know about physical memory allocation. There are **frame table** for this.  
Frame table has 1. is available or allocated 2. if allocated, which page has this frame.

OS have copy of each process' page table. Every time OS tries to convert logical address to physical address, OS use this table.

## Hardware Support

**Most of OS allocates each page table per process.**  
Pointers for page table saved in PCB, just like other register values. ****When dispatcher loads these registers, page table becomes available.

Simplest way of supporting page table is using exclusive register set.  
This is useful when page table is small \(&gt;= 256\).

Modern computer have page table containing 1 million items, so using exclusive register set is too costly.  
So, most of the modern computer uses **PTBR \(Page Table Base Register\)**, which points page table, and **save page table in main memory.**

This reduces context switching time, but there are some side effects.  
If user wants to access to memory\[i\], user have to:  
    1. access to page table in memory  
    2. access to real address in memory with frame number  
so there are 2 times of memory access.

### TLB

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%286%29.png)

Standard way to solve this is to use **small hardware cache**, called **TLB**\(Translation Look-aside buffers\)  
TLB is consist of fast associative memory. Items in TLB is in key : value form.  
  
When request comes to TLB, it simultaneously compares all keys to find page number.  
When page number is matched, it returns frame number.  
TLB is quite costly, and size varies from 54 ~ 1024.

Usually, TLB contains only part of page table. There are many ways to implement TLB, from LRU or arbitrary.

Some TLB saves **ASID**s\(Address-Space Identifiers\) for each item.  
ASID indicates which TLB item is belong to \(process\), and protects address space of process.

Hit Ratio means probability of finding page number in TLB.

## Protection

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2835%29.png)

In page environment, memory protection is implemented with **protection bits** for each frame.  
These bits are usually included in page table.  
If write request comes for read-only memory, hardware trap is conveyed to OS.

There are **valid / invalid bit** on each item of page table.  
If this bit set as valid, it means that this page is legal. If this bit set as invalid, it means that this page is not included in process' logical address space.  
That is, illegal address can be found with valid / invalid bit.

Some system uses **PTLR \(Page Table Length Register\)** to measure page table size.  
Every logical address is compared with PTLR value to check range. If it's not in range, trap occurred.

## Shared Pages 

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2810%29.png)

Another advantage of paging is that it makes sharing common code easy.  
Consider 40 users runs editor program, and editor takes 150KB codes and 50KB data space.  
Without sharing, it takes 200 \* 40 = 8000KB memory space.  
With sharing, it takes 150KB of shared code copy + 50 KB \* 40 of data space = 2150KB.

Note that sharing code should be reentrant routine.

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}





