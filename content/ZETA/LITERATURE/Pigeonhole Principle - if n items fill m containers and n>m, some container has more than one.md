---
up:
tags:
  - atomic
created: 2025-01-07 10:16
---

> [!definition]
> The pigeonhole principle states that if n items are put into m containers, with n > m, then at least one container must contain more than one item.
# See also
- [[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them]] — the direct application: hash tables map a large universe of keys into a smaller array; by the Pigeonhole Principle, collisions are mathematically guaranteed
- [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata]] — the control word stores h₂ fingerprints precisely because collisions are inevitable; the two-level check (h₂ then full key) is the engineering response to the Pigeonhole constraint
- [[Axiom of Choice - for each family of non-empty sets it exists a function f(S) in S]] — both are statements about sets and their elements; the Pigeonhole Principle is constructive (a contradiction follows directly), the Axiom of Choice is non-constructive (existence is postulated without construction)
# References
- https://en.wikipedia.org/wiki/Pigeonhole_principle