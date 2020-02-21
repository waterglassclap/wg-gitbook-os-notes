# Methods for Handling Deadlocks

There are two ways handling deadlocks, guaranteeing that deadlock will not occur

1. Prevention
2. Avoidance

Prevention is to prevent one of the four condition.  
Avoidance requires process to provide resource usage plan.

If system do not uses any of this, system investigate if deadlock really occurred, if deadlock occurred, system restore itself with some algorithms

In many system deadlock occurs rarely\(so to speak, once in a year\). That is, restoring can be much more cheaper than prevention / avoidance.

For example, JVM does nothing to resolve deadlock. It is programmer's job to write deadlock-free program.

## Deadlock Detection

### Single Instance of Each Resource Type

If every resource has one instance, we can define deadlock detection with wait-for graph, describing resource allocation graph.

![\(a\) Resource allocation graph. \(b\) Corresponding wait-for graph](../.gitbook/assets/image%20%2847%29.png)

Only if there is cycle in this graph, there is deadlock.  
Time complexity is **O\(n^2\)**, where n is vertices count.

### Several Instances of a Resource Type

Wait-for graph cannot be used on multiple instances in one resource type.  
We can use Allocation - Request - Available Vector Table for this.

For example

|  | Allocation | Request | Available |
| :--- | :--- | :--- | :--- |
|  | A B C | A B C | A B C |
| P0 | 0 1 0 | 0 0 0  | 0 0 0  |
| P1 | 2 0 0 | 2 0 2 |  |
| P2 | 3 0 3 | 0 0 0 |  |
| P3 | 2 1 1 | 1 0 0 |  |
| P4 | 0 0 2 | 0 0 2 |  |

In this graph A, B, C are resources and P0 - P4 are processes.

* **Available** : How many instances are available for each resources
* **Allocation** : Which and how many instances are allocated for each processes
* **Request** : How many instances are requested for each processes, per each resources

Let's say there are **m resources**, **n processes**.  
Detection Algorithms is as follows

```python
# 

# 1.

Work = Available[:]
Finish = [ Allocation[i] == 0 for i in range(n) ]

# 2. find i which meets
Finish[i] == false and Request[i] <= Work
# if i not exists, go to step 4

# 3.
Work = Work + Allocation
Finish[i] = true
# and go to step 2

# 4.
for i in range(n):
    if Finish[i] is False:
        # P[i] is in deadlock
        print("P[i] is in deadlock")
```

Time complexity is **O\(m x n^2\)**

## **Recovery from Deadlock**

### Process Termination

1. **Terminate All deadlock processes** It surely breaks deadlock cycle, but all processes have to resume it's work, so cost might be too high.
2. **Terminate processes one by one until deadlock resolved** We have to check if deadlock resolved every time we terminates process, so overhead might be quite big.

Os have to decide which solution would minimize cost.

### Resource Preemption

If preemption is needed for resolve deadlock, there are three things to consider:

1. **Selection of a victim** Which resources and which process should be preempted?
2. **Rollback** How to preempt resources from one process ?
3. **Starvation** How to prevent starvation on resource preemption ? General solution is that considering rollback count on selection on victim.

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/7\_Deadlocks.html" %}





