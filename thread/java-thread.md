# Java Thread

There are two ways to create thread in Java:

1. **extends Thread** class, overrides run\(\) method
2. **implements Runnable** class, overrides run\(\) method

Implementing Runnable is relatively simple:

```java
@Data
class Sum {
    private int sum;
}

class Summation implements Runnable
{
    private int upper;
    private Sum sumValue;

    public Summation(int upper, Sum sumValue) {
        this.upper = upper;
        this.sumValue = sumValue;
    }

    public void run() {
        int sum = 0;
        for (int i = 0; i <= upper; i++) {
            sum += i;
        }
        sumValue.setSum(sum);
    }
}
```

After creating Thread, we have to run thread with start\(\) method.  
\(NEVER run thread with run\(\) method directly\) &lt;- ?  
start\(\) methods works like this:

1. Allocates Memory
2. Initialize Thread on JVM
3. calls run\(\) method, let thread have opportunity to run by JVM

For example:

```java
public class Driver {
    public static void main(String[] args) {
        Sum sumObj = new Sum();
        int upper = Integer.parseInt(args[0]);

        Thread thrd = new Thread(new Summation(upper, sumObj));
        thrd.start();
        
        try {
            thrd.join();
            System.out.println("The sum of " + upper + " is " + sumObj.getSum());
        } catch (InterruptedException ie) {
            // do nothing
        }
    }
}
```

Java separates thread type to

1. Daemon
2. Non-Daemon

Key differences is that JVM terminates after all non-daemon work terminates.  
On JVM start, it creates several daemon threads like garbage collector.  
Creating daemon thread can be done by calling:

```java
thrd.setDaemon(true);
```

## JAVA Thread Status

![source : https://www.javatpoint.com/life-cycle-of-a-thread ](../.gitbook/assets/image%20%281%29.png)

1. **new** : Thread object created with new ...\(\); call
2. **runnable** : when start\(\) command calls thread's run\(\) method
3. **blocked** \(not runnable\) : io\(\), or sleep\(\), ....
4. **running** : thread is on work
5. **terminated** : thread done its job

## Appendix: A Multithread Solution to the Producer-Consumer Problem

```java
import java.util.Date;

public class Factory {
    public static void main(String args[]) {
        Channel<Date> queue = new MessageQueue<Date>();
    
        Thread producer = new Thread(new Producer(queue));
        Thread consumer = new Thread(new Consumer(queue));
    
        producer.start();
        consumer.start();
    }
}
```

## References

[https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4\_Threads.html](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4_Threads.html)

[https://www.javatpoint.com/life-cycle-of-a-thread](https://www.javatpoint.com/life-cycle-of-a-thread)

[https://www.os-book.com/OS9/java-dir/4.pdf](https://www.os-book.com/OS9/java-dir/4.pdf)

