---
up:
  - "[[Acquire and release are the half-barriers that manufacture a synchronizes-with edge]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
A lock was never just "one thread at a time." It provides **two independent guarantees at once**, and forgetting the second is the classic mistake:

1. **[[Mutual exclusion makes a divisible region observably atomic by excluding other observers|Mutual exclusion]]** — only one thread holds the lock, so the critical section acts atomic (guarantee one).
2. **A [[Happens-before is the single relation guaranteeing visibility and ordering across threads|happens-before]] edge** — `unlock()` is defined as a **release** and `lock()` as an **acquire**. When a thread's lock-acquire observes the state left by the previous holder's unlock-release, they form a synchronizes-with edge; by transitivity every write made inside the previous critical section is guaranteed *visible and correctly ordered* for the next holder (guarantee two).

This is why a mutex-guarded critical section is safe where the store-buffer litmus test was not: the test had mutual-exclusion irrelevance *and* no happens-before edge; a lock supplies both. Fairness (FIFO acquisition) is a separate optional property and is **not** what provides visibility; a lock also does not make instructions physically atomic — it makes the region *observably* atomic while *publishing* its writes.

This single idea is the trunk of the whole subject: **every concurrency mechanism is one of these two guarantees, both, or neither.** Some examples:
- **[[RCU allows one updater and many readers concurrently|RCU]]** = happens-before **without** mutual exclusion (readers never lock; safety is publish + grace period).
- **[[Single Writer Principle, one thread own all writes to a resource|Single Writer]]** = design away the *need* for mutual exclusion; only publishing (guarantee two) remains.
- **[[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It|&mut T]]** = mutual exclusion enforced in the type system at compile time.

# See also
- [[Acquire and release are the half-barriers that manufacture a synchronizes-with edge]] — unlock=release and lock=acquire; this is how a lock delivers guarantee two
- [[Mutual exclusion makes a divisible region observably atomic by excluding other observers]] — guarantee one; a lock supplies it *plus* the happens-before edge
- [[The store-buffer litmus test proves mutual exclusion is not enough]] — the proof that both guarantees are needed; a lock is safe there precisely because it adds the second
- [[RCU allows one updater and many readers concurrently]] — the "happens-before without mutual exclusion" corollary
- [[Single Writer Principle, one thread own all writes to a resource]] — the "design away guarantee one" corollary
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — the "mutual exclusion in the type system" corollary

# References
- https://en.cppreference.com/w/cpp/atomic/memory_order
- https://docs.oracle.com/javase/specs/jls/se7/html/jls-17.html

# Questions
#flashcards/stem/os

What two guarantees does a lock provide?::Mutual exclusion (one thread at a time) AND a happens-before edge (unlock=release synchronizes-with the next lock=acquire, making the critical section's writes visible and ordered)

Why is a mutex-guarded critical section safe where the store-buffer litmus test was not?::The lock supplies the missing happens-before edge (unlock-release → lock-acquire) in addition to mutual exclusion; the test had neither

Every concurrency mechanism is one of the two lock guarantees, both, or neither: RCU is ==happens-before without mutual exclusion==; Single Writer ==designs away mutual exclusion==; `&mut T` is ==mutual exclusion in the type system==.
