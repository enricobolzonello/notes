---
area: CLANN
summary: Definition of LSH family
tags:
  - area/clann
  - theme/approximate-nearest-neighbor
  - theme/lsh
  - type/term
type:
  - area_note
created: 2024-12-14 20:26
---
# [[2. CLANN]] 
# Overview

> [!DEFINITION] 
> A locality-sensitive hash (LSH) family H is family of functions h : X → R, such that for each pair x, y ∈ X and a random h ∈ H, for arbitrary q ∈ X, whenever dist(q, x) ≤ dist(q, y) we have p(q, x) := Pr[h(q) = h(x)] ≥ Pr[h(q) = h(y)].
> — Aumüller, Martin, Tobias Christiani, Rasmus Pagh, e Michael Vesterli. «PUFFINN: Parameterless and Universally Fast Finding of Nearest Neighbors». arXiv, 28 giugno 2019. https://doi.org/10.48550/arXiv.1906.12211.


# Alternative Definition

> [!DEFINITION]
> A family $\mathcal{H}=\{h:S\rightarrow U\}$ is called $(r_1,r_2,p_1,p_2)$-sensitive for $D$ [^1] if for any $v,q\in S$:
> - if $v\in B(q,r_1)$ then $P[h(q)=h(v)\ge p_1$
> - if $v\not\in B(q,r_2)$ then $P[h(q)=h(v)]\le p_2$
> 
> to be useful, $p_1>p_2$ and $r_1<r_2$
> — M. Datar, N. Immorlica, P. Indyk, e V. S. Mirrokni, «Locality-sensitive hashing scheme based on p-stable distributions», in _Proceedings of the twentieth annual symposium on Computational geometry_, in SCG ’04. New York, NY, USA: Association for Computing Machinery, giu. 2004, pp. 253–262. doi: [10.1145/997817.997857](https://doi.org/10.1145/997817.997857).


## For Euclidean Distance

> [!DEFINITION]
> The LSH function for a point $\vec{x}\in \mathbb{R}^d$ is defined as:
> $$
h(x) = \Bigg\lfloor \frac{\vec{a}\cdot \vec{x}+b}{r}\Bigg\rfloor
> $$
> where $\vec{a}\in \mathbb{R}^d$ is a random vector with coordinates sampled from the normal distribution, $b$ is a random scalar distributed uniformly in $[0,r]$ and $r$ is a parameter

This function projects input points on a random direction, shifts them and then quantizes the shifted projections according to the parameter $r$, as you can see in the following figure: