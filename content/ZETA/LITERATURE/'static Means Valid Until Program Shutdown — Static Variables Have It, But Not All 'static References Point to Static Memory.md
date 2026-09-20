---
up:
  - "[[Lifetimes]]"
tags:
  - atomic
created: 2026-05-04 20:15
---
Values in static memory live for the entire execution of the program. 

In Rust, holds memory for variables declared with `static` and also some constant values like strings. String literals (`&str`) are the most common example: they are stored in the binary's read-only data section and have `'static` lifetime by default, which is why `"hello"` has type `&'static str`.

`'static` (notice the ') marks a reference as being valid "as long as static memory is around" (until program shuts down). Static variables (`static`) have `'static` references but the reverse is not necessarily true: there can be `'static` references that do not point to static memory, used for example in traits.

Another example is `thread::spawn` which requires the closure to be `'static`: since the new thread can live longer than the calling thread, the new thread cannot refer to anything stored in the old thread. 

# See also
- [[Lifetimes]] — 'static is a lifetime annotation like any other, just with the special meaning of "outlives everything"; the borrow checker treats it as an upper bound on all other lifetimes
- [[Rust compiler validates a graph of flows between accesses]] — a 'static flow never ends: it is valid from creation until program shutdown; understanding the flow model explains why thread::spawn requires 'static closures — the spawned thread's flow must not depend on any flow that could end before it
- [[A process in operating systems is a program in execution]] — static memory is the data section of the process memory layout: it is allocated when the process is loaded and deallocated when the process terminates
- [[Reference Types and Interior Mutability]] — static variables with interior mutability (`Mutex<T>`, `RwLock<T>`) are the correct way to have shared mutable state with 'static lifetime; raw static mut is unsafe for the same reason two exclusive flows to the same value are rejected
- [[Single Writer Principle, one thread own all writes to a resource]] — thread::spawn requiring 'static is the compiler enforcing the single writer principle: the spawned thread cannot borrow from the calling thread's stack because ownership cannot be safely shared across threads without 'static guarantees