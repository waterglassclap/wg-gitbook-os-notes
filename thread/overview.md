# Overview

## Motivation

Thread is basic unit of CPU Processing

![Single / Multi Threads](../.gitbook/assets/image%20%2812%29.png)

 **Each thread has**

* Thread ID
* PC
* Registers
* Stack

 **Threads in same process share**

* Code
* Data Section
* Heap
* OS Resources like Signal / Files open 

## Benefits

#### Responsiveness

For example, multithread web browser can communicate with user while another thread loads image files

#### Resource Sharing

Threads in same process shares resources and memory. 

#### Economy

Process : expensive, Thread : relatively cheap

#### Utilization of multiprocessor architectures

On multiprocessor, each thread can be processed each multiprocessor.  
Single thread process can use only one processor no matter how many processor there are.  
In short, multithreading on multiprocessor env can increase parallelism

## ETC

### Parallelism vs Concurrency

**Parallelism** : Physically. With hardware  
ㅇ -&gt; ㅇ -&gt; ㅇ -&gt; ㅇ -&gt; ㅇ -&gt; ...  
ㅁ -&gt; ㅁ -&gt; ㅁ -&gt; ㅁ -&gt; ㅁ -&gt; ..  
  
**Concurrency** : Logically. With program  
ㅇ -&gt; ㅁ -&gt; ㅇ -&gt; ㅇ-&gt; ㅁ-&gt; ㅇ-&gt; ...

## References

[https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/3\_Processes.html](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4_Threads.html)

[https://blog.naver.com/myca11/221224081981](https://blog.naver.com/myca11/221224081981)

