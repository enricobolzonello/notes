---
up:
  - "[[The store-buffer litmus test proves mutual exclusion is not enough]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
The [[The store-buffer litmus test proves mutual exclusion is not enough|store-buffer litmus test]] showed a second axis exists: whether writes become *visible* and *in order* to other threads. We need a *precise* rule for this — not "eventually, probably", but an exact statement of when one thread's memory effects are guaranteed seen by another.

That rule is the **happens-before** relation. If action $A$ happens-before action $B$, then $A$'s memory effects are guaranteed **visible to** $B$ and $A$ is guaranteed **ordered before** $B$. Visibility and ordering are not two separate guarantees — they are the two *observable effects* of this one relation.

You get a happens-before edge in exactly two ways, closed under transitivity:

1. **Program order** — within a *single* thread, if $A$ is written before $B$, then $A \to B$. (This is why single-threaded code always behaves.)
2. **Synchronizes-with** — a synchronizing action in one thread creates an edge into a matching action in another. This is the **only** way to get an edge that crosses thread boundaries.
3. **Transitivity** — if $A \to B$ and $B \to C$ then $A \to C$. Program-order edges chain *through* a cross-thread synchronizes-with edge to reach into the other thread.

The key insight: **the litmus test had no synchronizes-with edge** — only program-order edges, which say nothing across threads. No cross-thread edge → no visibility guarantee → both-read-0 is legal. To make one thread's write visible to another you must *manufacture* a synchronizes-with edge. Happens-before is a **causal**, not literal-temporal, guarantee: it constrains what effects must appear, not the wall-clock order the CPU actually executes in.

# See also
- [[The store-buffer litmus test proves mutual exclusion is not enough]] — this relation is the second guarantee that test demands; the test fails precisely because it establishes no synchronizes-with edge
- [[Acquire and release are the half-barriers that manufacture a synchronizes-with edge]] — the concrete mechanism for creating the cross-thread edge happens-before requires
- [[A lock provides two guarantees, mutual exclusion and a happens-before edge]] — a lock's unlock/lock pair is one way to create the synchronizes-with edge, giving this guarantee
- [[RCU allows one updater and many readers concurrently]] — RCU's grace period is a happens-before argument: reclamation waits until all readers' read-side critical sections have ended, establishing the ordering that makes reuse safe

# References
- https://docs.oracle.com/javase/specs/jls/se7/html/jls-17.html

# Questions
#flashcards/stem/os

What does "A happens-before B" guarantee?::A's memory effects are visible to B and A is ordered before B — visibility and ordering are the two observable effects of the one relation

What are the two kinds of happens-before edge, and which crosses threads?::Program order (within one thread) and synchronizes-with (across threads); only synchronizes-with crosses thread boundaries. Both are closed under transitivity

To make one thread's write visible to another, you must manufacture a ==synchronizes-with== edge; program order alone never crosses threads.

Happens-before is a ==causal== guarantee, not a literal-temporal one — it constrains which effects must appear, not the CPU's actual execution order.
