---
up:
  - "[[The process scheduler chooses an available process]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
aAn operation is **atomic** if no other thread can ever observe it partially complete — it has either not happened or is fully done, never in an in-between state. There is no visible middle.

The trouble is that almost nothing you write is atomic. `counter = counter + 1` looks like one action but is really three machine steps:

$$\underbrace{\text{load } counter}_{1} \rightarrow \underbrace{\text{add } 1}_{2} \rightarrow \underbrace{\text{store } counter}_{3}$$

A thread can be interrupted *between* any of these steps. If two threads both run this on a counter at 50 and interleave so both load 50 before either stores, both compute and store 51 — one increment is lost (final 51 instead of 52). That observable half-done middle (loaded but not yet stored) is exactly what atomicity forbids.

Hardware provides atomicity only for a few single instructions ( **compare-and-swap (CAS)**, **fetch-and-add**, load-linked/store-conditional). 

# See also
- [[Mutual exclusion makes a divisible region observably atomic by excluding other observers]] — the first fix: since the danger is *observing* the half-done middle, exclude all other observers during the region
- [[Single Writer Principle, one thread own all writes to a resource]] — a different fix to the same lost-update problem: if only one thread ever writes, no interleaving of writes can occur
- [[RCU allows one updater and many readers concurrently]] — relies on the CPU guaranteeing readers never see a *partially updated* reference, i.e. pointer publication is atomic
- [[The process scheduler chooses an available process]] — the reason the middle is reachable at all: the scheduler may preempt a thread between any two instructions

# References
- https://en.cppreference.com/w/cpp/atomic/memory_order

# Questions
#flashcards/stem/os

What does it mean for an operation to be atomic?::No other thread can observe it partially complete — it is either not started or fully done, never in a visible in-between state

Why isn't `counter = counter + 1` atomic?::It is three machine steps (load, add, store) and a thread can be interrupted between any of them, so two threads can both load the old value and lose an increment

Hardware provides atomicity only for a few single instructions like ==compare-and-swap== and ==fetch-and-add==; ordinary compound expressions get none.

Atomic does not mean ==instant==, and putting a compound expression on one source line does not make it atomic.
