# The Critical-Section Problem

Considering n process \(P0, P1, ..., Pn\) is running. Each Process has "**Critical Section**" code sector.

In Critical Section

* variable shared with other process is manipulated
* files can be written
* etc

While one process runs in its critical section, any other process cannot access to their critical section.  
That is, more than one process cannot be run in their critical section.

The critical section problem is designing protocol used in interprocess cooperation.

Each process request access when they enter critical section.  
Code section implementing this is called "**Entry Section**"

"**Exit Section**" follows Critical Section. The rest of the codes are called "**Remainder Section**". That is

```c
do {
  Entry Section 
  Critical Section
  Exit Section
  Remainder Section

} while (TRUE);
```

Every Solution of Critical Section should meet 3 conditions

* **Mutual Exclusion** if Process1 runs in its critical section, other processes cannot be run in their critical sections
* **Progress** If no process runs in their critical section and there is a process request access to its critical section, processes not running in their remainder section can only participate in deciding the process for critical section, and this should not be delayed forever.
* **Bounded waiting** Every process should have chance to enter critical section after \(n x process count\) time max \(?\)

For manipulating critical section, we must consider 2 types of kernel

* **Preemptive**
* **Non-Preemptive**

Clearly, on non-preemptive kernel we don't have to consider race condition on kernel data structure. 

In preemptive kernel, one process can be replaced with another process, so problem becomes more complicated.

