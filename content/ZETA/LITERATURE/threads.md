---
up:
tags:
  - todo
created: 2026-08-03 22:42
---

A thread is a basic unit of CPU utilization, with its own:
- program counter (PC)
- private set of registers
- stack

[[A context switch saves the PCB of the running process and restores another|context switch]] happen also in threads, but [[virtual memory|virtual address space]] is shared.

The state of the thread is stored in the TCB (thread control block). 