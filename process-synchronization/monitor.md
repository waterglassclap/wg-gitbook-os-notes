# Monitor

If some in-corporative programmer

* changes acquire / release sequence

```text
mutex.release();
...
// critical section
...
mutex.acquire();
```

* write acquire on release

```java
mutex.acquire();
...
// critical section
...
mutex.acquire();
```

* does not write acquire / release 

dead lock might occur.

To prevent this common problems, Researchers developed high-class constructs like **Monitor**

## **Usage**

![](../.gitbook/assets/image%20%2833%29.png)

![](../.gitbook/assets/image%20%2814%29.png)

Monitor is class. ****Restriction is that **only one method within any given monitor object may be active at the same time**

We can define condition variable in monitor:

```java
condition x, y;
```

![](../.gitbook/assets/image%20%2816%29.png)

For conditional variable, only two action is allowed:

1. wait\(\)
2. signal\(\)

Process which call **wait\(\)** should wait until another Process calls **signal\(\)  
signal\(\)** activates **exactly** one process. If there is no process delayed, signal\(\) takes on effect \(unlike semaphore\)

Consider that process **P calls x.signal\(\)**, and another process **Q related to x** exists.  
Clearly, **To activate Q, P should be waiting**. Unless, P and Q are activated in monitor at the same time.

There are two options to implement this:

1. **Signal and Wait** P should be waiting until Q leaves monitor or waits for another condition.
2. **Signal and Continue** Q should be waiting until P leaves monitor or waits for another condition.

## Solve Dining Philosophers Problem with Monitor

To solve dining philosophers problem,   
First, define three status of philosophers

```java
enum State { THINKING, HUNGRY, EATING };
State[] states = new State[5];
```

One philosopher can set its state **states\[i\]** with **State.EATING**,  
only when **both neighbors are not at EATING** status.

Also, we define monitors' condition variables

```java
Condition[] self = new Condition[5];
```

Finally, philosophers proceed in this way

```java
dp.takeForks(i);
eat();
dp.returnForks(i);
```

With this prerequisites, we can solve Dining philosophers problems:

```java
monitor DiningPhilosophers {
    enum State { THINKING, HUNGRY, EATING };
    State[] states = new State[5];
    Condition[] self = new Condition[5];
    
    public DiningPhilosophers {
        for (int i = 0; i < 5; i++) {
            states[i] = State.THINKING;
        }
    }
    
    public void takeForks(int i) {
        states[i] = State.HUNGRY;
        test(i);
        if (states[i] != State.EATING) {
            self[i].wait();
        }
    }
    
    public void returnForks(int i) {
        states[i] = State.THINKING;
        test((i + 4) % 5);
        test((i + 1) % 5);
    }
    
    private void test(int i) {
        if ((states[(i + 4) % 5] != State.EATING) &&
            (states[i] == State.HUNGRY) &&
            (states[(i + 1) % 5] != State.EATING)) {

            states[i] = State.EATING;
            self[i].signal();
        }
    }
}
```

Note that this code might cause starvation \(How to solve this?\)

## **References**

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/5\_Synchronization.html" %}

{% embed url="https://tiredsleeper.tistory.com/38" %}

\*\*\*\*

