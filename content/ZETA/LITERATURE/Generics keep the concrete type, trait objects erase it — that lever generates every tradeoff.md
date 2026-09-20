---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-09-08 09:54
---
A trait can be used two ways — as a **trait bound on a generic** (`fn f<T: Draw>(x: &T)`) or as a **trait object** (`fn f(x: &dyn Draw)`). The single distinction that generates *every* tradeoff between them:

> **Generics keep the concrete type; trait objects erase it.**

- **Generics** are *monomorphized*: the compiler stamps out a specialized copy of the code per concrete `T`, so the concrete type is known at compile time.
- **Trait objects** are *fat pointers* (data ptr + vtable ptr, 16 bytes): the concrete type is erased, only the vtable of method pointers remains. One code instance handles all types.

Everything else is a consequence of keep-vs-erase:

| | Generics (type kept) | `&dyn Trait` (type erased) |
|---|---|---|
| Dispatch | static, inlinable | vtable, 2 derefs, slightly slower |
| Code size / compile time | one copy per type — bigger | one copy total — smaller |
| Multi-trait bounds | easy (`T: Debug + Draw`) | awkward (combinatorial helper traits) |
| Pass on to `Draw`-bounded code | ✓ (concrete type known) | can *call* Draw methods, but ✗ upcast `dyn Shape`→`dyn Draw` |
| Heterogeneous `Vec` | ✗ (each `T` is a distinct type) | ✓ (`Vec<&dyn Shape>`) |
| Runtime-loaded types (`dlopen`) | ✗ (nothing to monomorphize) | ✓ (only the vtable is needed) |

**Advice: prefer generics** (faster, best for multi-bounds), reach for trait objects when **type erasure is the feature you want** — smaller code / faster compiles, heterogeneous collections, or runtime-loaded types.

Note: `trait Shape: Draw` means *Shape also-implements Draw*, **not** *Shape is-a Draw*. The `dyn Shape` vtable includes Draw's methods (so you can call them), but there's no standalone Draw vtable, so you can't upcast `&dyn Shape` to `&dyn Draw` — no Liskov substitution.

# See also
- [[Object safety is whether a vtable can be built; where Self Sized carves offending methods out of the dyn interface]] — the constraint on *which* traits can even become trait objects; the erase-the-type half of this note is exactly why the vtable has to be buildable
- [[Coherence guarantees one impl per (trait, type) pair, enforced by the orphan rule and no-overlap]] — the vtable and the blanket-impl machinery both rest on there being exactly one impl of a trait for a type
- [[Variance Describes When a Subtype Can Be Used in Place of a Supertype, Covariant, Invariant, or Contravariant]] — the no-upcast limitation is the concrete Rust example of *lacking* the subtype substitution that variance describes elsewhere
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — trait objects are always behind a reference/pointer (`&dyn`, `Box<dyn>`) because the erased type is unsized

# References
- Effective Rust, Item 12: "Understand the trade-offs between generics and trait objects" — https://lurklurk.org/effective-rust/generics.html

# Questions
#flashcards/rust

What single distinction generates all the generics-vs-trait-objects tradeoffs?::Whether the concrete type is *kept* (generics/monomorphization) or *erased* (trait objects). Dispatch, code size, multi-bounds, upcasting, and heterogeneous collections all follow from that.
<!--SR:!2026-09-16,1,230-->

Generics are monomorphized so the concrete type is ==kept== (static dispatch, code bloat); trait objects are fat pointers so the concrete type is ==erased== (one code copy, vtable indirection).

When should you reach for a trait object instead of generics?::When type erasure is the goal — smaller code / faster compiles, heterogeneous collections (`Vec<&dyn Trait>`), or runtime-loaded (`dlopen`) types. Otherwise prefer generics.
<!--SR:!2026-09-16,1,230-->

Why can't you upcast `&dyn Shape` to `&dyn Draw` even though `trait Shape: Draw`?::`Shape: Draw` is *also-implements*, not *is-a*. The `dyn Shape` vtable includes Draw's methods (callable) but there's no standalone Draw vtable to convert to — no Liskov substitution.
<!--SR:!2026-09-16,1,230-->
