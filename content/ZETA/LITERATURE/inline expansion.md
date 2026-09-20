---
up:
tags:
created: 2026-06-16 17:53
---
> **inline expansion** is a compiler optimization that replaces a function call site with the body of the called function. 

Some inlining improve speed at minor cost of space, but too much will hurt speed due to inlined code consuming too much of the instruction cache.

- best for small functions that are called often

main benefit:
- allow further optimizations as better optimization is possible on larger functions
	- overall lower cache miss ratio for small caches
	- inverse or no effect for large cache sizes

# References
- https://en.wikipedia.org/wiki/Inline_expansion