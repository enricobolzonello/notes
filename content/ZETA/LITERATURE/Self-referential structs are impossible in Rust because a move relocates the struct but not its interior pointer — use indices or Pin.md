---
up:
  - "[[Rust compiler validates a graph of flows between accesses]]"
tags:
  - atomic
created: 2026-09-10 10:40
---
You can't write a struct where one field holds a reference into another field of the *same* struct:

```rust
struct SelfRef {
    text: String,
    title: Option<&str>, // slice into `text` — won't compile
}
```

**Why it's forbidden (the semantic reason, not the syntax one):** Rust values can *move* — stack↔heap, or to a new location on assignment/passing. A move relocates the whole struct, but an interior pointer would still hold the **old** address, now pointing at freed/garbage memory, and there's no mechanism to fix up the pointer during the move. So the borrow checker refuses the construction. (The surface symptom is "missing lifetime specifier," but the real issue is move-invalidation.)

**Fixes:**
- **Indices/ranges** instead of references (e.g. `title: Option<Range<usize>>` into `text`). Offsets survive a move and are invisible to the borrow checker — but they become fragile pseudo-pointers that can go out of sync (same drawback as index-as-pointer designs).
- **`Pin`** — pins a value in place, guaranteeing it never moves, so interior self-references stay valid. This is the primary motivation for `Pin`, which underpins `async` (a pending `async` block captures its environment *and* references into it — inherently self-referential).
- Crates like `ouroboros` that encapsulate the difficulty.

General advice: **avoid self-referential data structures**; prefer owning data or restructure.

# See also
- [[The borrow rule (many &T XOR one &mut T) exists to guarantee no aliased mutation — enabling optimization and data-race-freedom]] — both are consequences of Rust references being *borrowed* pointers into movable data; the borrow checker polices reference validity, and moves are what make self-references unpoliceable
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — moving is an owner-only power, and the reason a move can't coexist with a live interior reference is the same exclusivity logic
- [[If your code must own data, make the caller provide it. Use Cow when ownership is decided at runtime]] — the "prefer owning data" escape from lifetime tangles applies here too: owning avoids the self-reference trap entirely
- [[A Lifetime Names the Region of Code a Reference Must Be Valid For, Not Necessarily the Full Scope]] — a self-reference would need a lifetime internal to the struct, which the lifetime system can't express (lifetimes are for things external to the value)

# References
- Effective Rust, Item 15: "Understand the borrow checker" — https://lurklurk.org/effective-rust/borrows.html

# Questions
#flashcards/rust

Why can't a Rust struct hold a reference into another of its own fields?::Values can *move*, relocating the struct; the interior pointer would still hold the old (now-invalid) address with no way to fix it up. So the borrow checker forbids it.
<!--SR:!2026-09-16,1,228-->

What are the two main ways to work around the need for a self-referential struct?::Store indices/ranges into the data (survive moves, invisible to the borrow checker but fragile), or use `Pin` to guarantee the value never moves (the motivation behind `async`).
<!--SR:!2026-09-16,1,230-->

`Pin` exists to ==pin a value in place so it never moves==, keeping interior self-references valid — which is why it underpins `async`.
