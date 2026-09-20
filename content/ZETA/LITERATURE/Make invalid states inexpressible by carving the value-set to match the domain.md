---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-09-02 20:12
---
A type **is** exactly its set of legal values (its cardinality is that set's size: `bool` = 2, `u8` = 256, `()` = 1, an empty enum = 0). Once you see a type as a value-set, data-structure design becomes arithmetic:

- **structs multiply** — a struct is a *product type*, its value-set is the cartesian product of its fields'. `struct Pixel { on: bool, shade: u8 }` has $2 \times 256 = 512$ values, because fields coexist independently.
- **enums add** — an enum-with-fields is a *sum type*, its value-set is the disjoint (tagged) union of its variants'. `enum Color { Monochrome, Foreground(RgbColor) }` has $1 + |RgbColor|$ values, because a value is in one arm *or* the other.

The design lever: **a product over-counts.** Its value-set is strictly larger than the domain's legal states, so it can represent combinations the domain forbids. The tell is a comment policing an invariant the compiler doesn't:

```rust
pub struct DisplayProps {
    pub monochrome: bool,
    // fg_color must be (0,0,0) if monochrome is true.  <-- smell
    pub fg_color: RgbColor,
}
```

Fix it by choosing the algebra (here, a **sum**) whose value-set *equals* the domain's legal states:

```rust
pub enum Color { Monochrome, Foreground(RgbColor) }
```

Now `(monochrome, red)` isn't a value of the type — it has **no representation**, so it can't be constructed and there's nothing to check. That is what "make invalid states inexpressible" means: the invalid region is carved out of the value-set entirely.

**Inexpressible ≠ validating constructor.** A `new() -> Result<Self, E>` that rejects bad field combinations is weaker: the invalid value still *exists* in the type, can be built by bypassing `new`, and is only caught by a check that runs **at runtime**. Inexpressibility is a **compile-time impossibility** — the value simply cannot be typed.

**`Option` and `Result` are the two universal sums** applying this:
- `enum Option<T> { None, Some(T) }` — value-set $1 + |T|$, the "maybe absent" domain carved as a sum.
- `enum Result<T, E> { Ok(T), Err(E) }` — value-set $|T| + |E|$, "success or failure".

This is why a **sentinel** (`-1`, `nullptr`) is the anti-pattern for absence: it signals *in-band*, jamming "absent" into `T`'s own value-set so `-1` means both "the integer -1" and "no value" — re-creating the over-counting ambiguity. `Option` pulls "absent" *out-of-band* into a disjoint `None` variant, so it can never be confused with real data.

# See also
- [[The Newtype pattern wraps a single type in a single-field tuple struct]] — the other tool for the same goal: wrapping a `bool`/`String` in a newtype restricts its value-set and adds type-safety, best when the semantics are permanently fixed (use an enum instead if new alternatives may appear)
- [[non_exhaustive attribute prevents implicit construction and exhaustive matching outside the crate]] — because a fielded enum is a sum, adding a variant is a breaking change; `#[non_exhaustive]` is how a library keeps that value-set open for extension
- [[Principle of Least Astonishment]] — encoding invariants in the type (not a comment) makes the API's intent obvious to both the compiler and the reader
- [[Every Rust type should implement Debug, Send, Sync, Clone and Default]] — the flip side, standard *behaviour* to add once the *data* shape is right

# References
- Effective Rust, Item 1: "Use the type system to express your data structures" — https://lurklurk.org/effective-rust/use-types.html

# Questions
#flashcards/rust

Why is a struct called a *product type* and an enum-with-fields a *sum type*?::A struct's value-set is the cartesian product of its fields' value-sets (multiply — fields coexist independently); an enum's is the disjoint tagged union of its variants' (add — a value is in one arm or the other).

What is the essential difference between making a state inexpressible (sum type) and guarding it with a validating constructor (`new() -> Result`)?::Inexpressible = the bad value has no representation in the type (compile-time impossibility); validating constructor = the bad value still exists and is only rejected by a check that runs at runtime, bypassable if you skip `new`.
<!--SR:!2026-09-16,1,230-->

Why is a sentinel value (e.g. `-1` meaning "absent") worse than `Option<T>`?::The sentinel signals in-band — it overloads a value already inside `T`'s value-set to mean "absent", so "absent" isn't disjoint from real data. `Option` gives "absent" its own disjoint `None` variant (out-of-band).
<!--SR:!2026-09-18,3,250-->
