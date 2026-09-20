---
up:
  - "[[&T Is a Shared Reference, Copy but Not Mutable]]"
tags:
  - atomic
created: 2026-05-05 10:53
---

`&mut T` is called **mutable reference**: no other threads can access the target value, meaning it is *exclusive*. 
It lets you mutate only the memory location that the reference points to. 

Between owning and having a mutable you can do the same set of actions apart from two differences:
- owner is responsible for dropping the value
- if you move the value behind the mutable reference, then you must leave another value in its place

# See also
- [[&T Is a Shared Reference, Copy but Not Mutable]] — the direct contrast: `&T` allows many coexisting readers, `&mut T` allows exactly one writer and no readers simultaneously
- [[Rust compiler validates a graph of flows between accesses]] — `&mut T` creates an exclusive flow in the graph: the compiler rejects any other flow to the same value while the exclusive flow is live
- [[Reference Types and Interior Mutability]] — the deeper framing: `&mut T` is not "mutable reference" but "exclusive reference"; interior mutability is what allows mutation through &T in controlled circumstances
- [[Single Writer Principle, one thread own all writes to a resource]] — `&mut T` is the compiler-enforced version of the single writer principle: exclusive access to a value is guaranteed statically, not through runtime coordination

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.