---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-05-18 17:39
---
> Tuple struct with a single field to make an opaque wrapper for the type. 

Example:
```rust
struct Password(String);
```

Motivation:
- share implementation details between types while controlling interface
- allow backward compatible changes -> promise less, break less
- distinguish units
- implementing foreign traits on foreign types

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.
- https://rust-unofficial.github.io/patterns/patterns/behavioural/newtype.html