---
up:
  - "[[Paradoxes Broke 19th-Century Math and Set Theory Rebuilt It — Until Gödel]]"
tags:
  - atomic
created: 2025-05-16 10:17
---


> [!important] 
> Every set theory that contains an unrestricted comprehension principle leads to contradictions

--> unrestricted comprehension principle: there is a set of all and only the objects that have that property

# Counter example 
Let $R$ be the set of all sets that are not members of themselves. If $R$ is not a member of itself, then its definition entails that it is a member of itself.
Yet if it is a member of itself, then it is not a member of itself since it is the set of all sets that are not members of themselves.
In symbols:
$$
\text{Let } R=\{x|x\not\in x\}, \text{then } R\in R \Longleftrightarrow R\not\in R
$$
which is a paradox.


# See also
- [[Paradoxes Broke 19th-Century Math and Set Theory Rebuilt It — Until Gödel]] — Russell's Paradox is one of the central paradoxes that triggered the foundational crisis; it directly destroyed naive set theory's unrestricted comprehension principle
- [[Axiom of Choice - for each family of non-empty sets it exists a function f(S) in S]] — the Axiom of Choice is part of ZFC, the restricted set theory built specifically to avoid paradoxes like Russell's; the restriction replaces unrestricted comprehension with carefully bounded axioms
- [[Hilbert's program was to formalize all of math, disproven by Gödel]] — Hilbert's program was motivated partly by Russell's Paradox: if naive set theory is inconsistent, we need a complete and provably consistent formal system to replace it
- [[Gödel's incompleteness theorems]] — Gödel's response to Hilbert's program; Russell's Paradox showed naive set theory was broken, Gödel showed the fix (formal axiomatic systems) couldn't be complete either
- [[Modus ponens, P è vero quindi Q è vero]] — the paradox is a breakdown of inference: R∈R and R∉R are both derivable by modus ponens from the same definition, which means the system proves a contradiction and collapses

# References
- https://en.wikipedia.org/wiki/Russell%27s_paradox