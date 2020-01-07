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

```java
Lock lock = new ReentrantLock();
Condition[] condVars = new Condition[5];

for (int i = 0; i < 5; i++) {
    condVars[i] = lock.newCondition();
}

// myNumber is the number of the thread
// that wished to do some work
public void doWork(int myNumber) {
    try {
        // if it's not my turn, then wait
        // until I'm signaled
        if (myNumber != turn) {
            condVars[myNumber].await();
        }
        
        // do some work for awhile
        
        // Finished working. Now indicate to the
        // next waiting thread that it is their
        // turn to do some work
        turn = (turn + 1) % 5;
        
        condVars[turn].signal();
    } catch (InterruptedException ie) {}
    finally {
        lock.unlock();
    }
}
```

