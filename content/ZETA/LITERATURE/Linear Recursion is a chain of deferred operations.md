---
up:
  - "[[Recursion]]"
tags:
  - atomic
created: 2025-11-18 21:30
---
> A recursive process is characterized by a shape of expansions followed by contraction. It can also be thought as a *chain of deferred operations*. 
> - The expansion builds up a chain of deferred operations
> - The contraction performs the operations

Recursive *process* is not the same as recursive *procedure*:
- procedure = syntactic fact that the procedure definition refers to the procedure itself
- process = how the process evolves, not about the syntax

These are not the same: a recursive procedure can produce an iterative process (if [[Tail Call optimization replaces call with jmp|tail-call optimised]]) and a tail-recursive procedure is still syntactically recursive.

# See also 
- [[Tail Call optimization replaces call with jmp]] — TCO eliminates the chain of deferred operations: instead of expanding and contracting, the process stays flat; linear recursion becomes an iterative process in O(1) stack space 
- [[A process in operating systems is a program in execution]] — the stack section is where the chain of deferred operations lives; each deferred call pushes a new frame, which is why deep linear recursion causes stack overflow 
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — the chain of deferred operations is function composition in time: g(f(x)) defers g until f returns, which is exactly the expansion phase