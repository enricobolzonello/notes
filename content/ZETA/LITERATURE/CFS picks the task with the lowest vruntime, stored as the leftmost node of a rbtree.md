---
up:
  - "[[The process scheduler chooses an available process]]"
tags:
  - atomic
created: 2026-05-12 11:59
---
On a real hardware only one task can run at once, hence why the need for a task scheduler. To do that, the concept of *virtual runtime* is introduced, which specifies when its next timeslice would start executing on the ideal multi-tasking CPU.

In Linux, the implementation is called **CFS** (Completely Fair Scheduler).

The task are picked based on `p->se.vruntime`, which is a per-task measure of the virtual runtime. It aims to always try to run the task with the smallest vruntime value.

To do that, it uses a time-ordered [[A Red-black tree is a BST where height invariant guarantees O(log n) operations|rbtree]], where all runnable tasks are sorted by `p->se.vruntime` key and picking the task is essentially just picking the leftmost task (the one with lowest `p->se.vruntime`).

The implementation of the rbtree in Linux has an additional ready queue which caches a pointer to the leftmost node, making the operation `O(1)` instead of `O(log n)`, making it par with the heap complexity. Another reason why rbtree is being chosen is that heaps are array based and hence require contiguous memory in kernel space, making it unsuitable for storing thousands of entities. 

# See also
- [[The process scheduler chooses an available process]] — CFS is the Linux implementation of the abstract scheduler: the ready queue described there is the rbtree here, and dispatching is picking the leftmost node
- [[A Red-black tree is a BST where height invariant guarantees O(log n) operations]] — CFS uses an rbtree specifically because picking the minimum is O(log n) without caching and O(1) with the leftmost pointer cache; the height bound is what makes this practical with thousands of tasks
- [[In a process execution, it goes through many stages]] — `vruntime` is only tracked for tasks in the running or ready state; waiting tasks are removed from the rbtree entirely and re-inserted when they become runnable again
- [[A process is represented in memory with the Process Control Block (PCB)]] — `p->se.vruntime` is a field in the PCB's scheduler entity (`sched_entity`); the PCB is what CFS reads and updates on every context switch
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — every context switch updates `vruntime` for the outgoing task before saving its PCB; the rbtree is then rebalanced to reflect the new ordering
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — the note mentions heaps are array-based and cache-friendly; CFS chose rbtree over heap precisely because contiguous memory for thousands of kernel entities is impractical, accepting the cache miss cost in exchange for dynamic allocation

# References
- https://docs.kernel.org/scheduler/sched-design-CFS.html
- https://stackoverflow.com/a/35561372