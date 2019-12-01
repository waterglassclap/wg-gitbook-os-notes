# Semaphores

**Semaphore** is synchronization tool

* Semaphore includes integer **value**
* Except for initialization, process can access to semaphore only with 2 function: **acquire\(\)**, **release\(\)**

**acquire\(\)**

```c
acquire() {
    while(value <= 0) {
        // do nothing
    }
    value--;
}
```

**release\(\)**

```c
release() {
    value++;
}
```

#### Conditions

* **Changing semaphore "value" should not be done separately**. That is, If one thread changes semaphore value, any other thread cannot be change same semaphore value at same time.
* **acquire\(\) line 2** \(value &lt;= 0\) and **line 5** \(value--;\) **should not be interrupted**.

## Usage

There are two types of semaphore

* **Counting** semaphore value has no limit
* **Binary** \(**Mutex lock**\) semaphore value can be 0 or 1

// TODO













\*\*\*\*

\*\*\*\*

