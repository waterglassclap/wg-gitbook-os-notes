# Summary

## Hardware Support

**Single or Multiple Separation**  
Does not need hardware Support

**Paging / Segmentation**  
Needs hardware support \(Mapping Table\)

## Performance

The more structure becomes complicated, the more time takes to convert logical address to physical address.  
If paging and segmentation have to manipulated in main memory, memory access speed would be very slow.

**TLB** device can resolve this.

## Fragmentation

**Fixed Size Allocation System** like paging or single partition would have **internal fragmentation problem**

**Variable Size Allocation System** like Segmentation or multiple partition would have **external fragmentation problem**

## **Relocation**

One of the solution for external fragmentation is compaction.  
To do this, logical address can be dynamically relocated. If address defined in load time, it cannot be done.

## Swapping

OS can move process from main memory to sub memory, or move process from sub memory to main memory.

## Sharing

Sharing is to execute many process in limited memory.

## Protection

Page or Segment can define each part as execute-only / read-only / read-write.



