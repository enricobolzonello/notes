---
up:
  - "[[In a process execution, it goes through many stages]]"
tags:
  - atomic
created: 2026-04-03 13:16
---

The aim is to maximize CPU utilization. The **process scheduler** aims to do that by choosing an available process for an execution on a core.

When a process is created, it is immediately put in the **ready queue**, and it waits there until it is *dispatched*. If instead the process is waiting for some operation (for example, I/O) then it is put in the **waiting  queue**. 

The role of the **CPU scheduler** is to select one of the processes in the ready queue. Another intermediate form of scheduling is [[OS - Memory Management#Swapping|swapping]].


# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».

# See also
- [[In a process execution, it goes through many stages]] — the scheduler is what drives the ready→running and running→waiting transitions in the state diagram
- [[A process is represented in memory with the Process Control Block (PCB)]] — the PCB is what the scheduler reads to select a process: it contains the process state, CPU registers, and scheduling information needed to dispatch and context-switch
- [[A process in operating systems is a program in execution]] — the memory layout (stack, heap) is what gets swapped in and out when the scheduler moves processes between queues
- [[SIMD - one operation applied to multiple data points simulaneously]] — SIMD is an alternative strategy to maximise CPU utilisation within a single running process rather than across multiple processes; both serve the same goal from different angles