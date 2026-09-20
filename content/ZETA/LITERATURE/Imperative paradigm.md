---
up:
tags:
  - atomic
created: 2025-04-13 18:20
---
In the imperative paradigm, a program is a sequence of steps that mutate state to produce a result.

example:
```rust
let mut sum = 0;
for i in 1..11 {
    sum += i;
}
println!("{sum}");
```

# See also 
- [[Functional Programming programs are trees of expressions, not sequences of steps]] — the contrasting paradigm: describes *what* to compute via expression trees, no mutable state 
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — function composition is the mechanism functional programming uses instead of sequential steps