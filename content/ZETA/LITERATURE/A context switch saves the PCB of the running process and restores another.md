---
up:
  - "[[The process scheduler chooses an available process]]"
tags:
  - atomic
created: 2026-04-03 13:43
---

Interrupts ( #todo ) makes the CPU change the current task with a kernel routine. When it happens, the context, represented in the [[A process is represented in memory with the Process Control Block (PCB)|PCB]], needs to be saved so that it can restore it later. This is known as **context switch**.

![[process_context_switching.png]]

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».

# See also
- [[The process scheduler chooses an available process]] — context switching is the mechanism the scheduler triggers when moving a process from running back to ready or waiting
- [[A process is represented in memory with the Process Control Block (PCB)]] — the PCB is exactly what gets saved and restored during a context switch: program counter, CPU registers, memory info
- [[In a process execution, it goes through many stages]] — a context switch drives the running→ready transition in the state diagram: the process doesn't terminate, it just gets preempted
- [[Tail Call optimization replaces call with jmp]] — TCO reduces the number of stack frames that need saving during a context switch; fewer frames means cheaper context switches in recursive call chains