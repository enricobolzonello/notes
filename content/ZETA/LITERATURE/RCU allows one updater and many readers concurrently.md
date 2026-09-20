---
up:
  - "[[The process scheduler chooses an available process]]"
tags:
  - atomic
created: 2026-05-12 15:52
---
Read-copy update (RCU) is one of the synchronization mechanism of the linux kernel, which supports concurrency between a single updater and multiple readers. 

Updates are into "removal" and "reclamation" phases
- **removal**, remove references to items within a data structure. Can run concurrently with readers.
	- It is safe because modern CPUs guarantee that readers will not see a partially updated reference
- **reclamation**, free the data items. This phase must not start until readers no longer hold references to those data items.

The sequence is the following:
- remove pointers to a data structure so that subsequent readers cannot gain a reference to it
- wait for all existing readers to complete their RCU read-side critical sections (*grace period*). In this period, readers always read the old version.
- at this point, it can be safely reclaimed

# See also
- [[The process scheduler chooses an available process]] — RCU protects the task list that the scheduler reads on every scheduling decision; readers (scheduler picking a task) never block, writers (adding/removing tasks) defer reclamation until the grace period
- [[CFS picks the task with the lowest vruntime, stored as the leftmost node of a rbtree]] — CFS reads the rbtree of runnable tasks under RCU protection; the read-side critical section is the window between entering and exiting the rbtree traversal
- [[&T Is a Shared Reference, Copy but Not Mutable]] — RCU is the kernel-level analogue of `&T`: multiple concurrent readers hold shared references to the data structure; the updater publishes a new version rather than mutating in place
- [[Single Writer Principle, one thread own all writes to a resource]] — RCU enforces the single writer principle at the kernel level: only one updater can modify the data structure at a time; readers never need to acquire a lock
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — a context switch is one of the events that advances the grace period: once every CPU has gone through a context switch, all pre-existing read-side critical sections have completed
- [[A lock provides two guarantees, mutual exclusion and a happens-before edge]] — RCU is the "happens-before without mutual exclusion" case: readers never take a lock; safety comes entirely from publishing the new version (a release) and reclaiming only after a grace period establishes the ordering
- [[Happens-before is the single relation guaranteeing visibility and ordering across threads]] — the grace period is a happens-before argument: reclamation waits until all readers' read-side critical sections have ended, so no reader can still hold a reference to the freed version

# References
- https://docs.kernel.org/RCU/whatisRCU.html#whatisrcu


