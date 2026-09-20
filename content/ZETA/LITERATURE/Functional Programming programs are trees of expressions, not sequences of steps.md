---
connections:
  - "[[Imperative paradigm]]"
tags:
  - atomic
created: 2025-04-13 17:55
---

> Paradigm where programs are constructed by applying and composing functions.

Rather than a sequence of [[Imperative paradigm|imperative]] statements, function definitions are trees of expressions that each return a value.

example:
```rust
println!("{}", (1..11).fold(0, |a, b| a + b));
```
We are describing what to do rather than how to do it.
`fold` is a function that composes functions [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse|composes functions]]


# See also
- [[Imperative paradigm]] — the contrasting paradigm: imperative describes how via mutable steps, functional describes what via expression trees
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — function composition is the core mechanism of functional programming; fold is composition made concrete
- [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — the actor model and functional programming share the principle of avoiding shared mutable state; FP eliminates mutation entirely, actors isolate it per actor
- [[Single Writer Principle, one thread own all writes to a resource]] — the single writer principle is the concurrency-safe approximation of functional immutability: if you can't eliminate mutation, at least confine it to one owner
- [[Tail Call optimization replaces call with jmp]] — tail call optimisation is particularly important in functional programming because recursion replaces loops; without TCO, deeply recursive functional programs overflow the stack
- [[Atomic Notes are high cohesion low coupling, reusable in multiple outputs]] — the software analogy that grounds the atomic note concept: functional programs compose small pure functions the same way a [[Zettelkasten]] composes atomic notes into essays