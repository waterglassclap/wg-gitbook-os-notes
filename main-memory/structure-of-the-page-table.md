# Structure of the Page Table

## Hierarchical Paging

Most of the modern computer supports 2^32 ~ 2^64 bits of logical memory space.  
In this environment, page table itself becomes very big.

Considering 2^32 memory space / Page size 4KB \(2^12\).  
There would be 1 million \(2^32 / 2^12\) items in Page Table. Each item would have 4B, so total page table size would be 4MB physical space.

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2846%29.png)

In this case page table cannot be placed consecutively in main memory. We can divide page table hierarchically, like above. 

In this case \(with 4 layer of page hierarchy\), logical address would be:

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2822%29.png)

In 32-bit system, this would be enough, but in 64-bit system, there would be 7 layer of page hierarchy.  
This takes too much time on memory access, so it's not adequate.

## Hashed Page Table

Hashed Page Table is widely used on system with &gt; 32 bit address.  
Each item in hashed page table has linked list, with 3 fields:

1. Virtual Page Number
2. Projected Page Frame Number
3. Pointer for next item on Linked List

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2842%29.png)

Algorithm is as follows:

1. Hashes Virtual Page Number on Virtual Address Space
2. Compares first item \(in hashed linked list\) with Virtual Page Number
3. If matched, get physical address with page frame number
4. If not matched, continue to search on next item in linked list

## Inverted Page Table

// TODO



## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}



