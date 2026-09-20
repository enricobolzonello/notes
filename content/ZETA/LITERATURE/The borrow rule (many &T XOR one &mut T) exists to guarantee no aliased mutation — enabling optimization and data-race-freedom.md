---
up:
  - "[[Rust compiler validates a graph of flows between accesses]]"
tags:
  - atomic
created: 2026-09-10 10:40
---
The borrow rule — at any point, either **many `&T`** (shared) **XOR** exactly **one `&mut T`** (exclusive), never both — isn't arbitrary strictness. It exists to give the compiler a hard **aliasing guarantee**: *data reachable through immutable references can never be mutated via some aliased mutable reference at the same time.*

That guarantee buys two concrete things:

1. **Optimization.** The compiler can cache a value in a register across a stretch of code, knowing no hidden aliased write can invalidate it. In C/C++ two pointers *might* alias, so the compiler must conservatively re-read from memory; Rust's rule lets it assume they don't.
2. **Data-race-freedom.** A data race requires a concurrent read and write (or two writes) to the same location. Since you can't have a shared borrow and an exclusive borrow coexist, unsynchronized concurrent mutation is impossible *by construction* — this is the static half of Rust's `Send`/`Sync` story.

So "many-shared XOR one-exclusive" is the single rule that makes both aggressive optimization *and* memory/thread safety sound at once.

# See also
- [[Rust compiler validates a graph of flows between accesses]] — this is the *why* behind that note's flow-validity check: forbidding two overlapping flows where one is exclusive is exactly what produces the no-aliased-mutation guarantee
- [[Single Writer Principle, one thread own all writes to a resource]] — the borrow rule is the compile-time enforcement of the single-writer principle: one exclusive writer, no concurrent readers, at the language level
- [[Happens-before is the single relation guaranteeing visibility and ordering across threads]] — aliasing control is why Rust can prevent data races statically, whereas runtime concurrency relies on happens-before edges to order accesses that *do* alias
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — the exclusivity of `&mut T` is precisely the mechanism that delivers the no-aliased-mutation guarantee

# References
- Effective Rust, Item 15: "Understand the borrow checker" — https://lurklurk.org/effective-rust/borrows.html

# Questions
#flashcards/rust

Why does the borrow rule (many `&T` XOR one `&mut T`) exist \u2014 what does it buy the compiler?::A hard aliasing guarantee: shared data can't be mutated via an aliased `&mut` concurrently. This enables register-caching optimizations (no hidden write invalidates a cached value) and makes data races impossible by construction.

The no-aliased-mutation guarantee makes both ==aggressive optimization== and ==data-race-freedom== sound at the same time.

Why can C/C++ not cache a value in a register as aggressively as Rust across pointer operations?::Two C/C++ pointers might alias, so a write through one could invalidate a value read through another — the compiler must conservatively re-read from memory. Rust's borrow rule rules out that aliasing.
<!--SR:!2026-09-16,1,230-->
