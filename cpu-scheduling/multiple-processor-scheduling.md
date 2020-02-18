# Multiple Processor Scheduling

## Approaches to Multiple Processor Scheduling

Multiple processor can be manipulated as:

1. **Asymmetric Multiprocessing** : Master - Slave. master handles scheduling / IO handling / other system activities, while slaves runs user code. This is relatively simple, as only one processor can access to system data structure.
2. **Symmetric Multiprocessing \(SMP\)** every processor choose its own scheduling. Every process can be in one ready queue, or each processor-separated queues. Almost every OS supports Symmetric Multiprocessing.

## Processor Affinity

Each Processor has its own cache. When process 1 runs on processor 1, it is likely to be in processor 1's cache, therefore, decreases cost. When process 1 moves from processor 1 to processor 2, processor 1's process 1 cache should be invalidated, and processor 2 cache should be filled with process 1.  
So, most of the SMP system avoids process move from processor to another processor, and tends to **run same process in same processor**. This is called "**Processor Affinity**"

* **Soft Affinity** : When OS tends to run same process in same processor but not guarantees it
* **Hard Affinity** : Process cannot leave its first processor. some system like Linux supports this call for special process.

## Load Balancing

* **push migration** : specific task checks each processor's load periodically, and when processor is too busy, push processes to another processor
* **pull migration** : not busy processor pulls job from another processor

push / pull migration are not necessarily exclusive.

Note that load balancing sometimes against processor affinity. So, in some system there is some threshold that load balancing can be happened.

## Symmetric Multithreading

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2843%29.png)

Symmetric multithreading, \(so called hyperthreading in intel\) is to provide multiple logical processor in same physical processor.

Each logical processor has **its own architecture state** \(general / machine-state registers\), **supports interrupt over logical processors**.

**Symmetric multithreading should be supported by hardware**, that is, hardware can mark each logical processor's interrupt handling / architecture status.

## References

[https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6_CPU_Scheduling.html)

