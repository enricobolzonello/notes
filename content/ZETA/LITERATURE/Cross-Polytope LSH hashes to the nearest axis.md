---
up:
  - "[[An LSH Family maps closer points to the same bucket with higher probability]]"
tags:
  - atomic
created: 2025-01-03 10:58
---
Efficient and practical [[An LSH Family maps closer points to the same bucket with higher probability|LSH family]] for the [[Angular Distance is the true metric version of cosine distance|angular distance]].

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

# See also 
- [[An LSH Family Maps Closer Points to the Same Bucket With Higher Probability]] — Cross-Polytope LSH is an instance of this definition for angular distance on the unit sphere 
- [[Angular Distance is the true metric version of cosine distance]] — the distance metric $\tau = \|p-q\|$ in the theorem is angular distance; the collision probability decays with angular distance 
- [[SimHash - h(x) = sign(wᵀx)]] — SimHash is the simpler hyperplane LSH for the same distance; Cross-Polytope achieves the same theoretical bounds but is more efficient in practice with multiprobe
- [[Natural Batching, start a batch as soon as requests arrive, complete it when full or queue is empty]] — multiprobe is natural batching applied to LSH queries: instead of processing one bucket per table, greedily process nearby buckets until enough candidates are found
# References 
- [[@andoniPracticalOptimalLSH2015a]]