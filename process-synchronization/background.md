# Background

Considering Finite Buffer Problem

#### Producer

```c
while( count == BUFFER_SIZE ) {
// do nothing
}
++count;
buffer[in] = item;
in = (in + 1) % BUFFER_SIZE;
```

#### Consumer

```c
while( count == 0 ) {
// do nothing
}
--count;
item = buffer[out];
out = (out + 1) % BUFFER_SIZE;
```

If we run this code in parallel, it does not work well.

Producer code 4 would be translated as

```c
register1 = count
register1 = register1 + 1
count = register1
```

Note that register1 is local register which one CPU can access to.

Consumer Code 4 would be translated as

```c
register2 = count
register2 = register2 - 1
count = register2
```

That is, above code could be executed as

```c
register1 = count // producer. register1 == 5
register1 = register1 + 1 // producer. register1 == 6
register2 = count // consumer. register2 == 5
register2 = register2 - 1 // consumer register2 == 4
count = register1 // producer. count == 6
count = register2 // consumer. count == 4
```

That is, count is 4 although actual buffer size == 5. Guaranteeing that only one process access to variable "count" at one time matters.

Condition that multiple process manipulating to same data and result of the operation depends on the sequence of executing each commands is called "**Race Condition**"

## References

[https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/6\_CPU\_Scheduling.html](https://www2.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/5_Synchronization.html)





