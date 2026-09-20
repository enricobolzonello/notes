---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2026-04-23 11:12
---

Processes in memory are represented by a tree, where each process has a parent. In Linux, `systemd` is always the root parent processes for all user processes and has pid 1. In MacOS, launchd has the same role.

Child processes are created via `fork()`, which duplicates the parent process. Optionally, `exec()` can then load a new program into the child's address space.

When a child process needs resources, either it obtains them directly from the OS or from the parent.

During execution, there are two possibilities:
- parent continues to execute concurrently with its children
- parent waits until some or all of its children have terminated

Also for address-space there are two possibilities:
- child process is a duplicate of the parent process
- child process has a new program loaded into it

# See also
- [[A process is represented in memory with the Process Control Block (PCB)]] — each node in the process tree is represented by a PCB; the tree structure is how the OS tracks parent-child relationships between PCBs
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — when a parent waits for a child to terminate, a context switch moves the CPU away from the parent; the PCB preserves its state until the child finishes
- [[The process scheduler chooses an available process]] — the scheduler treats all processes in the tree as candidates for the ready queue regardless of their parent-child relationship; the tree is a structural relationship, not a scheduling one
- [[Tree Recursion branches at each level]] — the process tree is the OS-level instance of tree recursion: each process can fork children, which fork their own children; the structure is identical to a recursive tree with systemd as the root
- [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — the two address-space options (duplicate vs new program) map directly onto actor model thinking: a duplicate child shares the parent's context, a new-program child is a clean actor with its own isolated state

# References
- A. Silberschatz, P. B. Galvin, e G. Gagne, «Operating System Concepts».