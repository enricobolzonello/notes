---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-09-02 20:43
---
**Coherence** is Rust's guarantee that for any pair (trait `T`, type `U`) there is **at most one** `impl T for U` in the *entire program* — across every crate linked together.

**Why it must exist:** without it, a `(trait, type)` pair could have multiple impls, so which one runs at a call site would be ambiguous — and the choice could change just by linking a different crate. That would let a harmless-looking new dependency silently alter behaviour (e.g. `Hash` inserting under one impl, looking up under another). Coherence makes trait-method resolution deterministic everywhere.

Coherence is a *goal*; the compiler enforces it (compiling one crate at a time, blind to all others) via **two guardrails**, one per threat:

- **Orphan rule** — guards the *cross-crate* threat. You may write `impl T for U` only if **`T` is local to your crate OR `U` is local**. Otherwise two unrelated crates could both write the same foreign-trait-for-foreign-type impl and collide at link time. The forbidden case is exactly *both foreign* (e.g. `impl Display for Vec<u8>`). An impl owning neither side is an "orphan" — no crate is entitled to it.
- **No-overlap** — guards the *within-visible-code* threat. Two impls whose type-patterns overlap (both match some pair) are rejected, because they'd both apply.

They are two mechanisms serving **one principle**, not two unrelated rules.

**Consequences (this is why Rust error handling looks the way it does):**
- Can't `impl Error for String` — both foreign (orphan). Fix: newtype it — `struct MyError(String)` makes the *type* local, so `impl Error for MyError` is allowed.
- A library must hand-write `impl From<io::Error> for MyError` itself: a downstream *user* owns none of `From`, `io::Error`, `MyError`, so the orphan rule makes it impossible for them. Providing it lets `?` auto-convert.
- **`anyhow` exists because of no-overlap.** The ergonomic catch-all `impl<E: Error> From<E> for WrappedError` overlaps the reflexive `impl<T> From<T> for T` (since `WrappedError: Error` too), so it's rejected. `anyhow` sidesteps this with a layer of `Box` indirection.

# See also
- [[The Newtype pattern wraps a single type in a single-field tuple struct]] — the standard escape hatch from the orphan rule: wrapping a foreign type in a local newtype makes the type local, so you can implement a foreign trait on it
- [[Use thiserror for structured error callers can match on, anyhow when error type doesn't matter]] — coherence is *why* those crates exist: `thiserror` automates the orphan-rule-mandated `From` boilerplate; `anyhow` sidesteps the no-overlap clash with the reflexive `From`
- [[Provide blanket implementations for &T, &mut T, Box<T> and IntoIterator, Deref for ergonomics]] — blanket impls are powerful *because* coherence lets exactly one exist; they also cause the reflexive-`From` overlap that blocks catch-all wrappers
- [[Implementation from traits can be removed with negative impls]] — another way the compiler reasons about which impls exist for a type; both are about controlling the single-impl-per-pair space
- [[non_exhaustive attribute prevents implicit construction and exhaustive matching outside the crate]] — another local-vs-foreign-crate boundary rule: what downstream crates are and aren't allowed to do with your types

# References
- Effective Rust, Item 4: "Prefer idiomatic Error types" — https://lurklurk.org/effective-rust/errors.html

# Questions
#flashcards/rust

What is coherence in Rust, and why must it exist?::The guarantee that for any (trait, type) pair there is at most one `impl` in the whole program. Without it, which impl runs at a call site would be ambiguous and could change just by linking a different crate.
<!--SR:!2026-09-18,3,250-->

What does the orphan rule allow?::You may `impl T for U` only if the trait `T` OR the type `U` is local to your crate. The forbidden case is a foreign trait for a foreign type (you own neither side).

The orphan rule and the no-overlap rule are ==two enforcement mechanisms for the same goal, coherence== — the orphan rule guards the cross-crate threat, no-overlap guards the within-visible-code threat.

Why does `anyhow` need to exist rather than just writing `impl<E: Error> From<E> for MyWrapper`?::Because `MyWrapper: Error` too, so that blanket impl overlaps the reflexive `impl<T> From<T> for T` — a coherence (no-overlap) violation. `anyhow` sidesteps it with a layer of `Box` indirection.
