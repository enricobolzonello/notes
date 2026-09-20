---
up:
  - "[[Rust compiler validates a graph of flows between accesses]]"
tags:
  - atomic
created: 2026-05-05 10:47
---

`&T` is a pointer that may be shared and it's called **shared reference**. Each shared reference is `Copy`, so it can be duplicated without consuming the original, but it is not mutable and cast to a mutable one is not allowed.

Some edge cases exist to the last rule, see [[Reference Types and Interior Mutability#Interior mutability]]


# See also
- [[Rust compiler validates a graph of flows between accesses]] — a shared reference creates a shared flow; multiple shared flows can coexist, but none can overlap with an exclusive flow (`&mut T`)
- [[Reference Types and Interior Mutability]] — the complete picture: `&T` is not "immutable" but "shared"; interior mutability is the controlled mechanism for mutation through a shared reference
- [[Lifetimes]] — every `&T` has an associated lifetime; the borrow checker validates that the shared reference does not outlive the value it points to
- [['static Means Valid Until Program Shutdown — Static Variables Have It, But Not All 'static References Point to Static Memory]] — a `&'static T` is a shared reference with the longest possible lifetime; string literals are the most common example
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — at the hardware level, multiple shared references reading the same cache line is safe and efficient; false sharing only occurs when writes are involved, which `&T` prevents at the language level

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.