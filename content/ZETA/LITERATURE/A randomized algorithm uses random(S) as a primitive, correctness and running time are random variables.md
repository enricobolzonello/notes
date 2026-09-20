---
up:
tags:
  - atomic
created: 2026-05-15 12:39
---

Randomized algorithms use `X=random(S)` as a primitive, so $X$ is a random variable uniformly distributed over $S$. Each random is considered independent. 

Correctness and running time are random variables:
-  $P(A\text{ is correct on instances of size }n)$﻿
- $P(T_A(n)\ge f(n))$﻿, where $T_A(n)$﻿ is the random variable associated to worst-case complexity
- $E[T_A(n)]=\Theta(g(n))$

Usually there are two techniques:
- LAS VEGAS, which are always correct and the randomization only affects running time
- MONTE CARLO, in which algorithms can be incorrect ($P(i\not\Pi A(i))>0$﻿) and may affect running time

# See also
- [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]] - many randomized correctness proofs use Pigeonhole to show that a bad event is improbable because it requires too many coincidences

# References
- Advanced Algorithm Design notes, [[Randomized Algorithmic Techniques]]