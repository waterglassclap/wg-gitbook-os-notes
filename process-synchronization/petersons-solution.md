# Peterson's Solution

Peterson's solution requires 2 data item shared with 2 processes

```c
int turn;
boolean flag[2];
```

if **turn == i**, **Process\[i\] can run** in critical section.  
if **flag\[i\] == True**, **Process\[i\] is ready** to enter critical section.

#### Process i code

```c
while(true) {
  flag[i] = TRUE;
  turn = j;
  
  while(flag[j] && turn == j) {
    // do nothing
  }
  // critical section
  ...
  flag[i] = FALSE;
  // remainder section
  ...
}
```

#### Process j code

```c
while(true) {
  flag[j] = TRUE;
  turn = i;
  
  while(flag[i] && turn == i) {
   // do nothing
  }
  // critical section
  ...
  
  flag[j] = FALSE;
  // remainder section
  ...
}
```

1. **Mutual Exclusion** \(if Process1 runs in its critical section, other processes cannot be run in their critical sections\)  **proof\)** Let's say flag\[0\] == flag\[1\] == true.  As variable "turn" can only have one value at one time, only one process can pass while condition and enters critical section.  Lets say turn == j and Process\[j\] enters critical section. Then Process\[i\] runs "line 5" one more time.  one that moment, as flag\[j\] == true and turn == j, Process\[i\] cannot enter critical section.  
2. **Progress proof\)** d ****
3. **Bounded waiting proof\)** // TODO

