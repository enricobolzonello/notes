---
connections:
tags:
  - permanent_note
  - type/index
type: permanent_note
created: 2025-01-31 10:52
---
Everything about Rust that I am learning!

## Index 
- [[#Memory Model]] 
- [[#Type System]] 
- [[#Functional Programming]] 
- [[#Concurrency]] 
- [[#Best Practices]] 
- [[#Internals]] 
- [[#Resources]]

---
## Memory Model

- [[Lifetimes]] - time associated to a reference to make sure it is still valid when we need it
    - [[Rust compiler validates a graph of flows between accesses]] - interpretation of the borrow checker
        - [[The borrow rule (many &T XOR one &mut T) exists to guarantee no aliased mutation — enabling optimization and data-race-freedom]] - the *why* behind the rule
        - [[Self-referential structs are impossible in Rust because a move relocates the struct but not its interior pointer — use indices or Pin]] - moves break interior pointers
        - [[&T Is a Shared Reference, Copy but Not Mutable]]
            - [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]]
            - [[Interior Mutability Allows Mutation Through &T, Either by Runtime-Checked Exclusivity or In-Place Methods]]
        - [[If your code must own data, make the caller provide it. Use Cow when ownership is decided at runtime]] - good practice
    - [[A Lifetime Names the Region of Code a Reference Must Be Valid For, Not Necessarily the Full Scope]] - lifetime definition
        - [[&a T is covariant in 'a and T, &mut T is invariant in T]]
    - [['static Means Valid Until Program Shutdown — Static Variables Have It, But Not All 'static References Point to Static Memory]]
- [[Reference Types and Interior Mutability]] - Explains the change of mentality between `&`T and `&mut T` from immutable and mutable to the correct ones: **shared and exclusive reference**.
- [[Recursion]] - Why recursion is not fully safe in Rust
- [[Smart Pointers]]

--- 

## Type System

- [[Principle of Least Astonishment]]
    - [[Every Rust type should implement Debug, Send, Sync, Clone and Default]] - good practice
        - [[Provide blanket implementations for &T, &mut T, Box<T> and IntoIterator, Deref for ergonomics]] - good practice
- [[Make invalid states inexpressible by carving the value-set to match the domain]] - types are value-sets; structs multiply, enums add
- [[Generics keep the concrete type, trait objects erase it — that lever generates every tradeoff]] - static dispatch vs. type erasure
    - [[Object safety is whether a vtable can be built; where Self Sized carves offending methods out of the dyn interface]] - the gatekeeper for `&dyn`
    - [[Rust has no runtime reflection — type_name and TypeId are compile-time generics that report the static type]] - no runtime type info
    - [[std::any::Any is opt-in type-preservation via a TypeId in the vtable — a keyhole that recovers only the original concrete type, not reflection]] - opt-in downcasting, not reflection
- [[The Newtype pattern wraps a single type in a single-field tuple struct]] - `NewType(type)`
- [[non_exhaustive attribute prevents implicit construction and exhaustive matching outside the crate]]
- [[Closures]]
- [[Implementation from traits can be removed with negative impls]]

--- 

## Functional Programming

- [[Rust Functional Programming]]
    - [[Variance Describes When a Subtype Can Be Used in Place of a Supertype, Covariant, Invariant, or Contravariant]]

--- 
## Concurrency 
- [[Asynchronous Programming in Rust - Carl Fredrik Samson]] 

--- 
## Best Practices 
- [[Use thiserror for structured error callers can match on, anyhow when error type doesn't matter]] 
- [[Consolidate integration tests into one crate and avoid doc tests]] 
- [[`tracing` models execution as spans and events, richer than flat logging because it captures context]] 
- [[Principle of Least Astonishment]]
- [[Rust code organization]]
- [[The Newtype pattern wraps a single type in a single-field tuple struct]] - `NewType(type)`
- [[non_exhaustive attribute prevents implicit construction and exhaustive matching outside the crate]]
- [[Cargo links multiple versions of a crate as distinct types, so a version leaking into a public API breaks callers — re-export the dependency]] - public dependencies & re-exporting

---
## Internals

- [[Negative Sign Tokens]]

---
## Resources
- [[Asynchronous Programming in Rust - Carl Fredrik Samson]]