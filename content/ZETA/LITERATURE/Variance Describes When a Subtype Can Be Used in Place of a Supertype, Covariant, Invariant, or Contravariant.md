---
up:
  - "[[Functional Programming programs are trees of expressions, not sequences of steps]]"
tags:
  - atomic
created: 2026-05-05 11:40
---

Variance describes what types are subtypes of other types and when a type can be used in place of a supertype (and viceversa).
For example, Turtle is a subtype of Animal and in Java you can pass Turtle to a function that accepts an Animal.

All types with generic parameters have a variance with respect to those parameters. 
There are three kinds of variance:
- **covariant**, a subtype can be used in place of the type. If `Turtle <: Animal`, then `List<Turtle> <: List<Animal>` 
- **invariant**, you must provide exactly the given type; neither subtype nor supertype is accepted 
- **contravariant** — a supertype can be used in place of the type. Function argument types are contravariant: a function that accepts `Animal` can be used where a function that accepts `Turtle` is expected, because it handles more
# See also 
- [[Chomsky hierarchy - Regular < Context-Free < Context-Sensitive < Recursively Enumerable]] — the Chomsky hierarchy is a subtype relationship between language classes: a Regular language is a subtype of Context-Free; covariance applies here too 
- [[Functional Programming programs are trees of expressions, not sequences of steps]] — contravariance of function arguments is most visible in functional programming: a more general function (`Animal -> Bool`) can safely replace a more specific one (`Turtle -> Bool`)

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.