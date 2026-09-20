---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-06-16 06:57
---
When you need to remove an implementation of a trait, you can use **negative impls**. The feature is nightly only, and needs to be enabled with `#![feature(negative_impls)]`. 

Then you can use it like this:
```rust
#![feature(negative_impls)]

// I have some magic semantics for some synchronization primitive!
struct SpecialThreadToken(u8);

impl !Send for SpecialThreadToken {}
impl !Sync for SpecialThreadToken {}
```

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.