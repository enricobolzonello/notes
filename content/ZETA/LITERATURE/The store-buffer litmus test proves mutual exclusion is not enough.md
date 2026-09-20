---
up:
  - "[[Mutual exclusion makes a divisible region observably atomic by excluding other observers]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
Is mutual exclusion enough? The **store-buffer litmus test** proves it is not — and it does so with a program that has *no concurrent region-entry at all*.

Start with `x = 0`, `y = 0`. Two threads, each one write then one read:

$$\textbf{T1:}\quad x = 1;\ \ r_1 = y; \qquad\qquad \textbf{T2:}\quad y = 1;\ \ r_2 = x;$$

Intuition says at least one of $r_1, r_2$ must be 1: each thread writes *before* it reads, so surely the other thread sees the write. **That intuition is wrong.** On real hardware, $r_1 = 0$ **and** $r_2 = 0$ is a legal, observed outcome. Two independent mechanisms cause it:

- **Store buffer** — each thread's write can sit in its core's local store buffer, not yet flushed to shared cache/memory, when it does its read. So each read sees the other variable's *old* value 0.
- **Reordering** — within each thread the write and read are to *different* addresses, so single-threaded semantics are preserved if the compiler or CPU reorders them, moving the read before the write.

The decisive point: **no shared region is entered concurrently here**, so mutual exclusion is irrelevant — yet the program still breaks. That is airtight proof of a **second, independent axis**: whether writes become *visible*, and *in order*, to other cores. This is a completely different problem from "one thread at a time", and it is exactly the axis where stale-flag and reordering bugs live.

# See also
- [[Mutual exclusion makes a divisible region observably atomic by excluding other observers]] — this is the counterexample to mutual exclusion being sufficient: it fixes half-done state but does nothing for cross-core visibility
- [[Happens-before is the single relation guaranteeing visibility and ordering across threads]] — the missing second guarantee that this test motivates; the test fails because it has no happens-before edge across threads
- [[False sharing forces CPUs to serialise access when two threads write to the same cache line]] — the same hardware layer (store buffers, per-core caches, cache lines) that makes this test surprising
- [[An operation is atomic if no thread can observe it half-done]] — a different failure mode: here the individual writes *are* atomic, yet the program still misbehaves purely from visibility/ordering

# References
- https://preshing.com/20120515/memory-reordering-caught-in-the-act/
- https://docs.oracle.com/javase/specs/jls/se7/html/jls-17.html

# Questions
#flashcards/stem/os

In the store-buffer litmus test (x=1;r1=y // y=1;r2=x, both start 0), can both reads end up 0?::Yes — on real hardware each write can sit in a store buffer or be reordered after the read, so neither write is visible to the other yet

What does the store-buffer litmus test prove about mutual exclusion?::That it is not sufficient — the program has no concurrent region entry yet still breaks, revealing a second axis: visibility and ordering of writes across cores

The two mechanisms that let both reads see 0 are the CPU ==store buffer== and compiler/CPU ==reordering==.
