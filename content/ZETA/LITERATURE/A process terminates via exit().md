---
up:
  - "[[Processes in memory are represented by a tree]]"
tags:
  - atomic
created: 2026-04-23 11:21
---

A process terminates when it finished executing the last instruction and asks the OS to delete it by using the `exit()` sys call. 

Some systems do not allow a child to exists if parent has been terminated (**cascading termination**). 

When a process terminates its resource are deallocated but the entry in the process table must remai there until parent calls `wait()`. A **zombie process** is a child process which is terminated but whose parent has not yet called `wait()`. All processes briefly transitions to this state.

A more serious state is the **orphan**, which means that the parent did not call `wait()` but instead terminated. In this case, they are reassigned to the `init` process as the new parent.

# See also
- [[Processes in memory are represented by a tree]] — termination propagates through the tree: cascading termination, zombie and orphan states are all consequences of the parent-child relationship
- [[A process is represented in memory with the Process Control Block (PCB)]] — the PCB entry that must remain after termination until wait() is called is exactly the process table entry described there; zombie processes are PCBs without running processes behind them
- [[In a process execution, it goes through many stages]] — terminated is the final state in the state diagram; zombie is a sub-state of terminated where resources are freed but the PCB persists
- [[The process scheduler chooses an available process]] — zombie processes occupy a process table entry but are never put in the ready queue; they are invisible to the scheduler but visible to the OS bookkeeping
- [[Reliability means preventing faults from causing failures]] — zombie and orphan processes are resource leaks: a fault (parent not calling wait()) that can accumulate into a system failure if process table entries fill up

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».