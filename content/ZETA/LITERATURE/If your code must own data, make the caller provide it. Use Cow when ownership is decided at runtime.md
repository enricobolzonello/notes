---
up:
  - "[[Rust compiler validates a graph of flows between accesses]]"
tags:
  - atomic
created: 2026-05-14 17:34
---
In functions you will have to deal with the choice of passing **a reference or owned data**. Usually the choice is made by the function itself:

> If your code must own data, make the caller provide owned data

There are cases when you don't know until runtime, such as in return types to represent functions that sometimes allocate. For this case, `Cow` can be used, which lets you represent data that may be owned by holding either a reference or an owned value. `Cow` means **Clone-On-Write** and it only clones when mutation is needed.

In general, if you cannot reference due to lifetime issues, first clone inexpensive data then heap allocate huge chunk of bytes if it is performance sensitive.

# See also
- [[Rust compiler validates a graph of flows between accesses]] — owned data takes over the flow entirely; a reference borrows the flow for a limited region; the function signature is the declaration of which kind of flow is needed
- [[A Lifetime Names the Region of Code a Reference Must Be Valid For, Not Necessarily the Full Scope]] — lifetime issues are the primary reason to prefer owned over borrowed: when a reference cannot outlive the region it needs to, ownership is the only option
- [[&T Is a Shared Reference, Copy but Not Mutable]] — passing `&T` is the borrow path: the caller retains ownership, the function gets a shared flow for the duration of the call
- [[&mut T Is an Exclusive Reference, No Other Reference Can Coexist With It]] — passing `&mut T` is the exclusive borrow path: the caller retains ownership and drop responsibility, the function gets temporary exclusive access
- [[`tracing` models execution as spans and events, richer than flat logging because it captures context]] — `Cow<'_, str>` is the idiomatic return type for functions that format log messages: return the original `&str` if no formatting is needed, allocate a `String` only if it is

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.