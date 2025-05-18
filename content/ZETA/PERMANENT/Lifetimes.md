---
connections:
  - "[[ZETA/PERMANENT/Rust.md|Rust]]"
tags:
  - permanent_note
  - theme/engineering
  - theme/rust
type: permanent_note
created: 2025-03-11 10:12
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

Lifetimes ensures that references are valid as long as we need them. 
Most of the time they are implicit (remember the rules of out of scope), they must be annotated only when multiple types are possible. 

The Rust compiler has a borrow checker that compares scopes to determine whether all borrows are valid.

```rust
fn main() {
    let r;                // ---------+-- 'a
                          //          |
    {                     //          |
        let x = 5;        // -+-- 'b  |
        r = &x;           //  |       |
    }                     // -+       |
                          //          |
    println!("r: {r}");   //          |
}                         // ---------+
```
For example, in this case the inner `'b` block is smaller than the outer `'a` lifetime block, so the code will not compile. If it would, `r` would be referencing memory that was deallocated when `x` went out of scope, making `r` buggy.

# Evolution of Lifetimes
The concept of lifetimes is not new, at least in practice it was used also in C and C++. Values stored on the stack are temporary, what happens if you hold onto a pointer of the temporary stack values?

In old C it was OK to return a pointer to a local variable:
```c
/* C code. */ 
struct File { 
	int fd; 
}; 

struct File* open_bugged() { 
	struct File f = { open("README.md", O_RDONLY) };
	return &f; /* return address of stack object! */ 
}
```
If you are unlucky, this *appears* to work. For example, if the calling code uses the returned value immediately it works, but as soon as any other function calls happen, the stack area will be reused and the memory will be overwritten. On top on not working, it will also leak the resource.

In C++, this problem was solved by including destructors. The caller now gets an invalid pointer and the resources are reclaimed, but it's still possible to hold onto a pointer to an object that's gone. 

# Rust Approach
Rust brings this concept to the foreground of the language, where every type that includes `&` has an associated lifetime, even if implicit. 

> [!DEFINITION]
> The lifetime of an item on the stack is the period where the item is guaranteed to stay in the same place. 

## Lifetime Annotations
-> don't change how long references live
They describe relationship of the lifetimes of multiple references to each other. This means that the borrow checker should reject any values that don't adhere to these constraints. 
```rust
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```
Cleary, only one lifetime is useless. Let's consider a more concrete example, a function that returns a pointer to the longest string:

```rust
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
This code will not compile because the compiler cannot tell whether the reference being returned refers to `x` or `y`. Let's add the lifetime `'a` to each reference:

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
Now all string slices (both in input and output) will need to live at least as long as lifetime `'a`. 

## Struct Definitions
To hold references in structs you need to a lifetime annotation on every reference.

```rust
struct ImportantExcerpt<'a> {
    part: &'a str,
}

fn main() {
    let novel = String::from("Call me Ishmael. Some years ago...");
    let first_sentence = novel.split('.').next().unwrap();
    let i = ImportantExcerpt {
        part: first_sentence,
    };
}
```

## `'static` Lifetime
What if there are no input lifetimes, but the output return includes a reference?
```rust
pub fn the_answer() -> &Item {
    // ...
}
```
This will not work, the only possibility is for the returned reference to have a lifetime that's guaranteed to never go out of scope, indicated by `'static`. This doesn't happen if:
- type has a destructor
- type has interior mutability



# References
- https://www.lurklurk.org/effective-rust/lifetimes.html