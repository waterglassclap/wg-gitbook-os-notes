# Scheduling Criteria

## Criteria

Scheduling is for  
-  maximizing cpu utilization, throughput  
-  minimizing turnaround time, waiting time, response time

but researchers found in interactive system, reducing variance of requests is more important than reducing mean response time.

### CPU Utilization

**Keep CPU busy as possible**. Theoretically, cpu usage can be 0 to 100%, but in real system, 40 to 90% is recommended.

### Throughput

**Completed process / time**

### Turnaround Time

**Turnaround time** =  
        waiting time **from disk to memory**   
        + waiting time **in ready queue**  
        + **cpu operation time**  
        + **i/o time**

### Waiting Time

**Waiting time** = **total ready queue time**. CPU scheduling only affects process' ready queue time.

### Response Time

**Response time** = **first response started time** - **response submitted time**  
Response time does not includes output time. Total operation time is limited by output device's time generally.

## References

[https://brunch.co.kr/@leedongins/76](https://brunch.co.kr/@leedongins/76)

