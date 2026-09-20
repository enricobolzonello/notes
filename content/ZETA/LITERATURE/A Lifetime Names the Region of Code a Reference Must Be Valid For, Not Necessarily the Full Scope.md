---
up:
  - "[[Lifetimes]]"
tags:
  - atomic
created: 2026-05-05 11:17
---
A **lifetime** is the name for a region of code that some reference must be valid for. Often it coincides with scope, but not necessarily.

Whenever a reference with some lifetime `'a` is used, the borrow checker checks that it is still alive by tracing back and checking there is no conflicts along the path.
That's why it does not always coincides with scope. Consider the following example:
```rust
let mut x = Box::new(42);
let r = &x;
if rand() > 0.5 {
	*x=84; 
} else {
	println!("{}", r);
}
```
The lifetime created at line 2 is not extended into line 5 branch.

# See also
- [[Lifetimes]] — the broader reference: lifetime annotations, struct definitions, the `'static` lifetime, and the evolution from C/C++ dangling pointers to Rust's compile-time guarantees
- [[Rust compiler validates a graph of flows between accesses]] — a lifetime is the name for the span of a flow in the graph; the borrow checker validates lifetimes by tracing the flow and checking for conflicts along the path
- [['static Means Valid Until Program Shutdown — Static Variables Have It, But Not All 'static References Point to Static Memory]] — `'static` is the special case where the lifetime spans the entire program; the longest possible region of code
- [[&T Is a Shared Reference, Copy but Not Mutable]] — every `&T` has an associated lifetime; the borrow checker ensures the shared reference does not outlive the value it points to
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — same applies to `&mut T`; the exclusive flow has a lifetime, and the borrow checker rejects any other flow that overlaps with it

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.