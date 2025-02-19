---
connections: 
tags:
  - permanent_note
type: permanent_note
created: 2025-01-31 11:31
---
 
# Recursion
Neither tail recursion nor [[Tail Calls|tail call optimization]] are guaranteed by Rust. Specifically, not by Rust directly, but the LLVM compiler, although there have been [progresses](https://reviews.llvm.org/D99517) in the guarantees

# References
- https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html
- https://stackoverflow.com/questions/59257543/when-is-tail-recursion-guaranteed-in-rust/59258170#59258170