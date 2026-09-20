---
up:
  - "[[Lifetimes]]"
tags:
  - atomic
created: 2026-05-04 20:02
---

In Rust as a high level view you can imagine variables just as names. When a variable is accessed, you can imagine drawing a line from the previous access to the new one. This establishes a dependency relationship, called **flow**.

Flows can fork and merge, and each split has a distinct lifetime. The compiler checks if the graph is valid, as an example it checks:
- that two parallel flows do not have mutable access to a value
- that a flow that borrows a value while there is no flow that owns the value exists

To understand it, see the following code:
```rust
let mut x;
x=42;
let y=&x;
x=43;
assert_eq!(*y, 42);
```

which has two flows: line 2-4 (with one mutable access) and line 3-5 (with a reference). This code fails to compile since it has both an exclusive write (line 4) and an shared borrow (line 5).

# See also
- [[Lifetimes]] — lifetimes are the compiler's implementation of the flow validity check: each flow has a lifetime, and the borrow checker validates that no two incompatible flows overlap
- [[Reference Types and Interior Mutability]] — the two types of flows are exactly shared references (&T) and exclusive references (&mut T); the flow model is the intuition, the reference type system is the mechanism
- [[Single Writer Principle, one thread own all writes to a resource]] — the compiler's flow validation is the static enforcement of the single writer principle: no exclusive write flow can coexist with any other flow, just as no thread can write while another holds a reference
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — the flow model prevents false sharing at the language level: two parallel exclusive flows to the same value are a compile error before they can ever become a hardware cache conflict
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — lifetimes ensure references don't outlive the stack frames they point to; the flow model is what prevents the dangling pointer problem that C solved with destructors but never fully eliminated

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.