---
up:
  - "[[A randomized algorithm uses random(S) as a primitive, correctness and running time are random variables]]"
tags:
created: 2026-05-15 14:19
---

> An edge cut in a multigraph $G=(V,E)$ is a multisubset $C\subseteq E$ such that $G^\prime = (V, E - C)$ is not connected

In other words, it partitions the vertices of a graph into two disjoint subsets. 

The **Min-Cut problem** aims to find the edge-cut of minimum cardinality, defined as $|C| = \sum_{e\in E} m_e$.

# See also
- [[Tree Recursion branches at each level]] — Karger-Stein, the optimised min-cut algorithm, is a recursive algorithm that branches into two subproblems at each level; the edge cut is what it is trying to preserve through each contraction
- [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]] — the key lemma in Karger's correctness proof uses Pigeonhole: the minimum degree of any vertex is at least |C*|, which gives a lower bound on |E|; this bounds the probability of contracting a min-cut edge
- [[Clustering is the task of grouping a set of objects]] — min-cut and graph clustering are dual problems: clustering groups similar vertices together, min-cut finds the weakest boundary between groups; spectral clustering uses eigenvectors of the Laplacian, which is defined by the cut structure

# References
- https://mathworld.wolfram.com/EdgeCut.html
- Advanced algorithm design notes, [[Randomized Algorithmic Techniques]]
