---
up:
tags:
  - atomic
created: 2026-08-10 22:30
---
Compilers optimize data representation only when these two criteria are met:
1. all relevant functions are inlined
2. transformations have to be semantically reasonable 
	- depends on the language, but an heuristic could be "data has to be on the stack"

If this happens, then an aggregate data structure can be exploded into its component parts, and optimized as if they were all local variables.

# See also
- [[Tail Call optimization replaces call with jmp]] — TCO is another compiler transformation that requires similar preconditions: the call must be in tail position (semantically reasonable) and the compiler must be able to see it (analogous to inlining)
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — exploding an aggregate into local variables is a cache locality optimization: instead of following a pointer to a heap-allocated struct, all fields live in registers or on the stack, maximally cache-friendly
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — exploding aggregates eliminates false sharing risk entirely: once fields are local variables, they live in separate registers or stack slots with no shared cache line

# References
- https://www.tedinski.com/2019/01/29/data-structures-are-fundamental.html