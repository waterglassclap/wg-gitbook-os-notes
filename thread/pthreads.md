# PThreads

**PThreads** is Standard API for creating / synchronizing threads, made by POSIX. Each OS implements this API.  
PThreads includes:

### pthread\_create

```c
int pthread_create(pthread_t thread,
                   const pthread_attr_t attr,
                   void (start_routine)(void ), void arg);
```

Creates thread

* **thread** : unique thread ID
* **attr** : thread attributes. default = NULL
* **start\_routine** : functions to be run on thread
* **arg** : argument passed to start\_routine

### pthread\_self

```c
pthread_t pthread_self(void);
```

returns threads unique ID

### pthread\_join

```c
int pthread_join(pthread_t th, void **thread_return);
```

Wait thread stop, get thread exit signal and cleanup resources.

* **th** : thread ID to join
* **thread return** : thread return value

### pthread\_detach

```c
int pthread_detach(pthread_t th);
```

detaches thread from main thread using pthread\_create.  
separated thread immediately cleanup resources on exit, not waiting for pthread\_join.

### pthread\_exit

```c
void pthread_exit(void *retval);
```

terminate current thread

### pthread\_mutex\_init

```c
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutex_attr *attr);
```

inits thread mutex object

* **mutex** : target mutex object
* **attr** : mutex attributes \(fast / recursive / error checking .. \). default = fast

### pthread\_mutex\_lock

```c
int pthread_mutex_lock(pthread_mutex_t *mutex);
```

for thread mutex lock

### pthread\_mutex\_unlock

```c
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

### pthread\_mutex\_destroy

```c
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

## References

{% embed url="https://blog.naver.com/myca11/221224081981" %}

[https://guswnsla1223.tistory.com/70](https://guswnsla1223.tistory.com/70)

