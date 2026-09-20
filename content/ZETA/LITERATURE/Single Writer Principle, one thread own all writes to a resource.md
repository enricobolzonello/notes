---
up:
  - "[[The Actor Model Isolates State Behind Message Passing, No Shared Memory]]"
tags:
  - atomic
created: 2026-04-13 11:20
---
If some data or resource is written to, all writes should be made by a single thread. Wrap access to the resource in a dedicated [[The Actor Model Isolates State Behind Message Passing, No Shared Memory|actor]] thread that owns all writes.

**TAKEAWAY**: avoid protecting writable resources with a mutex, dedicate an actor to own every write

# See also 
- [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — the single writer principle is the actor model applied at the hardware level: one actor owns a resource and all mutations go through it 
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — the single writer principle also eliminates false sharing: if only one thread writes to a variable, there is no concurrent cache line contention 
- [[Interface Segregation Principle (ISP)]] - same philosophy at the API level: reduce unnecessary coupling; the single writer reduces unnecessary write coupling between threads.
# References 
- https://martinfowler.com/articles/mechanical-sympathy-principles.html