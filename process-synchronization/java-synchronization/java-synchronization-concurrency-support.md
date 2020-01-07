# Java Synchronization - Concurrency Support

## Reentrant Locks

```java
Lock key = new ReentrantLock();
key.lock();
try {
    // critical section
    // ...
} 
finally {
  key.unlock();
}
```

"Reentrant Lock" run like "semaphore".  
Thread get ReentrantLock with calling **lock\(\)** method.   
If lock is usable or thread already have access to lock, Thread owns lock.  
If lock is not usable, thread blocked until lock is usable.

## Java Semaphore

```java
Semaphore sem = new Semaphore(1);

try {
    sem.acquire();
    // critical section
    // ...
} catch (InterruptedException ie) {
    // do nothing
} finally {
   sem.release();
}
```

## Condition Variables



