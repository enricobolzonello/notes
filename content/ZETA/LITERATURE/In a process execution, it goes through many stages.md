---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2026-04-03 12:11
---

When a process executes, it changes **state**. 
The state diagram is the following:
![[process_states.png]]
- new: process is being created
- ready: waiting to be assigned to a processor
- running: instructions are executing
- waiting: process is waiting for some operations (for example, I/O)
- terminated: finished execution

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».

# See also
- [[A process in operating systems is a program in execution]] — the parent concept: understanding the memory layout (stack, heap, text, data) explains what is being set up in the "new" state and torn down in "terminated"
- [[Tail Call optimization replaces call with jmp]] — tail call optimization is relevant to the "running" state: TCO changes how stack frames are managed during execution, affecting how long a process stays in the running state without overflow
- [[SIMD - one operation applied to multiple data points simulaneously]] — SIMD is another lens on the "running" state: multiple data points processed per instruction, exploiting parallelism within a single running process
- [[System Programming - Compile utilities]] — ThreadSanitizer operates on running processes to detect race conditions that occur precisely in the transition between "running" and "waiting" states
