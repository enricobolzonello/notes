---
up:
tags:
  - atomic
created: 2026-04-03 11:59
---
A **process** in operating system informally is a program in execution. A program (usually represented by the executable file) becomes a process only when it is load in main memory.

The process memory layout is represented by the following figure:
![[process_memory_layout.png]]
- **text section**: stores the code
- **data section**: stores the global variables
- **stack section**: temporary storage when invoking functions
- **heap section**: dynamically allocated memory

In Linux specifically, each process is represented by a `task_struct` in a double-linked list which serves as the [[A process is represented in memory with the Process Control Block (PCB)|process table]]. 

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».

# See also
- [[Tail Call optimization replaces call with jmp]] — tail call optimization works directly on the stack section: TCO prevents new stack frames from being pushed, reducing stack memory from $O(n)$ to $O(1)$
- [[Linear Recursion is a chain of deferred operations]] — recursion builds a chain of deferred operations on the stack section; understanding the process memory layout explains why deep recursion causes stack overflow 
- [[SIMD - one operation applied to multiple data points simulaneously]] — SIMD operates at a lower level than the process: multiple processing elements working on data, bypassing the single-process execution model 
- [[System Programming - Compile utilities]] — practical tooling for working with processes: ThreadSanitizer and UBSan operate on running processes to detect race conditions and undefined behaviour