# Semaphores

**Semaphore** is synchronization tool

* Semaphore includes integer **value**
* Except for initialization, process can access to semaphore only with 2 function: **acquire\(\)**, **release\(\)**

**acquire\(\)**

```c
acquire() {
    while(value <= 0) {
        // do nothing
    }
    value--;
}
```

**release\(\)**

```c
release() {
    value++;
}
```

#### Conditions

* **Changing semaphore "value" should not be done separately**. That is, If one thread changes semaphore value, any other thread cannot be change same semaphore value at same time.
* **acquire\(\) line 2** \(value &lt;= 0\) and **line 5** \(value--;\) **should not be interrupted**.

## Usage

There are two types of semaphore

* **Counting** semaphore value has no limit
* **Binary** \(**Mutex lock**\) semaphore value can be 0 or 1

```java
Semaphore S = new Semaphore();
S.acquire();
// 임계영역
S.release();
// 나머지 영역
```

#### **Java Thread example**

```java
public class Worker implements Runnable {
    private Semaphore sem;
    private String name;
    
    public Worker(Semaphore sem, String name) {
        this.name = name;
        this.sem = sem;
    }
    
    public void run() {
        while (true) {
            sem.acquire();
            MutualExclusionUtilities.criticalSection(name);
            sem.release();
            MutualExclusionUtilities.nonCriticalSection(name);
        }
    }
}

public class SemaphoreFactory {
    public static void main(String args[]) {
        Semaphore sem = new Semaphore(1);
        Thread[] bees = new Thread[5];
        for (int i = 0; i < 5; i++) {
            bees[i] = new Thread(new Worker(sem,
                                 "Worker" + (new Integer(i)).toString()));
        }
        for (int i = 0; i < 5; i++) {
            bees[i].start();
        }
    }
}
```

#### Another Example

If there's **P1: contains S1**, **P2 : contains S2**,  
and **S2 should follow S1**:

```java
Semaphore synch = new Semaphore(0);

// P1
S1;
synch.release();
...

// P2
synch.acquire();
S2;
...
```

## Implementation

Major drawback of above approach is that every process needs **busy waiting.**  
That is, if one process is in their critical section, all other process have to run its entry section over and over again.  
Busy waiting wastes CPU time of waiting processes.  
This kind of semaphore is called **Spinlock**  
\(Spinlock is useful when context switching takes long time comparing to critical section time\)

To prevent busy waiting, we newly define Semaphore as:

```java
acquire() {
    value--;
    if (value < 0) {
        // put this process to list / queue
        block();
    }
}

release() { 
    value++;
    if (value <= 0) {
        // pop one process from list / queue = P
        wakeup(P);
    }
}
```

* **block\(\)** call postpone a process itself
* **wakeup\(P\)** call resume process P

Waiting queue \(with PCB\) can be fifo queue, list, or any other thing.

In this implementation, semaphore's value can have minus value \(previous one don't\)  
If semaphore's value haver minus value = -n, it means that n process is waits for semaphore.

**Most important thing about semaphore is it's call should be atomic.  
That is, we have to guarantee that acquire\(\) and release\(\) cannot be called at the same time.**

**In single processor** env, **simply preventing interrupt call during acquire / release** call will do.  
**In multi processor** env, **we have to prevent interrupt call for all processors**. If hardware does not support this, we have to consider special software solution \(6.2\)



Note that we did not solve busy waiting.  
Rather, we move busy waiting from entry section to critical section.  
But, critical section is quite short \(if properly designed, &lt; 10 line\), so, critical section is empty for most of the time, and busy waiting takes quite short time.

## Deadlock and Starvation

### Deadlock

| P0 | P1 |
| :---: | :---: |
| acquire\(S\); | acquire\(Q\); |
| acquire\(Q\); | acquire\(S\); |
| ... | ... |
| release\(S\); | release\(Q\); |
| release\(Q\); | release\(S\); |

P0 waits release\(Q\) to acquire\(Q\)  
P1 waits release\(S\) to acquire\(S\)

### Starvation

Infinite blocking or starvation means some process infinitely waits on queue. This can be happened on LIFO queue, for example.

## References

{% embed url="https://stackoverflow.com/questions/29213346/working-with-threads-and-a-semaphore-in-java-how-does-acquire-work" %}

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/5\_Synchronization.html" %}













\*\*\*\*

\*\*\*\*

