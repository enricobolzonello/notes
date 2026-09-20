---
connections: 
reference: 
tags:
  - type/term
  - theme/mathematics
type: literature_note
created: 2024-12-20 19:26
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!DEFINITION]
> Cosine similarity is the cosine of the angle between vectors; that is, it is the dot product of the vectors divided by the product of their lengths
> — https://en.wikipedia.org/wiki/Cosine_similarity


$$
\text{cosine sim.} = \cos(\theta) = \frac{A\cdot B}{||A|| \cdot ||B||}
$$
where $||X||$ is the magnitude of vector $X$, which in general is defined as $||x||=\sqrt{x_1^2 +...+x_n^2}$.


The **cosine distance** is defined as follows:
$$
\text{dist}(A,B) = \sqrt{(A-B)\cdot (A-B)} = \sqrt{2(1-\text{sim}(A,B)}
$$
but often it is defined without the square root, since it maintains the same relative order between the elements and it is easier to compute:
$$
\text{dist}(A,B) = 1-\text{sim}(A,B)
$$
Note that the cosine distance is **not a true metric distance**, since it does not have the triangular inequality and violates the coindicence axiom.
Convert to euclidean or [[Angular Distance]].