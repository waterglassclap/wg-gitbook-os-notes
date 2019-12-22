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

![](../.gitbook/assets/image%20%2819%29.png)

![](../.gitbook/assets/image%20%287%29.png)

Monitor is class. ****Restriction is that **only one method within any given monitor object may be active at the same time**

\*\*\*\*

\*\*\*\*

\*\*\*\*

## **References**

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/5\_Synchronization.html" %}

\*\*\*\*

