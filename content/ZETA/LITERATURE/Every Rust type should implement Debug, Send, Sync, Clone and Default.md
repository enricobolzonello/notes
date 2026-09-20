---
up:
  - "[[Principle of Least Astonishment]]"
tags:
  - atomic
created: 2026-05-06 11:09
---

Common traits and their priority:
- `Debug` - every type should implement it
- `Send` and `Sync` - implement unless there is a specific reason not to. No `Send` means the type can't be sent to another thread (no thread pools, no `Mutex<T>`). No `Sync` means a [[&T Is a Shared Reference, Copy but Not Mutable|shared reference]] to the type can't be sent across threads (no `Arc<T>` or `static`)
- `Clone` and `Default` - must implement
- `PartialEq`, `PartialOrd`, `Hash`, `Eq` and `Ord` - where possible implement them, especially `PartialEq` and `PartialOrd` 
- `Serialize` and `Deserialize` - most libraries choose to provide a `serde` feature flag to not force a dependency

# See also
- [[Principle of Least Astonishment]] - implementing standard traits is a Least Astonishment expectation
- [[&T Is a Shared Reference, Copy but Not Mutable]] - `Sync` is the thread-safety equivalent of `&T`. `T` is `Sync` if and only if `&T` is `Send`
- [[Interior Mutability Allows Mutation Through &T, Either by Runtime-Checked Exclusivity or In-Place Methods]] - types with interior mutability are not `Sync` because shared references could race
- [[Interface Segregation Principle (ISP)]] - the `serde` feature flag pattern is ISP applied to Rust crates: don't force a `serde` dependency on callers who don't need serialisation

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.