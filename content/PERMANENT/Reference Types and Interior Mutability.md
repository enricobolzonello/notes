---
connections:
  - "[[ZETA/PERMANENT/Rust.md|Rust]]"
tags:
  - permanent_note
  - theme/engineering
  - theme/rust
type: permanent_note
created: 2025-01-31 11:30
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

# Reference Types
"immutable" means "non-exclusive". Actually non-mutable references can mutate with a process called "interior mutability", which happens when working with threads. 

The better naming would be **shared reference** and **exclusive reference**.

## Beginners view
A function that takes an argument by immutable reference is allowed to read the data behind the reference:
```rust
struct Point {
    x: u32,
    y: u32,
}

fn print_point(pt: &Point) {
    println!("x={} y={}", pt.x, pt.y);
}
```
but it is not allowed to mutate the data:
```rust
// gives error
fn embiggen_x(pt: &Point) {
    pt.x = pt.x * 2;
}
```

## Where it falls apart
`&T` is not an "immutable reference" or "const reference" to data of type `T` — it is a "shared reference". And `&mut T` is not a "mutable reference" — it is an "exclusive reference".

**Exclusive reference**:  no other reference to the same value could possibly exist at the same time.

**Shared reference**: other references to the same value might exist, on other threads or the caller's stack frame on the current thread.

In some cases, like [[Rust#Interior mutability]], shared references (`&T`) may mutate.

## Interior mutability
Interior mutability is the mutation through a shared reference. 

The std library `UnsafeCell<T>` is the **only way** to hold data that is mutable through a shared reference. This should not be used directly, there are abstractions over this type for different use cases, in particular:

|            | Mutable? | Description                                                                                                                                 |
|------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Cell<T>    | ✅        | single threaded and cannot obtain a reference to the content                                                                                |
| RefCell<T> | ✅        | single threaded and dynamically checked borrow rules will prevent attempts to mutate while a reader is holding a reference into the content |
| Mutex<T>   | ✅        | only one of the references may operate on the inner type at a time; other accesses will block until the current one has release its lock    |
| RwLock<T>  | ✅        | only one of the references may be used to mutate the type at a time, and only while no other references are being used for reading          

# References
- https://blog.reverberate.org/2021/12/18/thread-safety-cpp-rust.html
- https://docs.rs/dtolnay/0.0.9/dtolnay/macro._02__reference_types.html