# Page Replacement

There would be memory **over-allocating** in multiprogramming.  
It means that even one process needs new frame for page fault, there is no left pages in system.

To resolve this, **page replacement** is used.

## Basic Concept

1. Find position of necessary page in disk
2. Find empty page frame
   1. If there is empty page frame, use that
   2. If there is no empty page frame, run replacement algorithm to find victim frame
   3. mark victim disk on disk, edit related tables
3. read new page in emptied frame and edit frame table
4. rerun user process

Note that it takes twice of time when there is no empty frame left. \(empty frame + read frame\)  
This overhead can be reduced with **dirty bit** \(**modify bit**\)

![Reference : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/9\_VirtualMemory.html](../.gitbook/assets/image%20%2810%29.png)

**Each page or frame has its own dirty bit in hardware.**

1. When victim page is selected, first check its dirty bit
2. If dirty bit is set, content of page is different from original. In this case, we have to write contents to disk before replacement.
3. If dirty bit is not set, content of page is same with its original, so we don't have to write contents to disk.

This can reduce i/o time significantly.

**Demand Paging** have to solve two important problem:

1. **Frame Allocation** Algorithm Decide how many frames would be allocated in each process
2. **Page Replacement** Algorithm Decide which page would be replaced on page replacement

Performance of page replacement can be measured by page fault count with specific memory reference sequence.

## FIFO Page Replacement

Simplest form of page replacement is FIFO Page Replacement.

It relates each page with memory load time. When page replacement required, it kicks out oldest pages.

FIFO Algorithm not always performs good. Consider below memory reference sequence

> 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5

In this sequence, there would be 10 page fault on 4 frame, while 9 page fault occurs on 3 frame.  
**Belady's anomaly** means that there is more page fault even though we increased number of frames.

## Optimal Page Replacement

// TODO





## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/9\_VirtualMemory.html" %}



