---
up:
  - "[[Hash Tables · Crafting Interpreters]]"
tags:
  - atomic
created: 2026-03-29 10:46
---

A hash function takes an arbitrary value and outputs a fixed-size integer. Requirements: deterministic, uniform distribution, fast. One common implementation is FNV-1a:

```rust
pub trait Hashable {
    fn hash(&self) -> u32;
}

impl Hashable for String {
    fn hash(&self) -> u32 {
        let mut hash = 2166136261;
        for c in self.as_bytes() {
            hash = (hash ^ (*c as u32)).wrapping_mul(16777619);
        }
        hash
    }
}
```

# References
- https://craftinginterpreters.com/hash-tables.html#open-addressing

# See also
- [[SimHash - h(x) = sign(wᵀx)]] — a hash function designed specifically to preserve cosine similarity, rather than distribute uniformly