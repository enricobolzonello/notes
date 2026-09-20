---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - permanent_note
created: 2025-01-31 11:31
---
# Recursion
Neither tail [[Linear Recursion is a chain of deferred operations|Linear Recursion is a chain of deferred operations]] nor [[Tail Call optimization replaces call with jmp|tail call optimization]] are guaranteed by Rust. Specifically, not by Rust directly, but the LLVM compiler, although there have been [progresses](https://reviews.llvm.org/D99517) in the guarantees

# References
- https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html
- https://stackoverflow.com/questions/59257543/when-is-tail-recursion-guaranteed-in-rust/59258170#59258170