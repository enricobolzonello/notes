---
up:
  - "[[Every Rust type should implement Debug, Send, Sync, Clone and Default]]"
tags:
  - atomic
created: 2026-05-06 11:09
---
 When you define a new trait, you'll usually want to provide blanket implementations for that trait for:
 - `&T`, no dereferencing with [[&T Is a Shared Reference, Copy but Not Mutable|shared references]]
 - `&mut T`, same as above
 - `Box<T>`, for heap-allocated types

For ergonomics, also consider:
-  `IntoIterator`  for both `&T` and `&mut T` to have for loops
- `Deref` if you provide a transparent type (like `Arc`) allows calling methods on the inner type via `.`. Avoid it on types in which you don't know in advance the inner type

# See also
- [[Principle of Least Astonishment]]
- [[Every Rust type should implement Debug, Send, Sync, Clone and Default]] - the parent: first focus on standard traits
- [[OCP - software should be open for extension and closed for modification]] - blanket implementations are open for extension

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.