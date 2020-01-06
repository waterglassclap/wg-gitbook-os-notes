# Java Synchronization - Problems

## Bounded Buffer

```java
public class BoundedBuffer implements Buffer {
    private static final int BUFFER_SIZE = 5;
    
    private int count, in, out;
    private Object[] buffer;
    
    public BoundedBuffer() {
        count = 0;
        in = 0;
        out = 0;
        buffer = new Object[BUFFER_SIZE];
    }
    
    // insert
    public synchronized void insert(Object item) {
        while (count == BUFFER_SIZE) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        ++count;
        
        buffer[in] = item;
        in = (in + 1) % BUFFER_SIZE;
    
        notify();
    }
    
    // remove
    public synchronized Object remove() {
        Object item;
    
        while (count == 0) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        
        --count;
            
        item = buffer[out];
        out = (out + 1) % BUFFER_SIZE;
        
        notify();
        
        return item;
    }
}
```

## Multiple Notification

Considering Threads {T0, T1, T2, T3, T4} and variable "turn", indicates which thread have to work.  
T'work' can only be proceed, other thread have to wait until their turn.

```java
public synchronized void doWork(int myNumber) {
    while (turn != myNumber) {
        try {
            wait();
        } catch (InterruptedException e) {}
    }
    
    // do some work for awhile
    
    // Finished working. No indicate to the
    // next waiting thread that it is their
    // turn to do some work.
    
    turn = (turn + 1) % 5;
    
    notifyAll();
}
```

note that **notify\(\)**  can only choose arbitrary thread.  
another call **notifyAll\(\)** can wake all threads on wait set.

## Reader-Writers Problem

```java
public class Database implements RWLock {
    private int readerCount;
    private boolean dbWriting;
    
    public Database() {
        readerCount = 0;
        dbWriting = false;
    }
    
    public synchronized void acquireReadLock(int readerNum) {
        while (dbWriting == true) {
            try { 
                wait();
            } catch(InterruptedException e) { }
        }
        ++readerCount;
    }
    
    public synchronized void releaseReadLock(int readerNum) {
        --readerCount;
        
        // if I am the last reader tell all others
        // that the database is no longer being read
        if (readerCount == 0) {
            notify();
        }
    }
    
    public synchronized void acquireWriteLock(int writerNum) {
        while (readerCount > 0 || dbWriting == true) {
            try {
                wait();
            } catch (InterruptedException e) {}
        }
        
        // once there are either no readers or writers
        // indicate that the database is being written
        dbWriting = true;
    }
    
    public synchronized void releaseWriteLock(int writerNum) {
        dbWriting = false;
        
        notifyAll();
    }
}
```



## References



