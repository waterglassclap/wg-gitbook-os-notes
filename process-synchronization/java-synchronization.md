# Java Synchronization

When one application access with multiple thread **concurrently**, and data consistency is preserved, we call this **Thread Safe**

## **Busy Waiting**

We described busy waiting in semaphore section:

> Major drawback of above approach is that every process needs busy waiting  
> ****That is, if one process is in their critical section, all other process have to run its entry section over and over again.  
> Busy waiting wastes CPU time of waiting processes.

To solve this, process waiting queue is one option. In Java, **Thread.yield\(\)** will do this.

But, consider this scenario:  
\(Note that JVM prefers high priority process than low priority process in scheduling\)

1. Producer has high priority than Consumer
2. Buffer is full
3. Producer yield\(\) \(or busy wait\) until count &lt; BUFFER\_SIZE

As consumer has low priority than producer, Consumer will never be scheduled with JVM.  
This situation called **Livelock**

## Race Condition

We described race condition in background section:

> Condition that multiple process manipulating to same data and result of the operation depends on the sequence of executing each commands is called "**Race Condition**"

In Java, we use **synchronized** keyword for this.

Before we go, note that

* Every object in java is related to one lock
* Object's Lock owned by one Thread

When one method defined with synchronized and called, it requires lock of this object.

If Thread A calls synchronized method and another thread B owns object O's lock,  
thread A is blocked and put in entry set for object O.

When thread ends method, object O's lock is released.

When lock is released, JVM chooses random\(?\) thread of object O's entry set.

```java
// Entry set insert / lock implementation

public synchronized void insert(Object item) {
    while (count == BUFFER_SIZE) {
        Thread.yield();
    }
    ++count;
    buffer[in] = item;
    in = (in + 1) % BUFFER_SIZE;
}

public synchronized Object remove() {
    Object = item;
    
    while (count == 0) {
        Thread.yield();
    }
    
    --count;
    item = buffer[out];
    out = (out + 1) % BUFFER_SIZE;
    
    return item;
}
```

## Deadlock

1. Consider that buffer is full, and consumer is in sleep status
2. If producer calls insert\(\) \(as lock is usable\) producer is allowed to proceed
3. when producer calls insert\(\), as buffer is full, producer calls yield\(\)
4. Though, producer still has lock
5. When consumer awaken and try to call remove\(\), as producer has lock, consumer cannot call remove\(\), so buffer remained full.

This is one example how yield\(\) makes deadlock

#### Wait and Notify

![](../.gitbook/assets/image%20%2811%29.png)

Each Object in Java has "**wait set**", "**entry set**" of threads.  
When Thread goes to synchronized method, thread has object's lock.  
If Thread cannot proceed \(like buffer is full, and producer cannot produce\), thread releases its lock and goes to its "wait set", to prevent deadlock.

  
when **wait\(\)** called

1. Thread releases monitor's lock \(which called by synchronized\)
2. Thread status goes to "blocked"
3. Thread goes to object's wait set

when **notify\(\)** called

1. choose arbitrary Thread T from wait set
2. move T from wait set to entry set
3. change T's status from blocked to runnable



```java
public synchronized void insert(Object item) {
    while (count == BUFFER_SIZE) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    ++count;
    buffer[in]= item;
    in = (in + 1) % BUFFER_SIZE;
    
    notify();
}

public synchronized Object remove() {
    Object item;
    
    while (count == 0) {
        try {
            wait();
        } catch (InterruptedException e) {}
        
        --count;
        item = buffer[out];
        out = (out + 1) % BUFFER_SIZE;
        
        notify();
        
        return item;
    }
}
```







## References

{% embed url="https://app.gitbook.com/@waterglassclap/s/pl-notes/java/java-singleton" %}

{% embed url="https://www.baeldung.com/java-wait-notify" %}

{% embed url="http://egloos.zum.com/iilii/v/5565036" %}







