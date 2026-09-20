---
up:
  - "[[Prefer sequential memory access, CPUs predict and prefetch based on locality]]"
tags:
  - atomic
created: 2026-04-13 11:16
---

Within caches, memory is stored in contiguous chunks called *cache lines*, which are always a power of two in length. If two CPUs write to two separate variables that share the same cache line, they are forced to take turns. This phenomenon is called **False Sharing**. 

To prevent it, pad cache lines with empty data to ensure each independently-written variable occupies its own cache line.

**TAKEAWAY**: check if any data structure is being written to by multiple threads and check for false sharing.

# See also 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — false sharing is the dark side of spatial locality: proximity that helps reads hurts concurrent writes - [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — the actor model eliminates false sharing structurally: no shared memory means no shared cache lines 
- [[System Programming - Compile utilities]] — ThreadSanitizer detects race conditions on shared data; false sharing is a performance pathology of the same category 
# References 
- https://martinfowler.com/articles/mechanical-sympathy-principles.html