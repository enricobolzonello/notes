---
up:
  - "[[The Actor Model Isolates State Behind Message Passing, No Shared Memory]]"
tags:
  - atomic
created: 2026-04-13 11:27
---

An [[The Actor Model Isolates State Behind Message Passing, No Shared Memory|actor]] begins to create a batch as soon as requests are available in its queue, and completes the batch as soon as the maximum batch size is reached or the queue is empty.

**TAKEAWAY**: build each batch greedily

# See also 
- [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — natural batching is an actor-specific optimisation: the actor's message queue is the natural accumulation point for a batch 
- [[The process scheduler chooses an available process]] — the scheduler and the natural batching actor share the same structure: a queue of work items, a dispatcher that picks from it greedily 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — processing a batch sequentially is cache-friendly: contiguous queue entries exploit spatial locality 
# References 
- https://martinfowler.com/articles/mechanical-sympathy-principles.html