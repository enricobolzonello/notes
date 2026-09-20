---
connections:
tags:
  - permanent_note
  - theme/engineering
  - theme/rust
type: permanent_note
created: 2026-02-26 11:04
---

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


```rust
fn main() {
    let mut count = 0;
    let name = String::from("Enrico");

    // Case 1: non-move, Fn
    // Body only reads `name` -> fields are references, call takes &self
    let print_name = || println!("{name}");
    print_name();
    print_name(); // can call many times

    // Case 2: non-move, FnMut
    // Body mutates `count` -> field is &mut count, call takes &mut self
    let mut increment = || { count += 1; };
    increment();
    increment();

    // Case 3: non-move, FnOnce
    // Body moves `name` out (via drop or into another owner) -> call takes self by value
    let consume_name = || { let s = name; drop(s); };
    consume_name();
    // consume_name(); // ERROR: value used after move — struct itself was consumed

    // Case 4: move, Fn
    // `move` forces owned fields, but body only *reads* -> still &self
    let name2 = String::from("Bolzo");
    let print_owned = move || println!("{name2}");
    print_owned();
    print_owned(); // fine, still Fn even though it owns the String

    // Case 5: move, FnMut
    let mut count2 = 0;
    let mut inc_owned = move || { count2 += 1; println!("{count2}"); };
    inc_owned();
    inc_owned();

    // Case 6: move, FnOnce
    let name3 = String::from("Rust");
    let consume_owned = move || { let s = name3; drop(s); };
    consume_owned();
    // consume_owned(); // ERROR: FnOnce, can't call twice
}
```

## The `Fn*` hierarchy is a subtrait chain: `Fn : FnMut : FnOnce`

The three traits aren't disjoint — they nest. `Fn` is a subtrait of `FnMut` is a subtrait of `FnOnce`:

$$\texttt{Fn} : \texttt{FnMut} : \texttt{FnOnce}$$

So every `Fn` closure is *also* an `FnMut` and an `FnOnce` (like every `Cat` is an `Animal`). The set of `Fn` closures is the **smallest**; the set of `FnOnce` closures is the **largest** (every closure is callable at least once).

The governing principle — **a trait bound is a *demand*, and the weaker the demand, the larger the set of things that satisfy it**:
- `FnOnce` = "callable at least once" → weak demand → *every* closure qualifies (largest set).
- `Fn` = "callable repeatedly with only shared access" → strong demand → mutating/consuming closures fail it (smallest set).

**The names mislead.** `FnOnce` *sounds* more limited than `Fn` (only once vs. always), so intuition says its set is smaller — but the name describes the *closure's* limitation, while the bound describes the *caller's* demand. A caller asking only for "once" is being *less* demanding, so *more* closures qualify. Name and set-size point opposite ways — this is the classic trap (getting the direction backwards).

### Consequences (advice)
- **Accept the most general `Fn*` that works.** Call the closure once → take `FnOnce`; call repeatedly + mutate → `FnMut`; call repeatedly read-only → `Fn`. Weakest bound your code can live with = widest range of callers can pass their closure.
- **Prefer `Fn*` bounds over bare `fn` pointers.** A `fn` pointer is the bottom of the hierarchy (empty captured environment), so demanding `fn` is *maximally* restrictive — it rejects every capturing closure. `fn` auto-implements all three `Fn*` traits, so an `Fn*` bound accepts both plain functions and closures.


---

#flashcards/rust

What is a closure in Rust?::An anonymous function that can be saved in a variable or passed as an argument to other functions, and can capture values from its surrounding scope.
<!--SR:!2026-09-28,13,210-->

What are the 3 ways a closure can capture values from the environment?::Borrow immutably, borrow mutably, or take ownership (with the `move` keyword).
<!--SR:!2026-09-19,4,190-->

What determines how a closure captures values from the environment?::What the closure's body does with those values.
<!--SR:!2026-10-01,23,230-->

What does `FnOnce` mean for a closure?::The closure can only be called once, because it moves captured values out of its body.
<!--SR:!2026-09-15,0,150-->

What does `FnMut` mean for a closure?::The closure can be called more than once and may mutate captured values, but doesn't move them out.
<!--SR:!2026-09-17,2,230-->

What does `Fn` mean for a closure?::The closure can be called more than once without moving or mutating captured values (or it captures nothing).
<!--SR:!2026-09-17,2,230-->

What does the `move` keyword do in a closure?::Forces the closure to take ownership of captured values instead of borrowing them.
<!--SR:!2026-09-19,4,190-->

Are `move` and `Fn`/`FnMut`/`FnOnce` orthogonal?::Yes. `move` determines whether the compiled struct holds owned values or references; `Fn`/`FnMut`/`FnOnce` determines whether the call method takes `&self`, `&mut self`, or `self`.

What is the subtrait direction of the `Fn*` hierarchy, and which bound is "most general"?::`Fn : FnMut : FnOnce` — every `Fn` is also `FnMut` and `FnOnce`. `FnOnce` is the weakest demand / largest set, so it's the most general bound to accept as a parameter.

Why prefer an `Fn*` trait bound over a bare `fn` pointer parameter?::A `fn` pointer is the bottom of the hierarchy (empty captured environment), so demanding `fn` is the most restrictive — it rejects every capturing closure. An `Fn*` bound accepts both plain functions and capturing closures.
<!--SR:!2026-09-18,3,170-->