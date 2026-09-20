---
connections:
tags:
  - permanent_note
  - theme/engineering
  - type/note
type: permanent_note
created: 2025-01-31 10:52
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> Technique that allows the execution of processes that are not completely in memory

- [[OS - Memory Management]] algorithms assumed that instructions must be in physical memory to be executed
	- not all instructions may be needed at the same time
- **virtual address space**: logical view of how a process is stored in memory

![[OS_virtual_memory_1.png]]

- in the virtual address space of a process in memory the stack grows downwards while the heap grows upwards
	- the hole in between is part of the virtual address space but will require physical only if one of the two grows
- another benefit: *files and memory can be shared by two or more processes*

## Demand Paging

> Technique to load pages only when they are demanded

- similar to [[OS - Memory Management#Swapping|swapping with paging]] but it is a reactive approach (action only when requested) compared to proactive (when RAM full, OS does swapping with paging)
- needs hardware support to distinguish between pages in memory and pages in secondary hardware
	- **valid-invalid bit**
		- valid = page is both legal and in memory
		- invalid = page is either not valid or is valid but in secondary storage
	- access to pages marked invalid causes a **page fault**
		- procedure to handle page faults:
			- check an internal table to determine if the reference was valid or an invalid memory access
			- if invalid, terminate the process. If valid but the page is in secondary hardware, page it in
			- find a free frame
			- schedule a secondary storage op to read the page into the new frame
			- modify the internal table with the process and the page table to indicate that the page is now in memory
			- restart the instruction interrupted by the trap
![[OS_virtual_memory_pagefault.png]]

- extreme case - **pure demand paging**: load no pages in memory at start
- objection
	- theoretically some programs could access several new pages with each instruction execution
	- would impact performance
	- but, in practice, programs have **locality of reference**

> [!hint] Performance Analysis
> The formula is:
> $\text{effective access time} = (1-p)\cdot ma + p \cdot \text{page fault time}$
> where $p$ is the probability of a page fault. 
> Assuming 8 milliseconds of paging time (with HDD) and a memory-access time of 200 nanoseconds, we get:
> $\text{effective access time} = 200 + 7,999,800 \cdot p$
> If 1/1000 accesses would cause a page fault, the computer would be slowed down by a factor of 40.
> If we want less than 10% degradation, then:
> $p < 0.0000025$

## Free-Frame list

> Pool of free frames to resolve page faults

- allocated using **zero-fill-on-demand**
	- frames are zeroed-out before being allocated (erasing previous content)
- when system starts up, all available memory is placed on the free-frame list
- when the list must be repopulated (falls to 0 or below a threshold), some strategies are used


## Copy-on-Write

> Instead of  copying the parent's address space, `fork()` may use this technique to have parent and child processes initially to share the same pages

- pages are specifically marked
	- if either process writes to a shared page, a copy of it is created
- instead of `fork()` (fork with copy-on-write) there is `vfork()` on most UNIX (including linux and macos)
	- parent process is suspended
	- child process uses address space of the parent

## Page Replacement

- over-allocation may happen
	- while a process is executing, a page fault occurs. The OS finds that there are no free frames on the [[OS - Virtual Memory#Free-Frame list|free-frame list]].
	- how to solve? **Page replacement**

- approach
	- if no free frame, find one that is not currently used and free it
		- writing its content to swap space
		- change the page table to indicate that the page is no longer in memory
	- *two page transfers are required* (one for page-out, one for page-in)
		- reduce the overhead by using a **dirty bit**
			- set when any byte in the page is written into
			- when select a page for replacement, examine the bit
				- if bit is set, we must write the page to storage
				- if not, we need not write the memory page into storage
- **frame-allocation algorithm**
- **page-replacement algorithm**
	- how to select them? low page fault on a *reference  string* (string of memory references)

### FIFO Page replacement

- associate with each page the time when it was brought into memory
- when a page must be replaced, the oldest is chosen

- causes **Belday's anomaly**
	- page-fault increses as the number of allocated frames increses

### Optimal Page replacement

- replace the page that will not be used for the longest period of time

- lowest possible page-fault rate
- requires future knowledge of the reference string
	- just used for comparison

### LRU Page Replacement

- replace the page that has not been used for the longest period of time

- implementation requires some hardware to determine the order for the frames defined by the time of last use
	- two approaches
		- **counters**: 
			- each page-table entry has a time-of-use field
			- CPU requires a logical clock or counter
		- **stack**
			- keep a stack of page numbers
			- whenever a page is referenced, it is removed from the stack and put on the top
	- neither implementations are feasible due to the update that must be done for every memory reference, slowing down by a factor of at least ten

### LRU-Approximation Page replacement

- lru requires hardware support, many do not have it
	- instead, many systems provide a **reference bit**
		- set by the hardware whenever that page is referenced (either read or write)
- this bit is used for many algorithms

#### Additional-Reference-Bits algorithm

- keep a byte for each page in a table in memory
- at regular intervals, shift right the reference bit for each page, discarding the low-order bit
- *page with lowest number is the LRU page*

#### Second-Chance algorithm
- FIFO but inspects the reference bit
	- if the value is 0, we can replace the page
	- else, give the page a second chance and select the next FIFO page. Reset the reference bit
- can be implemented as a circular queue
- **enhanced version**
	- consider the reference bit and the modify bit as an ordered pair
	- four cases
		- (0,0), neither recently used or modified = best page to replace
		- (0,1), not recently used but modified = page will need to be written out
		- (1,0), recently used but clean = probably will be used again soon
		- (1,1), recently used and modified = combination of two above


## Allocation of Frames
- how to allocate the fixed amount of free memory among the processes
- diverse strategies, but the basic is that the *user process is allocated any free frame*
- constraints
	- cannot allocate more than the total number of available frames
	- must allocate at least a minimum number of frames
		- why?
			- performance = lower page-fault rate
		- chosen by the architecture

### Allocation algorithms

1. **Equal allocation**
	- split $m$ frames among $n$ processes by giving everyone $m/n$ frames
2. **Proportional allocation**
	- allocate $a_i$ available memory to each process $p_i$ according to its size $s_i$
		- $a_i = \sum s_i / S \cdot m$
	- there can be variations with priority or combination of size and priority

### Global and Local Allocation

- multiple processes compete for frames
	- **global replacement**
		- allows a process to select a replacement frame from the set of all frame
		- problem: set of pages in memory depends also on the paging behaviour of other processes
		- generally greater system throughput
	- **local replacement**
		- each process select from only its own set of allocated frames


- example global replacement strategy
	- keep the amount of free memory above a minimum threshold
	- when below, call a kernel routine called **reaper** to reclaim pages from all processes
		- reaper may adopt any [[OS - Virtual Memory#Page Replacement|page replacement]] algorithm (typically [[OS - Virtual Memory#LRU-Approximation Page replacement|lru approximation]])
		- if it cannot keep it below the threshold?
			- use a more aggressive algorithm (exampe FIFO)
			- extreme: **out-of-memory (OOM) killer**
				- selects a process to terminate
				- each process has a OOM score, higher means higher probability of being killed

### Non-Uniform Memory Access (NUMA)

- a given CPU can access some sections of main memory faster than it can access others
	- depends on how CPUs and memory are interconnected![[numa.png]]
	- slower, but can achieve greater levels of throughput and parallelism

## Thrasing
- process is *thrashing* if it is spending more time paging than executing

### Causes
- increasing multiprogramming above a certain threshold causes CPU utilization drops and so **thrashing**![[thrashing.png]]
	- limit trashing by using a local replacement algorithm
	- *to prevent, we must provide a process with as many frames as it needs*
		- example strategy:
			- look at how many frames a process is actually using
			- **locality model** = as a process executes, it moves from locality to locality. 
				- A *locality* is a set of pages that are actively used together

### Woking-Set model

> Model uses a parameter $\Delta$ to define the **working-set window**. The set of pages in the most recent $\Delta$ page references is the **working set**. If a page is in active use, it will be in the working set. If it is no longer being used, it will drop from the working set $\Delta$ time units after its last reference.

- approximation of the program's locality
- accuracy of working set depends on $\Delta$
	- if we compute the working-set size $WSS_i$ for each process we can say $D=\sum WSS_i$ where $D$ is the total demand for frames
	- if $D>m$ ($m$ is the total number of available frames), **trashing will occur**
- how to use
	- OS monitors the working set of each process
	- allocates enough frames to provide it with its working-set size
	- if there are enough extra frames, initiate another process
	- if $D>m$, select a process to suspend
		- process's pages are swapped and its frames reallocated
- **approximate the working-set model with a fixed-interval timer interrupt and a reference bit**
	- when we get a timer interrupt, we copy and clear the reference bit for each page
	- Thus, if a page fault occurs, we can examine the current reference bit and two in-memory bits to determine whether a page was used within the last 10,000 to 15,000 reference
	- If it was used, at least one of these bits will be on

### Page-Fault Frequency (PFF)

- another, more direct approach
![[pff.png]]

## Memory Compression
- alternative to paging
- Compress several frames into a single frame before moving them to the free-frame list. If one of the compressed frames is later referenced, a page fault occurs and the compressed frame is decompressed.
- no paging on **mobile systems**, but there is memory compression
- higher compression = more expensive algorithms
- WKdm in apple systems

## Allocating Kernel Memory
- kernel memory is allocated differently than user mode memory, why?
	- minimize internal fragmentation that happens like in user mode
	- some hardware devices interact directly with physical memory and they can't have the benefits of the virtual memory

### Buddy system
- allocates memory from a fixed-size segment consisting of physically contiguous pages
- memory is allocated in power of 2 sizes
- divide the segment into two **buddies** until we can satisfy the request

![[buddy_allocation.png]]

- **Pro**: fast *coalescing* (combine buddies to form larger segments)
- **Cons**: fragmentation due to rounding up to the next highest power of 2

### Slab allocation
- **slab** = one or more physically contiguous pages
- **cache** = one or more slabs
- one single cache for each unique data structure
- each cache is populated with **objects** (instantiations of the kernel data structure)
- when a cache is created a number of objects (initially marked as free) are allocated
- when a new object is needed, the allocator assigns any free object from the cache and marks it as used

**Pros**:
- no memory fragmentation
- memory requests can be satisfied quickly


Linux initially used buddy system, then changed to `SLAB` and then again to `SLUB` and `SLOB`.
`SLUB` is the default

--- 

# Questions
#flashcards/stem/os 

Under what circumstances do page fault occur?::first access to a page, page was swapped out of disk, page table entry's "valid bit" is set to invalid
<!--SR:!2026-04-08,1,230-->

Describe the actions taken by the operating system when a page fault occurs.::trap the os, check if the memory reference was a legal address, find a free frame, if memory is full OS selects a victim page using a replacement algorithm, load the page from disk, update the page table entry, restart the faulting instruction
<!--SR:!2026-04-08,1,230-->

Assume that a program has just referenced an address in virtual memory. Describe a scenario in which of the following can occur::-TLB miss with no page fault -TLB miss with page fault -TLB hit with no page fault -TLB hit with page fault
<!--SR:!2026-04-08,1,230-->