---
connections: 
reference: 
tags:
  - type/term
  - theme/mathematics
type: literature_note
created: 2024-12-20 21:18
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!Definition]
> Smallest D such that for any radius r and point $u\in S$, all points in the ball of radius r centered at u are included in the union of at most $2^D$ balls of radius $r/2$ centered at suitable points
>  — [[@ceccarelloSolving$k$centerClustering2021]]


In computational geometry, doubling measures allow algorithms that were originally designed for Euclidean settings to be generalized and applied effectively in more abstract spaces.
For example, in the HNSW method for the [[(k, δ) Nearest Neighbor problem|k-NN problem]] the doubling property ensures that the graph does not become too dense, which helps in bounding the search time.

For clustering and k-NN this property ensures that the metric space behaves in a controlled way, specifically:
1) **bounding the number of neighbors**, since in a space with a doubling measure they are limited
2) **efficient partitioning**, doubling spaces can be often efficiently partitioned or embedded into lower-dimensional spaces with bounded distortion
3) **scalability**, ensures that computational resources grow in a controlled manner


## Iteratively Covering Smaller Balls

> Given the definition, we can apply it iteratively to break down ball of radius $r$ into smaller and smaller balls

Recursively cover each ball of radius $r$ with $2^D$ balls of half the radius $r/2$, then each of those with $2^D$ balls of radius $r/4$ and so on. After $k$ subdivisions, **the radius of each ball becomes $r/2^k$ and the number of balls needed is $(2^D)^k$.**

In terms of $\epsilon$, we want to cover a ball of radius $r$ with smaller balls of radius $\epsilon r$, with $\epsilon\le 1$. Set $\epsilon=1/2^k$ so that $\epsilon r = r/2^k$. Solving for $k$, we get $k=\log_2(1/\epsilon)$.

Substituting $k=\log_2(1/\epsilon)$ on the number of balls we get:
$$
2^{kD} = 2^{D\log_2(1/\epsilon)} = \bigg(\frac{1}{\epsilon}\bigg)^D
$$


























