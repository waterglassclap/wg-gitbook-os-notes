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

1. **Mutual Exclusion**  
   \(if Process1 runs in its critical section, other processes cannot be run in their critical sections\)  
  
   **proof\)**  
   \(Note that with state "flag\[0\] != flag\[1\]", mutual exclusion is guaranteed\)

   Let's say flag\[0\] == flag\[1\] == true.  
  
   As variable "turn" can only have one value at one time,  
   only one process can pass while condition and enters critical section.  
  
   Lets say turn == j and Process\[j\] enters critical section. Then Process\[i\] runs "line 5" one more time.  
  
   one that moment, as flag\[j\] == true and turn == j, Process\[i\] cannot enter critical section.  
  
   That is,  
   with status flag\[0\] != flag\[1\], mutual exclusion is guaranteed.  
   with status flag\[0\] == flag\[1\] == true, mutual exclusion is also guaranteed.  

2. **Progress** Let's say Process\[j\] is run in critical section, while Process\[i\] is waiting in while block. When Process\[j\] ends, it set flag\[1\] = False. As Process\[i\] does not change turn or flag in while state, it goes to critical section. ****
3. **Bounded waiting** Same with 2\). As Process\[i\] does not changes turn or flag in while state, it goes to critical section.

