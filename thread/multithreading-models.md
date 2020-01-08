---
description: models managing user threads / kernel threads
---

# Multithreading Models

## Many to One Model

![](../.gitbook/assets/image%20%2826%29.png)

#### Pros

* Thread management is handled by the thread library in user space, which is very efficient

#### Cons

* If a blocking system call is made, then the entire process blocks
* Because a single kernel thread can operate only on a single CPU, it does not allow individual processes to be split across multiple CPUs

## One to One Model

![](../.gitbook/assets/image%20%2827%29.png)

#### Pros

* One-to-one model overcomes the problems listed above involving blocking system calls and the splitting of processes across multiple CPUs

**Cons**

* The overhead of managing the one-to-one model is more significant, involving more overhead and slowing down the system.
* Most implementations of this model place a limit on how many threads can be created

## Many to Many Model

![](../.gitbook/assets/image%20%2829%29.png)

**Pros**

* Users have no restrictions on the number of threads created.
* Blocking kernel system calls do not block the entire process.
* Processes can be split across multiple processors.
* Individual processes may be allocated variable numbers of kernel threads, depending on the number of CPUs present and other factors.

Some system mixes Many-to-Many with One-to-One

## References

[https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/3\_Processes.html](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4_Threads.html)

[https://blog.naver.com/myca11/221224081981](https://blog.naver.com/myca11/221224081981)

