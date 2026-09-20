---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2026-04-13 11:11
---

Memory is organized in a hierarchy ( #todo )  of registers, buffers and caches and main memory with increasing latency at each level. CPUs exploit three locality rules to prefetch data efficiently:
- *temporal locality*: recently accessed memory will probably be accessed again soon
- *spatial locality*: memory near recently accessed memory will probably be accessed soon
- memory access will probably follow the same pattern

**TAKEAWAY**: prefer algorithms and data structures that enable predictable, sequential access to data


# See also 
- [[A process in operating systems is a program in execution]] — the process memory layout (stack, heap, text, data) is what the CPU traverses; sequential layout in the stack is cache-friendly by design 
- [[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them]] — open addressing is cache-friendly (all entries in a single array, sequential access); separate chaining is not (pointer-chasing through linked lists breaks spatial locality) 
- [[SIMD - one operation applied to multiple data points simulaneously]] — SIMD exploits the same spatial locality: processing contiguous data points with a single instruction is efficient precisely because they are already in the same cache line

# References
- https://martinfowler.com/articles/mechanical-sympathy-principles.html