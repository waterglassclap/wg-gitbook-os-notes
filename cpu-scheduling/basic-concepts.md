# Basic Concepts

CPU Scheduling is to utilize CPU at most. Maximum utilization might mean:  
1. Schedule jobs by their priority  
2. Prevent starvation  
3. Reduce average duration for all job

## CPU-I/O Burst Cycle

![source: https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2820%29.png)

Process operation = CPU operation + I/O operation.   
Process starts with CPU Burst. Then I/O Burst occurs, and another CPU burst ,.. and so on.  
CPU burst duration time varies from systems / processes, but usually it shows exponential distribution.  
I/O Bound task might have comparatively many short CPU burst.  
CPU Bound task might have comparatively many long CPU burst. 

+ cpu bound job wiki example

## CPU Scheduler

Short term scheduler chooses a process in ready queue when CPU is idle.  
Note that ready queue is not necessarily be FIFO queue. It can be FIFO queue, Priority Queue, Tree, or just simple linked list.

## Preemptive Scheduling

Cpu Scheduling can be occurred in 4 states:

1. When a process switches **from the running state to the waiting state**, such as for an **I/O request** or invocation of the **wait\( \) system call**
2. When a process switches **from the running state to the ready state,** for example in response to an **interrupt**
3. When a process switches **from the waiting state to the ready state**, say at **completion of I/O** or a **return from wait\( \)**
4. When a **process terminates**

and we divided type of scheduling as:

1. **Non-preemptive \(Cooperative\)** : when scheduling occurs only in **1,4**
2. **Preemptive** : Scheduling can be occurred in any step

In non-preemptive scheduling, once one process occupies CPU , it occupies until process terminates or changes to wait state. Non-preemptive scheduling used until Windows 95.

after Window 95 / OS X uses preemptive scheduling.

In preemptive scheduling, there are two troublesome points:

1. **Cost over access control on shared resources** when one process updating data, other process can read inconsistent data.
2. **System call handling** what if some process includes important kernel changes \(like I/O queue\) occupies CPU, while system call handles same system ? -&gt; Most of UNIX / other OS waits for system call or I/O blocking, and operates context switch after that. \(Unfortunately, this model is not adequate for real-time computing or multiprocessing. Discussed in 5.4 / 19.5\)

## Dispatcher

Another module for CPU scheduling is dispatcher:

1. Context Switching
2. Convert to User Mode
3. Jump to right position of user program, for restarting program

Dispatcher call occurs every processes' context switch call, so it has to be done asap. **Dispatch latency** : old process stop time + new process start time

## References

[https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6_CPU_Scheduling.html)

##  



