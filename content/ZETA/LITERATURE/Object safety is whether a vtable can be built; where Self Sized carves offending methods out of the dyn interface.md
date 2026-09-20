---
up:
  - "[[Generics keep the concrete type, trait objects erase it — that lever generates every tradeoff]]"
tags:
  - atomic
created: 2026-09-08 09:54
---
**Object safety** answers one question: *can the compiler build a vtable for this trait?* Only object-safe traits can become trait objects (`&dyn Trait`). Two rules, each following from what a vtable is (a **finite** table of concrete function pointers) and what a trait object is (a value of **unknown size** — the concrete type is erased):

1. **No generic methods.** A method `fn f<T>(&self)` is an *infinite* family (`f::<i32>`, `f::<u8>`, …). You can't fit infinitely many entries into a fixed-size vtable.
2. **No method mentions `Self` beyond the receiver.** E.g. `fn clone(&self) -> Self`. The caller holding a `&dyn Trait` doesn't know the concrete type, so it can't reserve stack space for a `Self` return of unknown size. (This is why `Clone`/`Copy` bounds make a trait not object-safe.)

**The `where Self: Sized` escape hatch.** Put that bound on the offending method:

```rust
trait Stamp: Draw {
    fn make_copy(&self) -> Self where Self: Sized;
}
```

`where Self: Sized` means "this method only exists when `Self` has a known compile-time size." A trait object (`dyn Trait`) is **unsized**, so the method simply *doesn't apply* to it — it is **carved out** of the vtable. The mechanism is **subtractive, not additive**: nothing is added to the vtable; the offender is *removed*. With it gone, the remaining methods form a valid vtable → `&dyn Stamp` is constructible. The cost: `make_copy` is callable only on concrete sized types (`square.make_copy()`), never through the trait object (`stamp.make_copy()` won't compile).

# See also
- [[Generics keep the concrete type, trait objects erase it — that lever generates every tradeoff]] — object safety is the gatekeeper for the *erase-the-type* path; a trait must be object-safe before it can be a `&dyn`
- [[Coherence guarantees one impl per (trait, type) pair, enforced by the orphan rule and no-overlap]] — both are about what the compiler can mechanically construct for a trait: one impl per pair (coherence) and one buildable vtable (object safety)
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — a `dyn Trait` is unsized, which is why trait objects always live behind a reference/pointer and why `Self: Sized` methods don't apply to them

# References
- Effective Rust, Item 12: "Understand the trade-offs between generics and trait objects" — https://lurklurk.org/effective-rust/generics.html

# Questions
#flashcards/rust

What two things make a trait NOT object-safe (unusable as `&dyn Trait`)?::(1) A generic method (an infinite family — can't fit in a fixed vtable); (2) a method mentioning `Self` beyond the receiver (caller can't size the erased return type).

Object safety is fundamentally the question: ==can the compiler build a vtable for this trait?==
<!--SR:!2026-09-16,1,230-->

How does `where Self: Sized` on a `Self`-returning method restore object safety?::A `dyn Trait` is unsized, so the method doesn't apply to it — it's *carved out* of the vtable (subtractive, not additive). The remaining methods form a valid vtable, so `&dyn Trait` becomes constructible; that method is then callable only on concrete sized types.
<!--SR:!2026-09-16,1,230-->
