# Segmentation

Logical Memory == Set of Segments

## Basic Method

![Reference : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%281%29.png)

Usually, segment is constructed when user program is compiled.  
For example, in C compiler, there would be those segments:

1. Code
2. Global Variable
3. Heap
4. Stack
5. Standard C library

## Hardware Support

![Reference: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html](../.gitbook/assets/image%20%2837%29.png)

Though user can access segment with 2-dimensional address,  
actually physical address is 1-dimensional address \(of course\).

That is, user-defined 2-dimensional address should be converted into 1-dimensional physical address. **Segment Table** can do this.





## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/8\_MainMemory.html" %}





