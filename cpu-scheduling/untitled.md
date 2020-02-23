# Scheduling Algorithms

## First Come First Served Scheduling

| Process | Burst Time |
| :--- | :--- |
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2830%29.png)

* Preemptive
* Convoy effect : all other process waits for a long process to be ended

## Shortest Job First Scheduling

| Process | Burst Time |
| :--- | :--- |
| P1 | 6 |
| P2 | 8 |
| P3 | 7 |
| P4 | 3 |

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2851%29.png)

* Can be Non-Preemptive / Preemptive

## Priority Scheduling

| Process | Burst Time | Priority |
| :--- | :--- | :--- |
| P1 | 10 | 3 |
| P2 | 1 | 1 |
| P3 | 2 | 4 |
| P4 | 1 | 5 |
| P5 | 5 | 2 |

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2813%29.png)

* Can be Non-Preemptive / Preemptive
* **Starvation Problem \(Infinite blocking\).** Solution : **Aging**

## Round Robin Scheduling

| Process | Burst Time |
| :--- | :--- |
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%284%29.png)

* **Performance highly depends on Time slice size**
* When **Time slice is extremely small**, it called "**Processor sharing**", and it seems that each process has its own processor which performs 1/n performance of real processor theoretically \(In real world, we should consider context switching time\).
* When **Time slice is extremely big**, it is equal to "**First come First Served Scheduling**"

## Multilevel Queue Scheduling

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2811%29.png)

## **Multilevel Feedback Queue Scheduling**

![source : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](../.gitbook/assets/image%20%2827%29.png)

* Jobs can be moved from queue to queue

## References

[https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6_CPU_Scheduling.html)

