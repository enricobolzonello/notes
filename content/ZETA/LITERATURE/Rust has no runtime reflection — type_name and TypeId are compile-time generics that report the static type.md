---
up:
  - "[[Generics keep the concrete type, trait objects erase it — that lever generates every tradeoff]]"
tags:
  - atomic
created: 2026-09-14 09:55
---
**Reflection** = a program inspecting a value's type *at runtime* (Java/Go/Python: determine type, explore fields, invoke methods). **Rust has none of this** — and can't, by design. Its default is the opposite: types are resolved at *compile time* (monomorphization) or *erased* (trait objects), so a value carries no "what am I" tag at runtime. There's nothing to reflect on.

The `std::any` helpers *look* reflective but aren't — they're **compile-time generics**:

- `std::any::type_name::<T>()` — generic, so `type_name::<u32>` and `type_name::<Square>` are different monomorphized functions, each baking in a statically-known type. Returns a *diagnostic* string; best-effort, may change, may not be unique — **don't parse it**.
- `TypeId::of::<T>()` — compile-time, unique, code-usable type identifier.

The tell that proves it's compile-time, not runtime: feed a *trait object*.

```rust
let square = Square::new(1, 2, 2);
let shape: &dyn Shape = &square;
println!("{}", type_name_of(&shape)); // "&dyn Shape", NOT "Square"
```

It reports the **static** type of the reference (`&dyn Shape`), not the concrete `Square`, because forming the trait object *erased* the concrete type — nothing at runtime carries it. Real reflection (Java/Go) would report the runtime `Square`.

# See also
- [[Generics keep the concrete type, trait objects erase it — that lever generates every tradeoff]] — the erasure half of that lever is exactly why there's no runtime type to reflect on; `type_name` on a trait object returns the static `&dyn` type
- [['static Means Valid Until Program Shutdown — Static Variables Have It, But Not All 'static References Point to Static Memory]] — `TypeId`/`Any` require `T: 'static` because `TypeId` ignores lifetimes, so non-`'static` references are excluded to stay sound
- [[Object safety is whether a vtable can be built; where Self Sized carves offending methods out of the dyn interface]] — both are about what a trait object's vtable can/can't carry; the vtable holds methods, not a general "what traits do I implement" record

# References
- Effective Rust, Item 19: "Avoid reflection" — https://lurklurk.org/effective-rust/reflection.html

# Questions
#flashcards/rust

Does Rust have runtime reflection (inspect a value's type at runtime like Java/Go)?::No. Types are resolved at compile time (monomorphization) or erased (trait objects); values carry no runtime type tag, so there's nothing to reflect on.
<!--SR:!2026-09-18,3,250-->

How do `type_name::<T>()` and `TypeId::of::<T>()` work?::They're compile-time generic functions monomorphized per type — they report the *static* type parameter `T`, with no runtime inspection.

For `shape: &dyn Shape` backing a `Square`, `type_name` reports ==`&dyn Shape`== (the static reference type), not `Square`, because the concrete type was erased.
