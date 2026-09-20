---
up:
  - "[[Coherence guarantees one impl per (trait, type) pair, enforced by the orphan rule and no-overlap]]"
tags:
  - atomic
created: 2026-09-15 09:43
---
A surprising fact: **Cargo can link multiple incompatible versions of the same crate into one binary.** Your binary can use `rand 0.8` while a dependency internally uses `rand 0.7`, and it just works — Cargo namespaces them as effectively *distinct crates* with *distinct types* (think `rand_v0_7::Rng` vs `rand_v0_8::Rng`). Most languages can't do this; Rust can.

This coexistence is **harmless while the dependency stays internal** (a *private* dependency): the binary never sees the library's `rand` types, so the two versions live in separate worlds.

It **breaks only when a version leaks into a public API** (a *public dependency*). If `dep-lib` exposes a `rand 0.7` type in a signature:

```rust
// dep-lib, built against rand 0.7
pub fn pick_number_with<R: Rng>(rng: &mut R, n: usize) -> usize { ... }
```

then the binary (holding a `rand 0.8` rng) can't satisfy it: the two versions are *distinct types*, so the `0.8` type doesn't implement the `0.7` trait. The compile error is baffling — `RngCore is not implemented for ThreadRng` — because it's really `RngCore_v0_7` unimplemented while the binary only has `v0.8`.

**Fix (the Item's title): the library re-exports the dependency.**
```rust
pub use rand; // in dep-lib
```
Now callers can name the *exact* version via `dep_lib::rand`, and construct matching-version arguments (`dep_lib::rand::thread_rng()`). Re-export the *whole crate* (not just the type) so its constructors come too. It's the library author's job — otherwise the binary author needs an awkward wrapper crate.

**Deeper caveat:** putting another crate's type in your API makes it a *public dependency* and couples your SemVer to theirs — their major bump forces *your* major bump. So think carefully before exposing a foreign type; re-export it when you do.

# See also
- [[Coherence guarantees one impl per (trait, type) pair, enforced by the orphan rule and no-overlap]] — the root cause is the same type-identity tracking: two crate versions are distinct types, so an impl/trait for one is not the impl/trait for the other
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — a public dependency is part of your observable API; Hyrum's Law says users will depend on the exact version's types, which is why a version bump is a breaking change
- [[non_exhaustive attribute prevents implicit construction and exhaustive matching outside the crate]] — both are about the crate boundary: what downstream code can see and rely on, and how that constrains a library's versioning

# References
- Effective Rust, Item 24: "Re-export dependencies whose types appear in your API" — https://lurklurk.org/effective-rust/re-export.html

# Questions
#flashcards/rust

Can Cargo link two incompatible versions of the same crate into one binary?::Yes — it namespaces them as effectively distinct crates with distinct types (e.g. `rand_v0_7::Rng` vs `rand_v0_8::Rng`), and they coexist transparently.

When does having two versions of a crate actually cause a problem?::Only when a version leaks into a *public API* (a public dependency): the caller's version and the library's required version are distinct, incompatible types, giving a confusing "trait not implemented" error.

How does a library author fix the public-dependency version clash?::`pub use` the dependency (re-export it), so callers can name its exact version via `dep_lib::dep` and build matching-version arguments.

Exposing another crate's type in your public API couples your ==SemVer to theirs== — their major bump forces your major bump.
