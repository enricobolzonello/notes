---
area: CLANN
summary: 
tags: area/clann/cross_polytope_lsh
type: area_note
created: 2025-01-03 10:58
---
# [[2. CLANN]] 
# Overview
Efficient and practical [[LSH Family]] for the [[Angular Distance]].

> [!DEFINITION]
> Consider the following hash family $\mathcal{H}$ for points on a unit sphere $S^{d-1} \subset \mathbb{R}^d$. Let $A\in \mathbb{R}^{d\times d}$ be a random matrix with i.i.d. Gaussian entries. To hash a point $x\in S^{d-1}$, we compute $y=\frac{Ax}{||Ax||}\in S^{d-1}$ and then find the point closest to $y$ from $\{\pm e_i\}_{1\le i\le d}$, where $e_i$ is the i-th standard basis vector of $R^d$

The collision probability for two points for this hash family function is bound in the following theorem:
> [!THEOREM]
> Suppose that $p,q\in S^{d-1}$ are such that $||p-q||=\tau$ where $0<\tau<2$. Then: 
> $$
> \ln \frac{1}{P_{h\sim \mathcal{H}} [h(p)=h(q)]} = \frac{\tau^2}{4-\tau^2}\cdot \ln d + O_\tau (\ln \ln d)
> $$

This theorem shows that the cross-polytope LSH achieves the same bounds as the theoretically optimal LSH for the sphere, in particular a data structure with sub-quadratic space and sublinear query time can be achieved. But this version is not practical, as applying a random rotation takes time proportional to $d^2$, which is clearly not feasible for large $d$. 

To solve this issue, the authors used pseudo-random rotations, applying the transformation $x\mapsto HD_3HD_2HD_1x$, where $H$ is the Hadamard transform and $D_i$ is a random diagonal $\pm1$-matrix, with the Fast Hadamard Transform (FHT) which takes time $O(d\log d)$ and space $O(d)$. Even this can be too slow for sparse vectors so, before performing the pseudo-random rotation, the dimensionality is reduced from $d$ to $d^\prime\ll d$ with feature hashing, taking down evaluation time to $O(s+d^\prime \log d^\prime)$. 

But even this is not enough, the critical component to make cross-polytope much more efficient than hyperplane LSH is multiprobe, where candidates from multiple cells in each table are considered. Without this modification, cross-polytope performs worse than hyperplane while with multiprobe it has a speed up of nearly $11\times$. 

# References 
- [[@andoniPracticalOptimalLSH2015a]]