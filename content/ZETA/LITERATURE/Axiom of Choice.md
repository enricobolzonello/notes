---
connections:
  - "[[Foundational Crisis of Mathematics]]"
reference: https://en.wikipedia.org/wiki/Axiom_of_choice
tags: 
type: literature_note
created: 2025-05-16 10:32
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

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

# References
- Jech, Thomas J. (1977). About the axiom of choice. In Jon Barwise, Handbook of mathematical logic. New York: North-Holland. pp. 90--345.
- https://en.wikipedia.org/wiki/Axiom_of_choice