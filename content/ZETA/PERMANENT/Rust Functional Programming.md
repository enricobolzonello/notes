---
connections:
  - "[[ZETA/LITERATURE/Functional Programming|Functional Programming]]"
tags:
  - permanent_note
type: permanent_note
created: 2025-04-13 18:46
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

Generics in C++ and Java are a meta construct for the compiler. For example, `vector<int>` and `vector<char>` in C++ are two different copies of the same code for a `vector` type. 
In Rust instead a generic type parameter creates a **type class constraint**. `Vec<isize>` and `Vec<char>` are two different types.

--> **monomorphization** = different types are created from polymorphic code [^1]

With this you can add not only additional behavior to a particular member of a type class, but extra behavior as well.


[^1]: This is the reason why Rust has compile time guarantees