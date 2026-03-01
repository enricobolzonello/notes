---
connections:
tags:
  - permanent_note
  - theme/engineering
  - theme/rust
type: permanent_note
created: 2026-02-26 11:04
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> Anonymous functions that can be saved in a variable or passed as arguments to other functions

Features:
- can capture values from the scope
- no need for type annotation (can be added)
- can capture values from the environment in 3 ways, *based on what the body does*
	- borrow immutable
	- borrow mutable
	- taking ownership - with `move` keyword

The way a closure captures and handles values from the environment affects which traits the closure implements. This are the traits that can be implemented:
- `FnOnce`, applies to closures that can be called once
- `FnMut`, applies to closures that don't move captured values out of their body but might mutate the captured values. Can be called more than once
- `Fn`, applies to closures that don't move captured values out of their body and don't mutate captured values, as well as closures that capture nothing from the environment. Can be called more than once without mutating the environment

| Trait    | Captures by               | Can be called            |
| -------- | ------------------------- | ------------------------ |
| `FnOnce` | Moving (consuming) values | Only once                |
| `FnMut`  | Mutable reference         | Multiple times (mutably) |
| `Fn`     | Immutable reference       | Multiple times           |

`move` and `Fn`/`FnMut`/`FnOnce` closures are orthogonal:
- `move` vs non-`move` is about **fields** of the compiled struct have the same type as the original vs are references
- `Fn`/`FnMut`/`FnOnce` is about whether the **call method** of the compiled struct has a receiver which is `&self` vs `&mut self` vs `self` 

---

#flashcards/rust

What is a closure in Rust?::An anonymous function that can be saved in a variable or passed as an argument to other functions, and can capture values from its surrounding scope.
<!--SR:!2026-03-01,3,250-->

What are the 3 ways a closure can capture values from the environment?::Borrow immutably, borrow mutably, or take ownership (with the `move` keyword).
<!--SR:!2026-02-27,1,230-->

What determines how a closure captures values from the environment?::What the closure's body does with those values.
<!--SR:!2026-03-01,3,250-->

What does `FnOnce` mean for a closure?::The closure can only be called once, because it moves captured values out of its body.
<!--SR:!2026-02-27,1,230-->

What does `FnMut` mean for a closure?::The closure can be called more than once and may mutate captured values, but doesn't move them out.
<!--SR:!2026-03-01,3,250-->

What does `Fn` mean for a closure?::The closure can be called more than once without moving or mutating captured values (or it captures nothing).
<!--SR:!2026-02-27,1,230-->

What does the `move` keyword do in a closure?::Forces the closure to take ownership of captured values instead of borrowing them.
<!--SR:!2026-02-27,1,230-->

Are `move` and `Fn`/`FnMut`/`FnOnce` orthogonal?::Yes. `move` determines whether the compiled struct holds owned values or references; `Fn`/`FnMut`/`FnOnce` determines whether the call method takes `&self`, `&mut self`, or `self`.
<!--SR:!2026-02-27,1,230-->