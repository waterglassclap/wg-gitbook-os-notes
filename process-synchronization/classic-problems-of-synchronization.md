# Classic Problems of Synchronization

In these situations, deadlock and starvation might occur

## The Bounded-Buffer Problem

### Producer

```java
import java.util.Date;

public class Producer implements Runnable {
    private Buffer buffer;
    
    public Producer(Buffer buffer) {
        this.buffer = buffer;
    }
    
    public void run() {
        Date message;
        while(true) {
            // nap for awhile
            SleepUtilities.nap();
            // produce an item & enter it into the buffer
            message = new Date();
            buffer.insert(message);
        }
    }
}
```

### Consumer

```java
import java.util.Date;

public class Consumer implements Runnable {
    private Buffer buffer;
    
    public Consumer(Buffer buffer) {
        this.buffer = buffer;
    }
    
    public void run() {
        Date message;
        while(true) {
            // nap for awhile
            SleepUtilities.nap();
            // consume an item from the buffer
            message = ((Date) buffer).remove();
        }
    }
}
```

### Factory

```java
public class Factory {
    public static void main(String args[]) {
        Buffer server = new BoundedBuffer();
        
        // now create the producer and consumer threads
        Thread producerThread = new Thread(new Producer(server));
        Thread consumerThread = new Thread(new Consumer(server));
        
        producerThread.start();
        consumerThread.start();
    }
}
```

## The Readers-Writers Problem

One database is shared between multiple processes.  
Some processes only reads db \(Reader\), other processes read/write db \(Writer\).

If Reader and Reader simultaneously access db, it does not make problem.  
If writer and writer \(or reader\) process simultaneously access db, it might be a problem.

To solve this problem, writer process should have exclusive authority. This is called Readers-Writers problem.

1. any reader should not be wait, when no writer accessing db.
2. when writer is ready, it should be started asap.

Note that in 1\), writer can be on starvation, and in 2\), reader can be on starvation.

### Reader

```java
public class Reader implements Runnable {
    private RWLock db;
    
    public Reader(RWLock db) {
       this.db = db;
    }
    
    public void run() {
        while(true) {
            // nap for awhile
            SleepUtilities.nap();
            
            db.acquireReadLock();
            
            // you have access to read from the database
            SleepUtilities.nap();
            
            db.releaseReadLock();
        }
    }
}
```

### Writer

```java
public class Writer implements Runnable {
    private RWLock db;
    
    public Writer(RWLock db) {
        this.db = db;
    }
    
    public void run() {
        while(true) {
            SleepUtilities.nap();
            
            db.acquireWriteLock();
            
            // you have access to write to the database
            SleepUtilities.nap();
            
            db.releaseWriteLock();
        }
    }
}
```

### RWLock Interface

```java
public interface RWLock {
    public abstract void acquireReadLock(int readerNum);
    public abstract void acquireWriteLock(int writerNum);
    public abstract void releaseReadLock(int readerNum);
    public abstract void releaseWriteLock(int writeNum);
}
```

### Database

```java
public class Database implements RWLock {
    private int readerCount;
    Semaphore mutex;
    Semaphore db;
    
    public Database() {
        readerCount = 0;
        mutex = new Semaphore(1);
        db = new Semaphore(1);
    }
    
    public void acquireReadLock() {
        mutex.acquire();
        ++readerCount;
        
        // if I am the first reader tell all others
        // that the database is being read
        if (readerCount == 1) {
            db.acquire();
        }
        mutex.release();
    }
    
    public void releaseReadLock() {
        mutex.acquire();
        --readerCount;
        
        // if I am the last reader tell all others
        // that the database is no longer being read
        if (readerCount == 0) {
            db.release();
        }
        mutex.release();
    }
    
    public void acquireWriteLock() {
        db.acquire();
    }
    
    public void releaseWriteLock() {
        db.release();
    }
}
```

This kind of Reader-Writer lock is useful when:

* Easy to recognize reader process and writer process
* Number of Reader process is more than number of writer process. Generally, reader-writer lock overhead is bigger than semaphore or mutex, and this can be cancelled out with increasing efficiency with parallel reader works.

## The Dining-Philosophers problem

```java
while(true) {
   // get left chopstick
   chopStick[i].acquire();
   // get right chopstick
   chopStick[(i + 1) % numPil].acquire();
   
   eating();
   
   // return left chopstick
   chopStick[i].release();
   // release right chopstick
   chopStick[(i + 1) % numPil].release();
   
   thinking();
}
```



