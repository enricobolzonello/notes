---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2025-01-29 23:33
---

> [!DEFINITION]
> Any function that is in the tail position, meaning the final action be be performed before a function returns

Without **Tail Call Optimization** (TCO) the callee $g()$ returns back to the caller $f()$ and creates a new stack frame and pushes the return address.

With TCO enables, instead of a `call` instruction the compiler emits a `jmp`.  $g()$ returns directly to whatever function called $f()$, as if it were part of the same function. 

What it does:
- reduces stack memory from $O(n)$ to $O(1)$ when making $n$ consecutive tail calls. Reduces stack overflow occurences
- `call` has more performance overhead than `jmp`

Based on a paper: https://dspace.mit.edu/handle/1721.1/5753

The problem is that it's not guaranteed, so the compiler can go back to an actual `call`. 

# See also
- [[A process in operating systems is a program in execution]] — TCO works directly on the stack section of the process memory layout: without it, n consecutive tail calls push n frames; with it, the stack stays flat
- [[Linear Recursion is a chain of deferred operations]] — TCO is what converts a linear recursive process into an iterative one: the chain of deferred operations collapses to a single frame because each call jumps rather than nesting
- [[Functional Programming programs are trees of expressions, not sequences of steps]] — functional programming relies heavily on recursion instead of loops; TCO is what makes this viable at scale without stack overflow
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — TCO reduces the number of stack frames that need saving during a context switch; fewer frames means cheaper context switches in recursive call chains
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — a flat stack (O(1) frames) is more cache-friendly than a deep stack (O(n) frames): fewer cache lines needed, more predictable memory access pattern

# References
- https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html