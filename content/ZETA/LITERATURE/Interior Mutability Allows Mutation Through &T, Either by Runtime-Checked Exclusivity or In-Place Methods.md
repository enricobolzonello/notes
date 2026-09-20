---
up:
  - "[[&T Is a Shared Reference, Copy but Not Mutable]]"
tags:
  - atomic
created: 2026-05-05 11:07
---

Some types allow you to mutate values through a shared reference with a mechanism called interior mutability.
There can be two categories:
- types like `Mutex` or `RefCell` which ensure that only one [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It|mutable reference]] and no [[&T Is a Shared Reference, Copy but Not Mutable|shared references]] exist at the same time
- types that do not give out a mutable reference to the inner value, but give methods to manipulate the value in place. Examples include the atomic integer types and `std::cell::Cell`

See [[Reference Types and Interior Mutability#Interior mutability]] for a complete list and comparison.

# See also
- [[&T Is a Shared Reference, Copy but Not Mutable]] — interior mutability is the controlled exception to `&T` being non-mutable; this note explains what that exception actually is
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — the first category of interior mutability types (`Mutex`, `RefCell`) enforces the same exclusivity guarantee as `&mut T`, just at runtime rather than compile time
- [[Reference Types and Interior Mutability]] — the complete lookup table: `Cell<T>`, `RefCell<T>`, `Mutex<T>`, `RwLock<T>`, when to use each
- [[Single Writer Principle, one thread own all writes to a resource]] — `Mutex<T>` is the runtime enforcement of the single writer principle: only one thread can hold the lock and mutate the value at a time
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — atomic types (the second category) are designed to avoid false sharing: they operate on values that fit in a single cache line and use hardware-level atomic instructions instead of locks
- [[Rust compiler validates a graph of flows between accesses]] — interior mutability moves the flow validation from compile time to runtime; `UnsafeCell<T>` tells the compiler to stop tracking the flow, and the type itself takes responsibility for enforcing exclusivity

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.