# Copy on Write

note that fork\(\) system call is copying parent process to child process.

We don't have to copy all pages from process when child process created, as most of the child process calls exec\(\) immediately \(which does not require copying\)

![References : https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/9\_VirtualMemory.html](../.gitbook/assets/image%20%2833%29.png)

**copy-on-write** means that **page copy is created when one of two process write on shared page**.

## References

{% embed url="https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/9\_VirtualMemory.html" %}





