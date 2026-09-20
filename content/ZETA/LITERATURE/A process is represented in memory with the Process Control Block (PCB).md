---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2026-04-03 12:17
---
To represent a process at high level the operating system uses the **Process Control Block** (PCB), which basically serves as the storage for all the data that is needed for a process to start, stop and restart.
![[process_control_block.png]]
Contains (among other things):
- [[In a process execution, it goes through many stages|process state]]
- **Program counter**, indicates the address of the next instruction to execute
- CPU registers
- CPU-scheduling information #todo 
- memory-management information
- I/O status information


In Linux the PCB is stored in kernel's memory space, which is an area of memory not accessible by the user space. The place of the pointer for the `task_struct` is architecture dependant: on x86 at the end of task kernel stack, there is `thread_info` struct.

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».
- https://stackoverflow.com/a/10605654
- https://linuxgazette.net/133/saha.html

# See also
- [[In a process execution, it goes through many stages]] — the process state field in the PCB is exactly the state machine described there: new, ready, running, waiting, terminated
- [[A process in operating systems is a program in execution]] — the memory layout (stack, heap, text, data) is what the PCB's memory-management information tracks and protects
- [[Tail Call optimization replaces call with jmp]] — the program counter field in the PCB is what gets saved and restored on context switches; TCO avoids pushing new return addresses precisely to reduce this overhead
- [[System Programming - Compile utilities]] — ThreadSanitizer detects race conditions that arise when the OS switches between processes, saving and restoring CPU registers and program counter via the PCB