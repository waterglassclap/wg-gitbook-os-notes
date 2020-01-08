# System Model

System is consist of finite number of resources. Each resources consist of multiple equivalent instances.  
If one process request for one resource, resource allocates its instance.

Process uses resources as

1. **Request** Process request for resource. If request does not allowed immediately, process waits until it gets resource
2. **Use** Process executes job with resource
3. **Release** Process releases resource

Example of resource request / release system call

1. **request\(\)** : **release\(\)**
2. **open\(\)** : **close\(\)**
3. **allocate\(\)** : **free\(\)**

Example of resource request / release non-system call 

1. semaphore **wait\(\)** : **signal\(\)**
2. mutex lock acquire : release

Every time process or thread uses resources, OS checks for its system table \(whether resource is free or allocated, which process has resource if allocated\)  
If one process request for resource already allocated to another process, process can be written on process queue waiting for the resource.

**If every process in one process group waits for event,  
which only can be occurred with one of its process,  
the process group is in deadlock**

