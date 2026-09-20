---
up:
  - "[[A Lifetime Names the Region of Code a Reference Must Be Valid For, Not Necessarily the Full Scope]]"
tags:
  - atomic
created: 2026-05-05 11:40
---

All types with generic parameters have a [[Variance Describes When a Subtype Can Be Used in Place of a Supertype, Covariant, Invariant, or Contravariant|variance]] with respect to those parameters.

In Rust lifetimes form a subtype relationship: `'static` is a subtype of `'a` because it is valid for *longer*.

Key variance rules:
- `&'a T` is **covariant** in both `'a` and `T`: you can provide `&'static T` where `&'a T` is expected
- `&mut T` is **invariant** in `T`: you must provide exactly `T`, not a subtype or supertype
- function arguments are **contravariant** — a function that accepts a longer-lived reference can be used where a shorter-lived one is expected

# See also
- [[Variance Describes When a Subtype Can Be Used in Place of a Supertype, Covariant, Invariant, or Contravariant]] — the general concept this note applies to Rust lifetimes specifically
- [[A Lifetime Names the Region of Code a Reference Must Be Valid For, Not Necessarily the Full Scope]] — the subtype relationship between lifetimes is grounded in the definition: a longer lifetime is a subtype because it satisfies every constraint a shorter one would
- [['static Means Valid Until Program Shutdown — Static Variables Have It, But Not All 'static References Point to Static Memory]] — `'static` is the bottom of the lifetime subtype hierarchy: it is a subtype of every lifetime, which is why `&'static T` can be used wherever `&'a T` is expected
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — `&mut T` being invariant in `T` is a direct consequence of its exclusivity guarantee; covariance would allow type-unsafe writes through the exclusive reference
- [[Reliability means preventing faults from causing failures]] — invariance of `&mut T` is a compile-time reliability mechanism: the unsoundness it prevents (writing the wrong type through an exclusive reference) would be a fault that propagates silently into a failure

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.