---
tags:
  - atomic
up:
  - "[[Paradoxes Broke 19th-Century Math and Set Theory Rebuilt It — Until Gödel]]"
created: 2025-05-16 10:32
---
Informally:
> given any collection of non-empty sets, it is possible to construct a new set by choosing one element from each set, even if the collection is infinite

>[!definition] Axiom
>Let $\mathcal{F}=\{A_i:i\in I\}$ be a collection of pairwise disjoint nonempty sets. There exists a set $C=\{x_i:i\in I\}$ which has exactly one element $x_i$ common with each $A_i \in \mathcal{F}$

Initially it generated many discussions. Why?
It postulates existence of a set $C$ which has certain properties, for example *choosing* one element, but does not say how to construct.
And, until the late 19th century, existence in mathematics was synonymous with construction.

The modern formulation of the principle is due to Zermelo, which was used to prove the total ordering of sets:

>[!definition] Axiom of Choice
>For every family $\mathcal{F}$ of nonempty sets, there exists a function $f$ such that $f(S)\in S$ for each set $S$ in the family $\mathcal{F}$

where the function $f$ is called a choice function on $\mathcal{F}$.

The two formulations are equivalent.

# See also
- [[Paradoxes Broke 19th-Century Math and Set Theory Rebuilt It — Until Gödel]] — the Axiom of Choice is one of the foundational axioms set theory adopted to resolve the crisis; it became the standard foundation of modern mathematics
- [[Russell's Paradox — R = {x s.t. x∉x} Implies R∈R ⟺ R∉R]] — Russell's Paradox is why unrestricted comprehension failed; the Axiom of Choice is part of the restricted, carefully constructed replacement (ZFC set theory)
- [[Ogni Ontologia Resta Cieca Finché non Chiarisce Prima il Senso dell'Essere]] — the controversy around the Axiom of Choice mirrors Heidegger's critique: mathematicians were doing set theory without clarifying what "existence" means — the Axiom postulates existence without construction
- [[Modus ponens, P è vero quindi Q è vero]] — modus ponens is the inference rule; the Axiom of Choice is a non-constructive existence axiom that cannot be derived by inference alone — it must be assumed
- [[Hilbert's program was to formalize all of math, disproven by Gödel]] — the Axiom of Choice is exactly the kind of axiom Hilbert's program wanted to ground everything on; Gödel later showed the Axiom of Choice is independent of ZF — it can neither be proved nor disproved from the other axioms

# References
- Jech, Thomas J. (1977). About the axiom of choice. In Jon Barwise, Handbook of mathematical logic. New York: North-Holland. pp. 90--345.
- https://en.wikipedia.org/wiki/Axiom_of_choice