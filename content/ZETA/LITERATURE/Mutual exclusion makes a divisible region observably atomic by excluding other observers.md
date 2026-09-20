---
up:
  - "[[An operation is atomic if no thread can observe it half-done]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
Hardware makes only a few single instructions atomic, but real critical sections are bigger (read a balance, check it, write it back). You can't make an arbitrary multi-step region physically indivisible, but you can stop anyone from *looking* while it runs.

**Mutual exclusion**: guarantee that at most one thread is inside the region at a time. Then no other thread is ever positioned to observe its half-done middle. The region is still physically divisible but the divisibility becomes **unobservable**. It is *observably* atomic: indistinguishable from atomic to every other thread.

This is the **first of the two guarantees** a lock provides. Note precisely what it does and doesn't do:
- It does **not** make the instructions physically atomic (the hardware still sees separate ops).
- It does **not** stop the scheduler from interleaving the threads generally — the other thread runs freely, it just can't *enter this region* concurrently.
- Fairness (acquiring in request order) is a separate, optional property, not what mutual exclusion is.

It is tempting to think this is the *whole* story of a lock. It is not — mutual exclusion alone is necessary but not sufficient. See [[The store-buffer litmus test proves mutual exclusion is not enough|the store-buffer litmus test]] to see why.

# See also
- [[An operation is atomic if no thread can observe it half-done]] — mutual exclusion recovers atomic *behaviour* for regions too big for hardware atomicity, by making the half-done middle unobservable
- [[The store-buffer litmus test proves mutual exclusion is not enough]] — the counterexample: a program with no concurrent region-entry still breaks, so one-at-a-time cannot be the whole story
- [[A lock provides two guarantees, mutual exclusion and a happens-before edge]] — mutual exclusion is exactly guarantee one of the two a lock supplies
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — Rust bakes mutual exclusion into the type system: `&mut` is compile-time exclusive access, guaranteed statically rather than at runtime

# References
- https://docs.oracle.com/javase/specs/jls/se7/html/jls-17.html

# Questions
#flashcards/stem/os

How does mutual exclusion make a divisible critical section "act atomic"?::By ensuring only one thread is inside at a time, no other thread can observe the region's half-done middle — it becomes observably atomic without being physically indivisible

Is mutual exclusion the whole story of a lock?::No — it is necessary but not sufficient; a program with no concurrent region entry can still break from visibility/ordering issues

Mutual exclusion makes the region's divisibility ==unobservable==, not physically ==indivisible==.
