---
connections: 
reference: https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html
tags:
  - theme/engineering
  - theme/low-level
type: literature_note
created: 2025-01-29 23:33
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!DEFINITION]
> Any function that is in the tail position, meaning the final action be be performed before a function returns

Without **Tail Call Optimization** (TCO) the callee $g()$ returns back to the caller $f()$ and creates a new stack frame and pushes the return address.

With TCO enables, instead of a `call` instruction the compiler emits a `jmp`.  $g()$ returns directly to whatever function called $f()$, as if it were part of the same function. 

What it does:
- reduces stack memory from $O(n)$ to $O(1)$ when making $n$ consecutive tail calls. Reduces stack overflow occurences
- `call` has more performance overhead than `jmp`

Based on a paper: https://dspace.mit.edu/handle/1721.1/5753

The problem is that it's not guaranteed, so the compiler can go back to an actual `call`. 
